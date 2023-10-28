# Hypothesis

VGM OSTs from 2000s onwards do use modes other than the standard minor and major, and this usage correlates somehow with the game theme/plot/universe.

Context: Western music is mostly written either in major or in minor mode (natural+harmonic). Maybe 90%. But the other 10% are written in other keys (scales, modes): phrygian, dorian, mixolydian, pentatonic, blues. The mode is an easy theoretical concept to train yourself to hear in a piece of music. It contributes a lot to the vibe of the track and its extra-musical connotations. It may convey emotions (if music can convey any).

Historically, medieval music was written in modes way more often than now. From 17th century onwards modes are used rarely. Their usage is higher in some traditional Western cultures like Celtic music. This may reinforce composers to exploit modes to portray a certain game setting.

First approach: let's learn to recognize modes on VGM soundtracks.

# Pipeline
1. Download VGM OST (an audio file).
2. Run basic-pitch to get raw midi conversion.
3. Run some script that outputs segments of possible dorian / phrygian modes.
4. Check by listening if that's really the case.

# First tasks
1. Listen to some Youtube videos explaining dorian / phrygian scales. Also [Hooktheory](https://book-two.hooktheory.com/section/dorian-mode). Also Chiptheory: [1](https://vpavlenko.github.io/chiptheory/search/scale/phrygian) [2](https://vpavlenko.github.io/chiptheory/search/scale/dorian) [3](https://vpavlenko.github.io/chiptheory/search/harmony/dorian_shuttle) [4](https://vpavlenko.github.io/chiptheory/search/harmony/phrygian_shuttle)
2. Choose a soundtrack and download its audio.
3. Run basic-pitch (web version or standalone). Maybe run demucs beforehand. It's best to work on small chunks, 1 to 5 minutes long. Btw check my write-up on [transcription](https://github.com/vpavlenko/study-music/blob/main/parts/transcription.md)
4. Browse the midi output using either [signal](https://signal.vercel.app/) or any DAW or Musescore. Think how to write a script that determines modes considering this noisy output.
5. Try to write such a script and run it on one hour of soundtrack. Listen to the segments marked as being in modes. Are they?

The script may be the hardest part. Consult papers, ask GPT4 vigorously and use the following ways to simplify the task:
1. Try to find any dorian modes in [the corpus of Irish tunes](http://www.oldmusicproject.com/oneils1.html). How well is the distinction between dorian and natural minor defined?
2. Write a simpler script that determines the parts of midi that are in minor vs. in major. How well is this thing defined? Search for algorithms that detect minor or major keys. There's Krumhansl-Schmuckler key-finding model - find modern citations of their article, try to understand the SOTA approach if an audio source is given.

# Literature
- [Albrecht 2014: A Statistical Approach to Tracing the Historical Development of Major and Minor Pitch Distributions, 1400-1750](https://www.dropbox.com/scl/fi/qiybsaymwg1dm4eg8ktmh/albrecht2014.pdf?rlkey=wp0yuxl118ztfbuf7rj1ehux7&dl=0)
- https://mtosmt.org/issues/mto.18.24.2/mto.18.24.2.white.html
- https://arxiv.org/pdf/1706.02921.pdf
- https://www.google.com/search?q=neural+network+determine+key+of+audio
