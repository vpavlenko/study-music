# Transcription and analysis

## Audio to midi



### RipX

<img src="https://github.com/vpavlenko/study-music/assets/1491908/59d0aedb-2545-4a50-924e-25be97585457" width="1000">


Suppose you have a wav/mp3 of Western music and you want to produce a midi.

Well, take [RipX DeepRemix](https://hitnmix.com/remix-software/) and you'll get a certain quality.  


Questions:
- Does it use spleeter? Is demucs better?
- How does it draw precise Melodyne-like pitch contours? I see them in a demo of Basic Pitch, but they're lost on midi export?
- How does it estimate midi notes?
- Does it extract midi notes first and then Q-filters a certain part over it for playback? Or how does it split a part into harmonics/notes in a polyphonic texture?

Other:
- [TuneFlow](https://tuneflow.com/) promises audio to MIDI - is it good?


The rest of this doc focuses on how to build your own RipX from existing tools.

### Demixing

[Demucs v4 (2022)](https://github.com/facebookresearch/demucs) [▶️](https://www.google.com/search?q=demucs+online) splits into bass, drums, vocals and other. Previously [spleeter (2020)](https://github.com/deezer/spleeter) was widely used - it can do additional fifth stem with piano.




### Beat tracking

Next, you want to get beats and downbeats (measures) - in millisecond timestamps. And verse/chorus/bridge form annotation, ideally. Well, since July 2023 you 
can get [All-in-One (2023)](https://github.com/mir-aidj/all-in-one) [🤗](https://huggingface.co/spaces/taejunkim/all-in-one):

![image](https://github.com/vpavlenko/study-music/assets/1491908/220fc35e-db5c-430c-9735-a0c2da4d8375)

There's also a [nice visualizer](https://github.com/tae-jun/music-dissector):

<img width="1728" alt="Screenshot 2023-09-05 at 11 14 02" src="https://github.com/vpavlenko/study-music/assets/1491908/bb28f70b-313d-4574-afd3-9c64ddefbcfb">

Other:
- [WaveBeat](https://github.com/csteinmetz1/wavebeat)
- [omnizart beat](https://music-and-culture-technology-lab.github.io/omnizart-doc/) - requires midi, [has](https://github.com/Music-and-Culture-Technology-Lab/omnizart/issues/100) [issues](https://github.com/Music-and-Culture-Technology-Lab/omnizart/issues/104) [running](https://github.com/Music-and-Culture-Technology-Lab/omnizart/pull/103) "beat" now
- [Spotify Track's Audio Analysis API](https://developer.spotify.com/documentation/web-api/reference/get-audio-analysis) - gives bars/beats, sections, key

Questions:
- does All-in-One improve madmom significantly?
- is Spotify's API any good?

### Pitch recognition

For each of non-drum parts you want pitch recognition. General-purpose SOTA is [Basic Pitch](https://basicpitch.spotify.com/):

<img width="600" alt="Screenshot 2023-09-05 at 11 17 27" src="https://github.com/vpavlenko/study-music/assets/1491908/5fc44b23-9689-446a-b6e6-aaee7ae7af29">

Other: 
- [sheetsage (2022)](https://github.com/chrisdonahue/sheetsage) for melody - although I tested it, and results are far from great


#### Piano

Historically, a lot of effort was put specifically into solo piano recognition. So now we have [Onsets and Frames (2018)](https://magenta.tensorflow.org/onsets-frames) [🐟](https://piano-scribe.glitch.me/)

<img width="600" alt="Screenshot 2023-09-05 at 11 37 00" src="https://github.com/vpavlenko/study-music/assets/1491908/3c164332-53c4-4bbc-a7a8-2f13601b1eda">

Other:
- [Bytedance (2020)](https://github.com/bytedance/piano_transcription)

### Automatic drum tracking

- omnizart drum
- [Magenta OaF Drums](https://magenta.tensorflow.org/oaf-drums)

### Assemble midi

Doing it straight away via [MT3](https://github.com/magenta/mt3) gives very bizarre results.

So: get your parts Basic Pitched, get your drums separately, get your downbeat timings, and then use gpt4 `mido` scripting / [midisox](https://pjb.com.au/midi/midisox.html) / Ableton (XML-hackable!) to merge parts back together.

Caveat: Basic Pitch produces midi with resolution 480, whereas omnizart outputs in 220. Merging them can lead to errors when using online tools


### Harmonic analysis: chords, keys

- [Omnizart chord (2019)](https://replicate.com/e7mac/omnizart)
- [Sheet Sage (2022)](https://github.com/chrisdonahue/sheetsage) - easy to run, chords are mostly right
- key: [Spotify API](https://developer.spotify.com/documentation/web-api/reference/get-audio-analysis)

Possibly, with "omnizart chord" and any beat tracking you can already build a clone of [Chordify](https://chordify.net/) and even improve it by adding form annotation.

<img width="700" alt="Screenshot 2023-09-05 at 11 56 05" src="https://github.com/vpavlenko/study-music/assets/1491908/b47afde3-5aeb-4345-b75a-0dedb1275c38">

## PDF sheet music to MusicXML (Optical Music Recognition, OMR)

[It's tough and not solved holistically yet.](https://www.google.com/search?q=challenges+omr+paper+music+survey)


# Read more

- https://paperswithcode.com/task/music-transcription/latest
