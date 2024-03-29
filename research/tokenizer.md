Scroll down to V2 below. V1 is very poorly written.

# V1

Here's a refined algorithm for tokenizing a Lakh-flavoured pop music MIDI file for music theory processing.

Suppose we generate measure 20. Suppose it's identical to measure 16. We encode this with a token "repeat_m_4", where 4 is a relative distance back. At all times choose the closest measure to reference back (exception: if you can repeat "repeat_m_i" many times, simply repeat it).

0. If you can calculate measure adjustments (incomplete measures, measure shifts) or a total modulation, emit it. It's hard computationally, though.
0. Only tokenize note onsets. Drop durations (assume full legato), velocities, pitch bends, instrument changes. Consider quantizing onsets to nearest 32nd. For string pad tracks with onsets slightly before measure starts (as calculated by histogram of onset positions) offset a track to the right to compensate (since this is timbral and not semantical).
1. Sort-group-map tracks to semantic ones.
2. Tokenizer works measure by measure. (This is a dubious tradeoff, alternatively we can encode many measures of repetitions in a single track simultaneously to leverage BPE on it, at the risk of not giving enough local context for other tracks on what's going on).
3. Emit "repeat_m_i" if there was a measure back in time with exactly the same content. (Optimize for an efficient merge of several such references in a corpus-wise BPE for chorus repetitions.)
4. If there was a measure back in time with exactly the same content but transposed, emit "repeat_m_i" "transpose_j" where j is a relative pitch.
5. Otherwise, we tokenize a measure track by track. Emit "new_measure".
6. Tracks are always (?) generated in the same order: drums, bass, all chord tracks, all melodic tracks, all ornamentation tracks. The order should be causal. What's easier - predict drum -> bass or bass -> drum? Is bass -> chord the correct way, even though chord sometimes syncopates to the previous measure?
7. Emit "track_N".
8. Emit "repeat_m_i" if there was a measure back in time at this track with exactly the same content.
9. Emit "repeat_m_i" "transpose_j" if there was a measure back in time at this track with the same content but transposed.
10. Emit "repeat_track_L_m_0" if this track's content is doubling some other track in this very measure that's already encoded.
11. Silently skip encoding tracks that don't have any onsets in this measure.
98. Maybe mix repetitions + adding manual notes: optimize track sorting to leverage this.
99. If all else fails, emit "manual_track_N" and encode measure note by note in two tokens: MIDI pitch and a time shift from measure start or the last onset in this measure.
    - MIDI pitch can be relative to the last known pitch in this track
    - Emit time shift only once per chord
    - So, a power chord as a first note in the measure after a 5/16 rest is encoded as "time_shift_5/16" "relative_pitch_0" "relative_pitch_7" "relative_pitch_12"
    - If there wasn't any pitch in this track before, input a relative MIDI pitch to the lowest note of a previous chord in this generation.
    - Probably calculate something relative to the bass and let the bass track the harmony, idk. Eg. harmony tracks always relate to the bass note, but melody relate to itself.
    - If it's the very first pitch in this file, emit absolute pitch.
    - A time shift emitted without a relative pitch is a last note/chord repetition.
    - Important: relative pitch for a first note in a chord starts from the *lowest note* of the previous chord, relative pitch for other notes in a chord is relative to notes below it.
    - Drum track pitches should probably be absolute or even somehow available for semantic extraction of bass drum / snare / hi-hat in case of variation in the data set.
    - Drum pitches shouldn't stack into chords: horizontal BPE (eg. straight 16th hi-hats) are more semantic
    

One expected consequence of relative pitch encoding is that a prior tonic estimation isn't necessary, at all, whereas the NN trained on this tokenization will probably be useful in inferring the tonic afterwards.

The next question is how to leverage basic-pitch recognition on Spotify data to further increase the model. I suspect that there are easier and harder genres, and we might start with easier ones.

Not all MIDI files are equal. First, focus on narrowing a dataset by excluding classical music, solo piano works and jazz.

# V2

After some experiments, I'm trying to write up a better tokenizer.

A tokenizer works on a grid of measures and channels (aka tracks aka voices). A cell is a measure+channel pair as a bunch of onsets. Eg. cell m.20 ch.3.

A tokenizer makes two passes through all cells via two nested loops:
```
for measure in measures:
    for channel in channels:
        cells[measure][channel] = encode(cells[measure][channel], ...context)
```
    
In the first pass, it transforms raw MIDI onsets into the intermediate representation (IR). In the second pass, it works on IR and tries to replace as much of it as possible with reference tokens marking repetition/doubling/transposition/reuse of ideas of any sort.


## First pass: cell-wise MIDI -> IR

The main idea: strumming patterns, drum patterns and melodic patterns should be referenced inside a song using special reference tokens. In order to do that, every instance of a pattern should be decoupled into a bag of notes and a pattern skeleton. A bag of notes is several MIDI numbers of notes. Inside a skeleton, they are referenced via a local numbering as `s_0`, `s_1`, `s_2`... from lowest to highest. 

Ideally, this decoupling should happen on units of harmonic rhythm (for chord tracks) and most common melodic lengths (for melodic tracks). For a slower harmonic/phrase rhythm, it shouldn't be an issue due to the second pass.

### Bag of notes

In Western pop songs, there is usually a bass track that has a good informational reference for other tracks to refer to. Also, this track is usually monophonic. So, I propose to encode bass notes from left to right throughout the entire track by relative references. This way the typical patterns like 2-5-1-6, chromatic descending, diatonic descending etc. will all naturally be visible, even though we don't make any tonic inference preprocessing.

Then a key assumption is that all other tracks get the most useful information for pattern extraction by referring to the first bass note in the same measure. 
(An exception to that is an anticipation bass note which started in a previous measure but is hearable through the measure start.)

Let's encode a bag of notes for any cell above the bass. Let's find a **pivot** MIDI number - a lowest transposition of a first bass note (+0, +12, +24, ...) such that it's either in a bag of notes or the bag of notes is as close to it as possible. Then this pivot is encoded as `oct_0`/`oct_1`/`oct_2` etc., and the bag of notes is encoded as `rel_-5`, `rel_0`, `rel_4` - this example is for a major chord in second inversion. (An alternative encoding could be to encode notes relative to one another - exposing intervals rather than chord degrees.)

### Pattern

In most MIDI files we have a good grid of measures and beats that is constructed from time signature and BPM events. Therefore, every onset can be encoded as `beat.subdivision`.

For better pattern extraction it's probably better to work with time shifts between two onsets rather than with absolute times within a measure. 

A major scale in 8ths will look like this: `s_0 t_0.00 n_+1 t_0.50 n_+1 t_0.50 n_+1 0.50 n_+1 0.50 ...`, assuming its bag of words is something like `oct_2 rel_0 rel_2 rel_4 rel_5 rel_7 ...`. A `s_0`/`s_1`/etc. tells which note from the bag of notes starts the pattern. Then notes in a pattern are references relative to their order within the bag of notes as `n±1`, `n±2` etc.  A `t_0.00` is an absolute coordinate for a first onset inside a measure. (Is there a better way to unify `t_` and `ts_`?) 

Two shorthands are used:
- simultaneous notes (a chord) are grouped together under a single time shift that's put after the notes
- if a chord is repeated several times, we don't repeat its notes and just add a new time shift

A swing eights strumming will look like this: `n_0 n_1 n_2 t_0.00 ts_0.67 ts_0.33 ts_0.67 ts_0.33 ...`. 

### Drums

Drums are unlike notes. Kick, snare and hi-hats have somewhat independent patterns that can be stacked on top of each other. On the other hand, all three hi-hat events are maybe connected.

For now we can encode them as `drum_35 t_0.00 ts_2.00 drum_42 t_1.00 ts_3.00 ...`.

## Second pass: IR -> IR with repetitions tokenized

Again, the outer loop goes over measures, the inner loop goes over channels (in order from lowest to highest average channel pitch), assuming all previous cells are already encoded.

If this particular cell is already a part of a large repetition found and encoded previously, we skip it. Otherwise, we try to find the best strategy to encode its most probable semantic relation to the content seen before (in previous measures + in cells below this one in the same measure). There's a semantic hierarchy on repetitions:

(Whenever we encode that a target sequence of cells partly repeats a source sequence of cells, we assume that they don't overlap.)


1. Find a longest sequence of previous cells in this channel such that the sequence starting from the current one is equal to them. Let it start D measures ago and be of length L. Intuitively, if L is large, than larger Ds have semantic value. Whereas it's not feasible to refer to a single chord 50 measures ago just because it's the same. Emit `repeat_D_L`.
3. Find a longest sequence of cells in another channel C starting just below such that the the sequence of equal length L starting from the current cell is an exact doubling up to an octave transposition. Emit `double_C_L`.
2. Find if this cell is identical to previous one in absolute note content (not relative to the bass), check if that's a riff that continues to N more cells. Emit `riff_N`.
5. Find a longest sequence of previous cells in this channel such that the sequence starting from the current one is their transposition to an interval N. This may be the case after a modulation. However, a sequence of IV chords after a sequence of I chords can also be recognized as such. (Which we should probably avoid.) Let's probably consider the length of at least 4, idk. Emit `transpose_D_L_N`. (A `repeat_D_L` is a special case of transposition with N = 0. My gut feeling is that a diagnosed doubling, especially of longer length, is more important than a transposition.)

Here comes the coolest part. Three previous steps couldn't help us encoding a transposed melody or a repeated strumming on a different chord quality *within a key*. This is because our tokenizer has no notion of scales. To find it, we try to encode a pattern and a bag of words separately.

Intuitively, encoding a pattern is more important because a pattern is more likely a uniquely used in this piece, whereas a harmony (a bag of notes) can more likely be generalized when processing a large corpus. (Although this is probably not relevant.)

4. If a pattern of this cell isn't covered by any previous multi-cell pattern repetition token, find a longest sequence of previous patterns ... and emit `pattern_D_L`. Probably not very important for very short patterns (of 1 or 2 notes) 50 measures ago.
5. Similarly, for a bag of words, find and emit `harmony_D_L`.
6. And only then, if either part of the information about the cell isn't covered, we emit it verbatim in the IR form.

What else can now be reused? Some partial repetitions of notes between two measures. Although this is harder to tokenize with a room for generalization: we'll need to remove and add arbitrary notes, and the transformer should be very confused on the small dataset like the one we have.

Also, we don't encode diagonal repetitions - which start some time ago in a different channel. We don't know how common it is - it's certainly common in classical orchestral music.
