Here's a refined algorithm for tokenizing a Lakh-flavoured pop music MIDI file for music theory processing.

Suppose we generate measure 20. Suppose it's identical to measure 16. We encode this with a token "repeat_m_4", where 4 is a relative distance back.

0. Only tokenize note onsets. Drop durations (assume full legato), velocities, pitch bends, instrument changes. Ideally sort-group-map tracks to semantic ones.
1. Tokenizer works measure by measure.
2. Emit "repeat_m_i" if there was a measure back in time with exactly the same content.
3. Otherwise, we tokenize a measure track by track.
