Here's a refined algorithm for tokenizing a Lakh-flavoured pop music MIDI file for music theory processing.

Suppose we generate measure 20. Suppose it's identical to measure 16. We encode this with a token "repeat_m_4", where 4 is a relative distance back. At all times choose the closest measure to reference back (exception: if you can repeat "repeat_m_i", repeat it).

0. Only tokenize note onsets. Drop durations (assume full legato), velocities, pitch bends, instrument changes. Ideally sort-group-map tracks to semantic ones. Consider quantizing onsets to nearest 32nd.
1. Tokenizer works measure by measure. (This is a dubious tradeoff, alternatively we can encode many measures of repetitions in a single track simultaneously to leverage BPE on it, at the risk of not giving enough local context for other tracks on what's going on).
2. Emit "repeat_m_i" if there was a measure back in time with exactly the same content. (Optimize for an efficient merge of several such references in a corpus-wise BPE for chorus repetitions.)
3. If there was a measure back in time with exactly the same content but transposed, emit "repeat_m_i" "transpose_j" where j is a relative pitch.
4. Otherwise, we tokenize a measure track by track. Emit "new_measure".
5. Tracks are always generated in the same order: drums, bass, all chord tracks, all melodic tracks, all ornamentation tracks.
6. Emit "track_N".
7. Emit "repeat_m_i" if there was a measure back in time at this track with exactly the same content.
8. Emit "repeat_m_i" "transpose_j" if there was a measure back in time at this track with the same content but transposed.
9. Emit "repeat_track_L_m_0" if this track's content is doubling some other track in this very measure that's already encoded.
10. Silently skip encoding tracks that don't have any onsets in this measure.
98. Maybe mix repetitions + adding manual notes: optimize track sorting to leverage this.
99. If all else fails, emit "manual_track_N" and encode measure note by note in two tokens: MIDI pitch and a time shift from measure start or the last onset in this measure. MIDI pitch can be relative to the last known pitch in this track. Emit time shift only once per chord. So, a power chord as a first note in the measure after a 5/16 rest is encoded as "time_shift_5/16" "relative_pitch_0" "relative_pitch_7" "relative_pitch_12". If there wasn't any pitch in this track before, input an absolute MIDI pitch. Important: relative pitch for a first note in a chord starts from the *lowest note* of the previous chord, relative pitch for other notes in a chord is relative to notes below it.
