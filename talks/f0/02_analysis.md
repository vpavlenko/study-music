# Analyze tracks in major

## [Carver Commodore - Drown Me In Emotions](https://www.youtube.com/watch?v=bLaipK9lisc)

- Found in everynoise's scan. Feels like it's in major.
- [Search for chords](https://www.google.com/search?q=Carver+Commodore+-+Drown+Me+In+Emotions+chords). 
- Found [chordify](https://chordify.net/chords/carver-commodore-drown-me-in-emotions-official-music-video-carver-commodore) - it's auto chords. It's a rare track, so neither midi nor human-entered chords.
- It's in E Major, because if we assume that, we get verse IV-I-V and chorus I-(iii)-ii-V, pretty straightforward.
- How do we extract the melody? Let's try demucs and RipX.
- `youtube-dl -x --audio-format "best" --audio-quality 0 --embed-thumbnail --add-metadata https://www.youtube.com/watch\?v\=bLaipK9lisc`
- [Stem Separation Comparison Dec 2022](https://www.youtube.com/watch?v=gl5AKCgMSSc)
   - Start with [demucs](https://github.com/facebookresearch/demucs) as it's free and cli-based
- What do we want to extract from this track? Drums, bass guitar, vocals. Can we separate [two guitars](https://www.youtube.com/watch?v=h6ytkmZEEUU) - lead from rhythm?
- Then feed the output of demucs to [Basic Pitch](https://basicpitch.spotify.com/) (bass)
- "Drum stems audio to midi" is a separate task which may have some good solution
- Maybe Ableton
- Try Omnizart. Omnizart uses spleeter under the hood, and maybe replacing it with demucs can give better results. Also [MT3](https://github.com/magenta/mt3)
   - Also see [MusicNetEM](https://benadar293.github.io/)
- For piano: either [bytedance](https://github.com/bytedance/piano_transcription) or "Onsets and Frames"
- [Omnizart for drums](https://replicate.com/e7mac/omnizart)
- [Merge midi files](https://www.ofoct.com/merge-midi-files) - select "Add Tracks" mode
- What's the correct way to merge files given tempo stuff and some other discrepances?
- Caveat: Basic Pitch produces midi with resolution 480, whereas omnizart outputs in 220. Merging them can lead to errors
- Also please try RipX
- Hint: can merge midi tracks in Ableton

## Singing

Can we sing something on this meeting?


# Obsolete notes

## Install omnizart

If fails due to PyYAML: [run this](https://github.com/yaml/pyyaml/issues/601#issuecomment-1693730229). (It also fails on colab).

I try on `pyenv global 3.8.10`.

`python3 -m pip install tensorflow-macos`

Maybe I should fix omnizart installation right in a colab.

Try on Colab. The issue: since May 2023, the default colab python is 3.10, and the original colab for omnizart is for 3.8. So there are two options:
- try to port it to 3.10 (which will be obsolete in 1-2 years again)
- try to bring the env version back to 3.8 (which requires installing an old ipykernel)

### Port it to 3.10

P
madmom 0.16 will crash on `from collections import MutableSequence`

### Bring env to 3.8

Find the right ipykernel install commands.
