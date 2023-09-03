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
