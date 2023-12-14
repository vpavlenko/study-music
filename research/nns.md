# Types of NNs for music theory

There's a lot of music produced. I want it to be organized into searchable and annotated corpora. 
Eg. all MIDI files, all sheet music, all spotify audio.

## Multimodal

[LLark](https://github.com/spotify-research/llark) crosses an English-language LLM and several embeddings for music to make a chat bot capable of answering questions on a specific audio uploaded. This is a great interface. 

Music theory is more about texts written by people about pieces and genre (books, papers) than coding tools ready to be crossed. So a similar system for music theory can be an English-language LLM fine-tuned on chunks of music theory books and [journals](https://www.mtosmt.org/docs/index-author.php) along with examples discussed in particular passages fed in some symbolic form (eg. [MidiTok](https://github.com/Natooz/MidiTok)).

## Tokenization

GPT-4's [tiktoken](https://github.com/openai/tiktoken) has around 100k tokens - English words, common chunks from programming languages, chops of Russian words, integers and other unicode characters. This preprocessing allows the transformer to extract patterns on a higher level. What's the good tokenization for MIDI, can we improve [REMI+](https://arxiv.org/pdf/2201.10936.pdf)? 
- Should we have a separate token for Vsus4-V(7), Iadd6 (in many voicings)
- should we decompose progressions from voicings (learn ii-IV-V simultaneously for power chords, triads, diatonic seventh chords and dominant seventh chords)?
- Should we tokenize repetitions and have a direct token for "verse 2 = verse 1"?
- How do we tokenize an exact repetition a semitone up, harmonic or melodic?
- Should we decompose rhythm from note content and have tokens for rhythmic repetiton/reference in a new phrase? Should we have a token for 3+3+2?

Sentences in a natural language are positionally akin to non-metrical improvisation. Periods can come after an arbitrary amount of tokens. Music, however, is very regular in time. Should every note have a metrical position embedding ("fourth beat", "third measure of a formal function") in addition to standard transformer's positional embeddings?

Should we infer tonic at the tokenization stage and transpose everything to C? Not doing that would be disastrous and akin to feeding an English-language transformer equal parts of standard English, its rot13 version and all other alphabet rotations. Another analogy: imagine a world in which we notate vowels differently depending on absolute pitch with which they were pronounced by an author of every text.

## Single-modal

Transformers are [widely fed](https://github.com/affige/genmusic_demo_list) on corpora of MIDI. And maybe they learn/extract all theoretical concepts along the way: keys, chords, voicings, voice-leading rules, formal structures, composers/genres. This information can't be extracted directly from the music generation setting, as transformers per se simply generate the next MIDI symbol. The corpus itself doesn't have any annotation on structures that we're interested in.

The very interesting question is whether the transformer itself can mine new structures overlooked by researchers yet, akin to a [tonic added-sixth chord](https://www.mtosmt.org/issues/mto.23.29.2/mto.23.29.2.martin.html)

One interesting thing we can readily extract from a transformer architecture is distribution of [expectation](https://mitpress.mit.edu/9780262582780/sweet-anticipation/), surprises and uncertainties in the next events. "Show me the weirdest place in this song", "generate a more expected measure"
