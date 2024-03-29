> In many respects, the differences between music and language are so great that it is difficult to know how to compare them. Both are systems of human communication, and both are universal across cultures. Beyond this, it is not obvious how to proceed.
> 
> [David Temperley. Music and Language](http://davidtemperley.com/wp-content/uploads/2022/02/temperley-arl22.pdf)

> Every time I fire a linguist, the performance of the speech recognizer goes up.
> 
> Frederick Jelinek

# Angry rant

<img src="https://github.com/vpavlenko/study-music/assets/1491908/91162d50-fc17-41e2-b516-9780cc051f7a" width="400px">

These are eight basic types of strokes in Chinese. All characters are built using those strokes. (A rude oversimplification.)

As an analogy, current attempts to train transformers for music generation (Chinese text generation, in this analogy) are made of these assumptions:
- Chinese language is best modeled if we feed Chinese characters tokenized as a sequence of strokes. It's cool that there are only eight strokes. (Ignore octave equivalence, scales, chords, riffs and any structures, at all. Especially the repetition.)
- However, strokes written by different people should be different strokes for our tokenizer. That's not an issue, since the transformer Will Figure It Out. (Velocities should be preserved at all cost.)
- Texts rotated 5%-10%-20%-50% to the left are all different texts, albeit in the same language. No need to align them on a preprocessing stage. Instead, let's augment the dataset by rotating each image in 12 different angles. (No tonic inference and transposing to C before tokenization stage.)
- Chinese language is very flexible, many sequences of characters sound good, it doesn't have any meaning, and we don't need to know anything about its structure. There are people who speak Chinese, we'll only use them at the evaluation stage by politely showing our generated music and asking them to review. (Music theory doesn't exist and should not be studied, at all.)

Engineers are treating this subject in a very colonial way. Remember what Andrej Karpathy put in the first place: ["Become one with the data"](https://karpathy.github.io/2019/04/25/recipe/).

One inspiring example: [Museformer](https://ai-muzic.github.io/museformer/) handles hypermeter in a nice way by attending to the 4th/8th/16th bar in the past. They did this by looking at the data.

However, beware of [The Bitter Lesson](http://www.incompleteideas.net/IncIdeas/BitterLesson.html)

See [**tokenizer.md**](tokenizer.md) for a very poorly written proposal of a better tokenizer. Or see a brainstorming below. [Or see the bat 🦇](https://github.com/vpavlenko/bat)

# Types of NNs for music theory

There's a lot of music produced. I want it to be organized into searchable and annotated corpora. 
Eg. all MIDI files, all sheet music, all spotify audio.

## Multimodal

[LLark](https://github.com/spotify-research/llark) crosses an English-language LLM and several embeddings for music to make a chat bot capable of answering questions on a specific audio uploaded. This is a great interface. 

Music theory is more about texts written by people about pieces and genre (books, papers) than coding tools ready to be crossed. So a similar system for music theory can be an English-language LLM fine-tuned on chunks of music theory books and [journals](https://www.mtosmt.org/docs/index-author.php) along with examples discussed in particular passages fed in some symbolic form (eg. [MidiTok](https://github.com/Natooz/MidiTok)).

## Single-modal

Transformers are [widely fed](https://github.com/affige/genmusic_demo_list) on corpora of MIDI. And maybe they learn/extract all theoretical concepts along the way: keys, chords, voicings, voice-leading rules, formal structures, composers/genres. This information can't be extracted directly from the music generation setting, as transformers per se simply generate the next MIDI symbol. The corpus itself doesn't have any annotation on structures that we're interested in.

The very interesting question is whether the transformer itself can mine new structures overlooked by researchers yet, akin to a [tonic added-sixth chord](https://www.mtosmt.org/issues/mto.23.29.2/mto.23.29.2.martin.html)

One interesting thing we can readily extract from a transformer architecture is distribution of [expectation](https://mitpress.mit.edu/9780262582780/sweet-anticipation/), surprises and uncertainties in the next events. "Show me the weirdest place in this song", "generate a more expected measure"

## Tokenization

GPT-4's [tiktoken](https://github.com/openai/tiktoken) has around 100k tokens - English words, common chunks from programming languages, chops of Russian words, integers and other unicode characters. This preprocessing allows the transformer to extract patterns on a higher level. 

[Here's what MidiTok supports.](https://miditok.readthedocs.io/en/latest/tokenizations.html) And here's [MidiTok BPE paper](https://arxiv.org/pdf/2301.11975.pdf). Is there room for improvement?

- Should we have a separate token for a power chord in all popular durations?
- Should we have a separate token for Vsus4-V(7), Iadd6 (in many voicings)
- Should we decompose progressions from voicings (learn ii-IV-V simultaneously for power chords, triads, diatonic seventh chords and dominant seventh chords)?
- Should we tokenize repetitions and have a direct token for "verse 2 = verse 1", "m.5 = m.1", "repeat last chord transposed -2 down"?
- How do we tokenize an exact repetition transposed a semitone up, harmonic or melodic?
- Should we decompose rhythm from note content and have tokens for rhythmic repetiton/reference in a new phrase? Should we have a token for 3+3+2?

Sentences in a natural language are positionally akin to non-metrical improvisation. Periods can come after an arbitrary amount of tokens. Music, however, is very regular in time. Should every note have a metrical position embedding ("fourth beat", "third measure of a formal function") in addition to standard transformer's positional embeddings?

Should we [infer tonic](https://github.com/vpavlenko/rawl/blob/master/src/corpus/tonics.json) at the tokenization stage and transpose everything to C? Not doing that would be disastrous and akin to feeding an English-language transformer equal parts of standard English, its rot13 version and all other alphabet rotations. Another analogy: imagine a world in which we notate vowels differently depending on absolute pitch with which they were pronounced by an author of every text.

In contrast, not everything from MIDI should be preserved with great care. As in a natural language, we don't notate intonation in writing. So, note onsets as conveying rhythm are very important, but note durations/offsets - less so and can probably be omitted at all (?). Same with onsets are shifted a notch to compensate for MIDI attack of a particular instrument (which font rendering is likely not the one that the file author optimized for). This is a difference between tokenization for generation and tokenization for theory, similar to speech synthesis where a system without intonation would produce a very robotic and unpleasant sound, whereas no word-contour intonation is needed for GPT-4.

The tracks in a MIDI file should also be curated. In some MIDI files, several tracks double each other purely for timbral effects, fully or partially. Doubling should probably be removed to reduce number of tokens used. Also, [GM](https://en.wikipedia.org/wiki/General_MIDI) has 128 instruments, whereas semantically there are way less categories - bass, chords, vocal, vocal dubbing, ornamentation, instrumental solo.

Hypermetrical placement of chords can help inferring the right tonic, see [David Temperley. Communicative Pressure and the Evolution of
Musical Styles](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=2fef2324caaf826d07c277612abf88a1f5103ea2):

<img width="600" alt="Screenshot 2023-12-16 at 20 18 24" src="https://github.com/vpavlenko/study-music/assets/1491908/abf3f280-caae-4e22-a263-6bf05d1586eb">
<img width="600" alt="Screenshot 2023-12-16 at 20 18 43" src="https://github.com/vpavlenko/study-music/assets/1491908/ed3d9675-2384-4aa0-b810-d291d79814b7">

See also:
- [Adarsh Kumar1 and Pedro Sarmento. From Words to Music: A Study of Subword Tokenization Techniques in Symbolic Music Generation](https://arxiv.org/pdf/2304.08953.pdf)
- [Research of Nathan Fradet](https://scholar.google.com/citations?user=YdSSbXoAAAAJ&hl=fr)

## Music theory aware tokenization algorithm



1. **Determine measures and beats**

I'm not sure it's very important as long as the drum track is encoded very semantically. Measures and beats in current MIDI tracks have [various issues](https://docs.google.com/document/d/1sW_XU2OW2UK0WWu_rW49XYA9pC_hgmp4bNtTo8ze6hE/edit)


2. **Determine local tonic and modulation regions**

This should be done using a LLM that is fine-tuned for this task. Therefore, our algorithm is bootstrapping: we use some simpler (theory-agnostic) tokenizer to determine tonics as a part of another tokenization process.

Where to get a corpus for it:
- RS200 (De Clercq - Temperley)
- GiantSteps
- Spotify API provides a key which can then be mapped to MetaMIDI
- MIDI files where key signature is present and is not C major
- [rawl tonics](https://github.com/vpavlenko/rawl/blob/master/src/corpus/tonics.json) for Lakh files

To fine-tune an LLM, transpose the dataset to all 12 pitch classes

3. **Determine harmonies for every measure/beat**

It's unclear how should we encode a harmony: i, i5, I5, i7, i7(9), i7(9)/3 etc.

4. **Encode tracks**

For every track and every measure, one of several encoding strategies may be picked:
- Encode relative to the harmony
- Encode relative to the key. May be good for melodies. A key - a pitch class collection - should be additionally inferred and stored
- Encode relative to previous content. This may be both as "verbatim repeat" and also as a "sequence" relative either to key or to harmony
- Encode relative to a simultaneous content in another track. There's a lot of doubling in MIDI-files
- Encode using some sort of a per-file BPE strategies (i.e. with a dictionary local to a specific MIDI-file)

### In another terms

Possibly, the better way to tokenize MIDI-files is first to try to write programs that generate those MIDI files. Probably, music theory is exactly the condensed knowledge of
how to structure computer programs generating MIDI files so that a program to generate each individual file is pretty small. So, interpretation is inferring a DSL from a MIDI file (which is possibly the mental model of composer/transcriber) and we should probably train NNs on DSLs rather than on direct MIDI files. I.e. we probably shouldn't wait until NN learns music theory, because it may forget to tell us about it afterwards.

## Very general method

If all of this sounds very sophisticated and failing to let the AI figure out all the data dependencies on their own, consider adding just a single set of tokens: "repeat Xth previous measure in this channel".

<img width="1700" alt="Screenshot 2023-12-25 at 00 42 26" src="https://github.com/vpavlenko/study-music/assets/1491908/cddf4109-9177-4114-bea1-3679fd6a22f4">


## Inspiration

David Temperley has [an article](https://www.annualreviews.org/doi/full/10.1146/annurev-linguistics-031220-121126) on parallels and differences between music and language. [Also](https://www.academia.edu/162993/Language_and_Music_as_Cognitive_Systems)
