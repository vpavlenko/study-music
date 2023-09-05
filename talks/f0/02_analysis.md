# Analyze tracks in major

## [Carver Commodore - Drown Me In Emotions](https://www.youtube.com/watch?v=bLaipK9lisc)

- Found in everynoise's scan. Feels like it's in major.
- [Search for chords](https://www.google.com/search?q=Carver+Commodore+-+Drown+Me+In+Emotions+chords). 
- Found [chordify](https://chordify.net/chords/carver-commodore-drown-me-in-emotions-official-music-video-carver-commodore) - it's auto chords. It's a rare track, so neither midi nor human-entered chords.
- It's in E Major, because if we assume that, we get verse IV-I-V and chorus I-(iii)-ii-V, pretty straightforward.
- `youtube-dl -x --audio-format "best" --audio-quality 0 --embed-thumbnail --add-metadata https://www.youtube.com/watch\?v\=bLaipK9lisc`
- [Stem Separation Comparison Dec 2022](https://www.youtube.com/watch?v=gl5AKCgMSSc)
   - Start with [demucs](https://github.com/facebookresearch/demucs) as it's free and cli-based
- What do we want to extract from this track? Drums, bass guitar, vocals. Can we separate [two guitars](https://www.youtube.com/watch?v=h6ytkmZEEUU) - lead from rhythm?
- Then feed the output of demucs to [Basic Pitch](https://basicpitch.spotify.com/) (bass)
- Try [Omnizart for drums](). Omnizart uses spleeter under the hood, and maybe replacing it with demucs can give better results.
   - Also [MT3](https://github.com/magenta/mt3)
   - Also see [MusicNetEM](https://benadar293.github.io/)
- Merge midi files:
   - Caveat: Basic Pitch produces midi with resolution 480, whereas omnizart outputs in 220. Merging them can lead to errors when using online tools
   - Can merge midi tracks in Ableton
   - Can also use [midisox](https://pjb.com.au/midi/midisox.html)
- Unplayable drum midi tracks is fixed by copy-pasting drum track onto a fresh track in signal. Probably, some important setup midi messages are created this way
- Maybe check ISMIR Slack
- [All-In-One Music Structure Analyzer](https://github.com/mir-aidj/all-in-one)

![download](https://github.com/vpavlenko/study-music/assets/1491908/49b1933f-7a8c-46f2-addf-5a093ff0ad7b)


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

### Cog

- [Docker installation for cog on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

## WaveBeat
   - Run on Ubuntu 20.04 with python3.8, numpy==1.19 and madmom==0.16.1 recompiled after installing numpy. [Installation](https://gist.github.com/vpavlenko/6d88bd19b4017c0bf63d70ca5a9738e7)
   - [Deploying wavebeat on Replicate: ChatGPT](https://chat.openai.com/share/de2f0f76-a6a0-4029-896e-16a37706f7ea)
      - [fork](https://github.com/vpavlenko/wavebeat), [Currently fails](https://gist.github.com/vpavlenko/6c4982ea9920ad0c46aa035b84afa300)


