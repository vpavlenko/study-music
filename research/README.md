# Who am I?

- I'm [Vitaly Pavlenko](https://www.linkedin.com/in/vitaly-pavlenko-9729bb76/)
   - an independent researcher of music theory
   - with a background in creating mobile and web products
   - also with a lot of teaching experience
- In the past:
   - I got a BSc in Applied Math and CS at MIPT (Moscow)
   - After that, I've studied at Skoltech, ШАД and [МКИМ](https://mcim.ru/)
   - I've created [pythontutor.ru](https://pythontutor.ru/), which is a popular Python course that's used by thousands of people every day
   - I've taught:
     - [Digital Technologies at a high school](https://sites.google.com/site/vpavlenkoinf/)
     - [web development at MIPT](https://github.com/vpavlenko/web-programming)
     - [Java](https://www.youtube.com/playlist?list=PLzQrZe3EemP7hx6NKGA26yr3HJ-RF4iwT)
     - intro to programming, algorithms and data structures - at MIPT, ЛКШ, three high schools and other places
   - I've mentored teams doing tech and startup projects, at two Russian universities
   - I've also worked at WhatsApp, [ASAP](https://asaptaste.com/getasap) and [Jetway](https://www.linkedin.com/pulse/how-i-launched-subsequently-messed-up-marketplace-igor-grigoriev/)
- Now:
   - I live in Tbilisi, Georgia 🇬🇪
   - I'm not employed and I'm not pursuing a degree
   - I'm working on [a corpus of analyses for NES soundtracks](https://github.com/vpavlenko/chiptheory)
   - I give [lectures](https://t.me/keetezh/945) on music theory in Tbilisi
- I'd be very glad to mentor students willing to do research in music theory 👩‍🔬🔬🧑‍🎓

# What is music theory?

Music theory is our knowledge of what musicians and composers do and do not. Also, it's about what listeners hear.

Music can be roughly split into notes (what keys does a pianist press?) and sound (how producers combine effects to create timbres?). I focus on the notes.

The questions I ask:
- In which order do notes go together in different music?
- Are there statistical patterns that musicians regularly apply?
- Do different composers use different toolboxes? Where does it come from?
- Do listeners actually know and hear that?
- Do sequences of notes, chords, motives and form structures represent genres and styles? How?

I care about [all musical cultures](https://github.com/vpavlenko/study-music): not only the classics and not only Western. For me, music theory is 95% theoretical linguistics and 5% mathematics.

I don't care about black box automatic music generation.

# How to start?

Browse topics below. Pick one or design your own. [Reach out to me](https://t.me/vitalypavlenko) to brainstorm over the possible work plan. Start. Iterate.

# Work principles

- Do corpus-based research: choose from 10 to 100k pieces and analyze them to find patterns
- Present the discoveries through web demos rich in audio examples and visual explanations
- Anti-perfectionism: release and demo as soon as there's something to play with
- Work in extremely small iterations. one week is great, one day is even better
- Limit the scope of the very first steps, make a humble MVP on the week one and iterate from there
- Help others with forking and reproducibility: publish the research code in open source repositories with clear setup instructions
- Consider making something publishable in real music theory journals like Music Theory Online
- However, optimize for teaching your friends on what you've discovered
- Listen to the type of music you're researching, even if it's outside of your comfort zone
- However, optimize for working on music that you deeply care about
- Read books and papers to get an idea of how other researchers understand its structure
- Switch back and forth between manual transcription/annotation and large-scale DS/ML processing
- [Write down](https://emusicology.org/index.php/EMR/article/view/8103/6032#:~:text=with%20questions) [questions](https://kb.osu.edu/bitstream/handle/1811/93138/1/FDMC_2021_Huron_005.pdf) before the research

Feel free to adjust them to your taste. I'm happy to navigate you towards reaching this style of research.

For the research and DS/ML, you may use any available tools and libraries. For visualizing the results, I personally use Githup Pages + React + TypeScript and I often ask GPT4 for help. I'm happy to help you with this stack (or any other).

Things will be faster if you have some background in music theory. You most likely have one if you've learned to play some instrument before. It's probably enough if you have an idea of what chords are, what's major/minor, what's an octave and a fifth, and if you can potentially play some songs given the chords - maybe on piano, guitar, ukulele or in the DAW. Or at least if you understand how others do that.

The curve to learn other useful concepts like Roman numerals, seventh chords, cadences and modulation can be steep. However, I'm very happy to navigate you through learning it as you proceed with your research.

# Topics

Below I give topics which I care about. I'm happy to work out any other research topics based on your personal interests. It's way better if you scratch your own itch and tackle the questions you can't stand being unanswered anymore. Let's make music structure uncovered, understood and clearly visualized, one question at a time.

## Jazz harmony

One of the key aspect of [functional](https://www.youtube.com/watch?v=BNTicwsLDek) [jazz](https://www.youtube.com/watch?v=4B5Lg0qExmY) [music](https://www.youtube.com/watch?v=icl1tpMUJzo) is harmony - the chain of chords that is played over and over again in choruses. 

Jazz harmony is pretty regular. Chords can be grouped into [blocks](https://github.com/vpavlenko/study-music/blob/main/parts/lego.md) like ii-V-I or chain of dominants.

Jazz music is constantly being developed: new composers compose new tunes. Every tune is usually represented as a lead sheet: chords + melody. Chords on a lead sheet help musicians to render a tune. However, they somewhat obscure the original composer's idea, and there may be better way to represent [the harmonic structure](https://openaccess.city.ac.uk/id/eprint/28140/1/Visualization_of_Harmonic_Structure%20Camera%20Ready%20Copy.pdf).

- Can we trace birth and death of certain lego blocks across history?
- Do composers and subgenres of jazz have certain preferences of lego blocks?
- Can we visualize harmony of all jazz standards at a single page to uncover patterns?

## Jazz solos

Another key aspect of jazz is solo: a [chain](https://youtu.be/lu5AV2hXDJc?si=spGwtVM47oTEGE-g&t=31) [of](https://www.youtube.com/watch?v=nYr_avtNntE) [phrases](https://www.youtube.com/watch?v=aRPKgl0rOzA) that a single musician plays over a chain of chords. Every jazz musician grows his solo vocabulary for the entire life by combining common patterns with personal discoveries and taste. [Some researchers](https://github.com/vpavlenko/study-music/blob/main/parts/jazz_solo.md#research) like Norgaard or Frieler tried to describe patterns in this activity. However, the clear picture is still absent.

- Can [Frieler's models](https://github.com/vpavlenko/study-music/blob/main/parts/jazz_solo_visualizations.md) (or any models from [Impro-visor](https://github.com/Impro-Visor/Impro-Visor/tree/master/grammars)) improve jazz solo transcription?
- Can Frieler's models help us build a real-time imrpovisation instrument that's fun to use? (Touch screen instruments? [Music Mouse](https://teropa.info/musicmouse/)-like?)


## Bass lines

Bass lines are everywhere in Western music. They can easily be separated from the track using demucs and further transcribed using basic-pitch.

A theory for bass lines should be more regular, because, in most cases, a bass line is inferred from a current chord, and in some cases it has a clear structure (riff or shape).

The questions for bass lines:
- Can we demonstrate that bass lines [become complex](https://www.youtube.com/watch?v=LMtf7PtqIlw) as a single musician matures? How to measure complexity/creativeness of a musician from album #1 to album #10?
- Can we make automatic [comparative analysis](https://digscholarship.unco.edu/dissertations/329/) of different bassists playing the same pieces?
- Are bass lines different for the same genre across different [countries](https://everynoise.com/countries.html)? Eg. do Italian metal bassists do the same things which French metal bassists don't do? Is "region" a thing in enthropy (perplexity) growth as we zoom out from a single musician to a whole genre?
- What's the easiest visual way to represent bass line patterns? Can we show piano roll bass patterns over [everynoise](https://everynoise.com/)?

## Expression in classical piano

A pianist [improvises](https://tuttitempi.com/#scoreId=U00000577908&youtube=1&spotify=0&muziekweb=0) by [controlling](https://touchpianist.com/) velocities and onsets of all notes written out by composer, without changing the order of the notes. The actual rendition is a product of:
- muscle abilities and limitations
- composer's marks on a music sheet
- cultural inertia of how should a certain piece sound
- composer's consistent taste across the pieces
- composer's approach to this individual piece

Can we decompose a certain piano rendition onto these axes?

Can we visualize the real expressiveness of a certain recording right on the score?

What are the patterns of expression for certain pieces/composers/styles in terms of volumes/onsets? How can we simplify and visualize it?

## Rock harmony

On the one hand, rock harmony is theorized in [several](http://davidtemperley.com/the-musical-language-of-rock/) [modern](https://press.umich.edu/Books/H/Hearing-Harmony2) [books](https://www.amazon.com/Japanese-Music-Harmony-Fundamental-Fluctuation-ebook/dp/B08513234C) by manual annotation and categorization of chord progressions.

On the other hand, we have a lot of datasets of chords for the long tail of rock music: both [uploaded by people](https://amdm.ru/) and [done automatically](https://chordify.net/).

- Can we use these datasets to generalize our model to other countries / rock bands?
- Can we show that a harmonic complexity grows as the band gets older?
- Can we show trends in using certain chord progressions over times and countries?
- Can we draw state machines for chords for certain bands to compare harmonic languages?

## Video game music

- https://jech2.github.io/YM2413-MDB/
- https://chrisdonahue.com/LakhNES/
- https://www.dropbox.com/scl/fi/5mgwcu9jevbyrndcsmn9e/Chiptune_music_An_exploration_Christopher_Hopkins.pdf?rlkey=n116axcnl27qq42ogzye64hru&dl=0

## Film music

Film music has one certain [feature](https://alpof.wordpress.com/2021/10/09/neo-riemannian-examples-in-music/) that's rarely used in other Western music: non-functional two-chord changes that are usually described as neo-Riemannian or as chromatic mediants.

- Given an entire film's soundtrack, can we reliably identify these two-chord patterns in the soundtrack?
- If "yes", can we batch-process a lot of film music to answer the following:
   - is there evolution of usage of them over time?
   - do all composers use them in the same way?
   - do they have stable semantic load? (can we separate "positive"/"negative", sorts of magic?)


## Barbershop quartets

[Barbershop](https://www.youtube.com/watch?v=7CBlPJE7Sew) [is](https://www.youtube.com/watch?v=jUffPtS3-7A) [a](https://www.youtube.com/shorts/yyHdDsP9iDU) [culture](https://www.youtube.com/watch?v=_W1CvQG01Q4) that nearly died at the start of the 20th century and then was semi-artificially preserved. Much like the spoken Hebrew language. It has The Book: ["Barbershop Arranging Manual" (1980)](https://www.dropbox.com/scl/fi/6tckdjyu4xe503ucu7bmh/barbershop_arranging_manual.pdf?rlkey=c2cvbhujywkihd0zc22xc3uwj&dl=0). Moreover, this is the culture driven by competition with clear rules of [contest judging](https://www.barbershop.org/files/documents/contestandjudging/C&J%20Handbook.pdf).

- Can we build a transcription pipeline that yields four barbershop voices?
   - Can we fine-tuning existing splitters/transcribers?
   - Can we improve its accuracy by exploiting the knowledge of these rules?
- How does The Manual and The Judging Handbook influence modern arrangers?
- Is the "lock and ring" really visible on the spectrogram? Can we measure the amount of it?
- Do arrangers have their fingerprints by which we can identify them?
- Can we measure the interestingness of the arrangement?


## Arabic music

Traditional Arabic music is a heterophonic, with a single melody elaborated by several instruments. In 20th century a lot of composers created original pieces, including [long](https://www.youtube.com/watch?v=jlPx-R7XmaA) [songs](https://www.youtube.com/watch?v=e7wl1tm35bM). Instead of using just two scales, as Western music, an Arabic music uses many scales, or rather jins (4 or 5 pitch collections) and modulates between them, creating a [narrative](https://maqamlessons.com/analysis/rast.html) through these modulations, much like Western music creates one with chords.

- Can we make an automatic transcription of a piece, exploiting this knowledge of its structure?
- How can we visualize the modulations in the most efficient way? What's the best piano roll for Arabic music?
- Are [networks of maqams](https://maqamlessons.com/playground/010_01_MaqamRast.html) not cliques? Are certain edges really absent? Why?

Also, tuning of quartertones is not fixed. Can we say anything about it?

## Adhans

[Adhan](https://youtu.be/ke4vcLCGgRY?si=3jykA74r6HIRQQEX&t=72) [is](https://www.youtube.com/playlist?list=PLMXv6l1xIo3LSoeDbL-y_bNo9--Kd_pTF) [the](https://www.youtube.com/watch?v=Ue1KjsAmoa0) Islamic call to prayer recited from the mosque five times daily. It's either recorded of performed live by a trained muezzin. It's in a maqam tradition and can be described an a vocal improvisation in a certain scale. In Turkey every time of a day is recited [in a different makam](https://www.youtube.com/watch?v=ueq8tROmyLE).

What are the precise rules of this improvisation? What's allowed and what's not?

## Persian music

[Persian](https://www.youtube.com/watch?v=e3oKIn6Vw5k) [traditional](https://www.youtube.com/watch?v=Bq-RX04vG24) radif improvisation is usually described as follows: a musician trained by a certain master glues motives from a radif together. 

Given an audio performance, can we highlight the certain radif chunks in it?

## Gamelan

[Gamelan](https://www.youtube.com/watch?v=B4Z_2a7_cgY) [music](https://www.youtube.com/watch?v=ccHTOepjK_s) [is](https://www.youtube.com/watch?v=iqKV59P4ZgI) performed on an orchestra of xylophones and gongs. This culture is mostly about preservation of cultural heritage across centuries, and not about the creativeness of individual performers. The rich soundscape is created by many instruments rendering a rather simple melody by rigid rules. 

As the rules are known, and multitracks are unavailable, can we build an unsupervised splitter of a mix into different tracks? Once this problem is solved, can we make automatic models for elaborating instruments like gender barung (in the style of Impro-Visor)?
