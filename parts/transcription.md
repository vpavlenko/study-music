# Transcription

## Audio to midi



### RipX

<img src="https://github.com/vpavlenko/study-music/assets/1491908/59d0aedb-2545-4a50-924e-25be97585457" width="1000">


Suppose you have a wav/mp3 of Western music and you want to produce a midi.

Well, take [RipX DeepRemix](https://hitnmix.com/remix-software/) and you'll get a certain quality.  


Questions:
- Does it use spleeter? Is demucs better?
- How does it draw precise melodyne-like pitch contours?
- How does it estimate midi notes?
- Does it extract midi notes first and then Q-filters a certain part over it for playback? Or how does it split a part into harmonics/notes in a polyphonic texture?



The rest of this doc focuses on how to build your own RipX from existing tools.

### Demixing

[Demucs v4 (2022)](https://github.com/facebookresearch/demucs) [▶️](https://www.google.com/search?q=demucs+online) splits into bass, drums, vocals and other. Previously [spleeter (2020)](https://github.com/deezer/spleeter) was widely used - it can do additional fifth stem with piano.




### Beat tracking

Next, you want to get beats and downbeats (measures) - in millisecond timestamps. And verse/chorus/bridge form annotation, ideally. Well, since July 2023 you 
can get [All-in-One (2023)](https://github.com/mir-aidj/all-in-one) [🤗](https://huggingface.co/spaces/taejunkim/all-in-one):

![image](https://github.com/vpavlenko/study-music/assets/1491908/220fc35e-db5c-430c-9735-a0c2da4d8375)

There's also a [nice visualizer](https://github.com/tae-jun/music-dissector):

<img width="1728" alt="Screenshot 2023-09-05 at 11 14 02" src="https://github.com/vpavlenko/study-music/assets/1491908/bb28f70b-313d-4574-afd3-9c64ddefbcfb">

Previous solutions:
- [WaveBeat](https://github.com/csteinmetz1/wavebeat)
- [omnizart beat](https://music-and-culture-technology-lab.github.io/omnizart-doc/) - requires midi, [has](https://github.com/Music-and-Culture-Technology-Lab/omnizart/issues/100) [issues](https://github.com/Music-and-Culture-Technology-Lab/omnizart/issues/104) [running](https://github.com/Music-and-Culture-Technology-Lab/omnizart/pull/103) "beat" now

### Pitch recognition

For each of non-drum parts you want pitch recognition. General-purpose SOTA is [Basic Pitch](https://basicpitch.spotify.com/):

<img width="954" alt="Screenshot 2023-09-05 at 11 17 27" src="https://github.com/vpavlenko/study-music/assets/1491908/5fc44b23-9689-446a-b6e6-aaee7ae7af29">


#### Piano

Historically, a lot of effort was put specifically into solo piano recognition. So now we have:



### Automatic drum tracking






## PDF sheet music to MusicXML (Optical Music Recognition, OMR)




 # Rest

- https://github.com/chrisdonahue/sheetsage
- https://paperswithcode.com/task/music-transcription/latest

Audio to midi
---


- https://piano-scribe.glitch.me/
- https://tuneflow.com/
- [**Lecture on analysis**](../talks/f0/02_analysis.md)
