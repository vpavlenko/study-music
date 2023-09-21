# NES

Pick any [NES tune](https://chiptune.app/browse/Nintendo):
- Is it in major/minor Western language?
- Does it conform to chords/melody duality?
   - Are there arpeggiated chords, bass?
   - Is the pattern the same for all chords?
- What's the structure of the melody?
- Does it have form? (AABA, verse-chorus, sentence, melody/solo?)
- Anything special in chords?

# Порядок разбора
- проставить аккорды - с помощью добровольца
   - [игра](https://www.youtube.com/watch?v=W1nPX5zn0lY), 1986, [composer](https://en.wikipedia.org/wiki/Naoki_Kodaka)
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Atlantis%20no%20Nazo
- simple
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/75%20Bingo?subtune=2
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/75%20Bingo?subtune=6
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Ankoku%20Shinwa%20-%20Yamato%20Takeru%20Densetsu?subtune=4
- https://vpavlenko.github.io/chiptheory/browse/Nintendo/2in1%20Cosmo%20Cop?subtune=1 - обсудить слои фактуры
- modulations:
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Addams%20Family?subtune=5
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Adventures%20of%20Dino-Riki?subtune=4
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/'89%20Dennou%20Kyuusei%20Uranai?subtune=3
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Alien%203?subtune=1
- pentatonic
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/AV%20Hanafuda%20Club?subtune=1
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Airwolf?subtune=1 (also modulation)
- spooky
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Adventures%20of%20Dino-Riki?subtune=3
- constant structures
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Aigiina%20no%20Yogen%20-%20From%20the%20Legend%20of%20Balubalouk?subtune=1
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Aspic%20-%20Mahebiou%20no%20Noroi?subtune=1
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/'89%20Dennou%20Kyuusei%20Uranai?subtune=9
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Akagawa%20Jirou%20no%20Yuurei%20Ressha?subtune=1
- atonal
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Adventures%20of%20Rad%20Gravity,%20The
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/A%20Ressha%20de%20Ikou?subtune=3
- blues
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/AV%20Hanafuda%20Club?subtune=2
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Al%20Unser%20Jr.%20Turbo%20Racing?subtune=29
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/AV%20Poker?subtune=5
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/'89%20Dennou%20Kyuusei%20Uranai?subtune=14
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/Apple%20Town%20Monogatari%20-%20Little%20Computer%20People?subtune=3
- цитаты
   - https://vpavlenko.github.io/chiptheory/browse/Nintendo/America%20Daitouryou%20Senkyo, [Musipedia search](https://www.musipedia.org/result.html?sourceid=melody-url&tx_mpsearch_pi1%5bsubmit_button%5d=Search&tx_mpsearch_pi1%5bpc%5d=lilyc%27%278+b%278+c%27%278+g%274.+e%274.+d%278+cis%278+d%278+a%274.+&filtertext=&coll=m&onlymatchfrom=0.3)



# Структура западной гармонии

Лад делит глобально 12 нот на 7 наших и 5 чужих. аккорд локально в ближайшие две секунды дальше делит эти 7 на 3 наших и 4 временно чужих

# Sound chip

[Spec](https://www.nesdev.org/2A03%20technical%20reference.txt)

A direct conversion to midi may lose too much information, including timbral. Eg. each square wave generator has duty cycle control.

- [Harmonics of rectangular waves](https://pages.uoregon.edu/emi/14.php)
- [Explanation on duty cycles harmonics cancelling](https://wigglewave.wordpress.com/2014/08/16/pulse-waveforms-and-harmonics/)
- [Oscilloscope](https://www.youtube.com/watch?v=OfrEoEQpPrI&list=PLeQUY34t8UPlJqQ1iJcw2h_gEIUtBqAr0)
   - [Silver Surfer](https://www.youtube.com/watch?v=Mi7l8ZIrG8s) - lots of vibrato and glides
   - [FDS Zelga](https://www.youtube.com/watch?v=-CPrdomMoA4)
   - [Perfect triangle wave](https://www.youtube.com/watch?v=8RrQrATnXXY)
  

# Trackers

- https://famistudio.org/

# Notes on games

- https://chiptune.app/browse/Nintendo/Battle%20Storm - doesn't use square 2 - two voices only
- https://chiptune.app/browse/Nintendo/Crystalis - 25% duty. Overall a great soundtrack
- https://chiptune.app/browse/Nintendo/Crime%20Busters - tune 2 has 25% and 12.5% simultaneously, also a lot of gliding. Also a clear minor/major language with boogie vibe
- https://chiptune.app/browse/Nintendo/Kero%20Kero%20Keroppi%20no%20Daibouken - tune 1, square 1 changes from 12.% to 50%
- https://chiptune.app/browse/Nintendo/Little%20Magic - purely 50% on three voices, has vibrato
- https://chiptune.app/browse/Nintendo/1991%20Du%20Ma%20Racing - huge detune
