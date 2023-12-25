Here's a refined algorithm for tokenizing a Lakh-flavoured pop music MIDI file for music theory processing.

Suppose we generate measure 20. Suppose it's identical to measure 16. We encode this with a token "repeat_m_4", where 4 is a relative distance back.

0. Only tokenize note onsets. Drop durations (assume full legato), velocities, pitch bends, instrument changes. Ideally sort-group-map tracks to semantic ones.
1. Tokenizer works measure by measure.
2. Emit "repeat_m_i" if there was a measure back in time with exactly the same content.
3. Otherwise, we tokenize a measure track by track. Emit "new_measure".
4. Tracks are always generated in the same order: drums, bass, all chord tracks, all melodic tracks, all ornamentation tracks.
5. Emit "repeat_track_N_m_i" if there was a measure back in time at this track with exactly the same content.
6. Emit "repeat_track_L_m_0" if this track's content is doubling some other track in this very measure that's already encoded.
7. 
99. If all else fails, encode measure note by note in two tokens: MIDI pitch and intra-measure location (1.25 is a sixth sixteenth-note, so beat.percent)
