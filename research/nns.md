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

GPT-4's [tiktoken](https://github.com/openai/tiktoken) has around 100k tokens - English words, common chunks from programming languages, chops of Russian words, integers and other unicode characters. This preprocessing allows the transformer to extract patterns on a higher level. What's the good tokenization for MIDI, can we improve [REMI+](https://arxiv.org/pdf/2201.10936.pdf)? 
- Should we have a separate token for Vsus4-V(7), Iadd6 (in many voicings)
- Should we decompose progressions from voicings (learn ii-IV-V simultaneously for power chords, triads, diatonic seventh chords and dominant seventh chords)?
- Should we tokenize repetitions and have a direct token for "verse 2 = verse 1", "m.5 = m.1"?
- How do we tokenize an exact repetition transposed a semitone up, harmonic or melodic?
- Should we decompose rhythm from note content and have tokens for rhythmic repetiton/reference in a new phrase? Should we have a token for 3+3+2?

Sentences in a natural language are positionally akin to non-metrical improvisation. Periods can come after an arbitrary amount of tokens. Music, however, is very regular in time. Should every note have a metrical position embedding ("fourth beat", "third measure of a formal function") in addition to standard transformer's positional embeddings?

Should we infer tonic at the tokenization stage and transpose everything to C? Not doing that would be disastrous and akin to feeding an English-language transformer equal parts of standard English, its rot13 version and all other alphabet rotations. Another analogy: imagine a world in which we notate vowels differently depending on absolute pitch with which they were pronounced by an author of every text.

In contrast, not everything from MIDI should be preserved with great care. As in a natural language, we don't notate intonation in writing. So, note onsets as conveying rhythm are very important, but note durations/offsets - less so and can probably be omitted at all (?). Same with onsets are shifted a notch to compensate for MIDI attack of a particular instrument (which font rendering is likely not the one that the file author optimized for). This is a difference between tokenization for generation and tokenization for theory, similar to speech synthesis where a system without intonation would produce a very robotic and unpleasant sound, whereas no word-contour intonation is needed for GPT-4.

The tracks in a MIDI file should also be curated. In some MIDI files, several tracks double each other purely for timbral effects, fully or partially. Doubling should probably be removed to reduce number of tokens used. Also, [GM](https://en.wikipedia.org/wiki/General_MIDI) has 128 instruments, whereas semantically there are way less categories - bass, chords, vocal, vocal dubbing, ornamentation, instrumental solo.

Hypermetrical placement of chords can help inferring the right tonic, see [David Temperley. Communicative Pressure and the Evolution of
Musical Styles](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=2fef2324caaf826d07c277612abf88a1f5103ea2):

<img width="600" alt="Screenshot 2023-12-16 at 20 18 24" src="https://github.com/vpavlenko/study-music/assets/1491908/abf3f280-caae-4e22-a263-6bf05d1586eb">
<img width="600" alt="Screenshot 2023-12-16 at 20 18 43" src="https://github.com/vpavlenko/study-music/assets/1491908/ed3d9675-2384-4aa0-b810-d291d79814b7">



## Inspiration

David Temperley has [an article](https://www.annualreviews.org/doi/full/10.1146/annurev-linguistics-031220-121126) on parallels and differences between music and language. [Also](https://www.academia.edu/162993/Language_and_Music_as_Cognitive_Systems)
