# Hypothesis

VGM OSTs from 2000s onwards do use modes other than the standard minor and major, and this usage correlates somehow with the game theme/plot/universe.

First approach: let's learn to recognize modes on VGM soundtracks.

Pipeline:
1. Download VGM OST (an audio file).
2. Run basic-pitch to get raw midi conversion.
3. Run some script that outputs segments of possible dorian / phrygian modes.
4. Check by listening if that's really the case.

First tasks:
1. Listen to some Youtube videos explaining dorian / phrygian scales. Also [Hooktheory](https://book-two.hooktheory.com/section/dorian-mode). Also [Ch](https://vpavlenko.github.io/chiptheory/search/scale/phrygian)[ip](https://vpavlenko.github.io/chiptheory/search/scale/dorian)[the](https://vpavlenko.github.io/chiptheory/search/harmony/dorian_shuttle)[ory](https://vpavlenko.github.io/chiptheory/search/harmony/phrygian_shuttle)
2. Choose a soundtrack and download its audio.
3. Run basic-pitch (web version or standalone). It's best to work on small chunks, 1 to 5 minutes long. Btw check my write-up on [transcription]()
