# Analyze tracks in major

# [bit.ly/gmaj](https://bit.ly/gmaj)

0. Let's try to sing [chords](https://book-one.hooktheory.com/section/chords)

## Show

0. [talks/sound.md](../sound.md)
1. AnthemScore - for spectrogram
2. RipX
3. All-in-One: [HuggingFace](https://huggingface.co/spaces/vpavlenko/all-in-one), [Music Dissector](https://music-dissector.vercel.app/)

## How to analyze

[Homework](https://github.com/vpavlenko/study-music/blob/main/talks/f0/01_major.md#homework)

1. Search on Hooktheory. If it's not there, aim for uploading it there
2. Check https://www.ultimate-guitar.com/
3. Search for midi.
4. If it's absent - try transcription tools:

[**Tools for transcription**](../../parts/transcription.md) 

# Obsolete notes

- Joe Yamada "Chasing the Dream" (solo piano) - easy major harmony, melody + arpeggios, mostly on 4-chord progressions
- Unplayable drum midi tracks is fixed by copy-pasting drum track onto a fresh track in signal. Probably, some important setup midi messages are created this way

## [Carver Commodore - Drown Me In Emotions](https://www.youtube.com/watch?v=bLaipK9lisc)

- Found in everynoise's scan. Feels like it's in major.
- [Search for chords](https://www.google.com/search?q=Carver+Commodore+-+Drown+Me+In+Emotions+chords). 
- Found [chordify](https://chordify.net/chords/carver-commodore-drown-me-in-emotions-official-music-video-carver-commodore) - it's auto chords. It's a rare track, so neither midi nor human-entered chords.
- It's in E Major, because if we assume that, we get verse IV-I-V and chorus I-(iii)-ii-V, pretty straightforward.
- `youtube-dl -x --audio-format "best" --audio-quality 0 --embed-thumbnail --add-metadata https://www.youtube.com/watch\?v\=bLaipK9lisc` or youtubepi



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


