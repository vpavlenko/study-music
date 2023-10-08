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
- I'd be very glad to mentor students willing to do research in music theory 🧑‍🎓🔬

# What is music theory?

Music theory is our knowledge of what musicians and composers do and do not. Also, it's about what listeners hear.

Music can be roughly split into notes (what keys does a pianist press?) and sound (how producers combine effects to create timbres?). I focus on the notes.

The questions I ask:
- In which order do notes go together in different music?
- Are there statistical patterns that musicians regularly apply?
- Do musicians and composers differ in the tools they use?
- Do listeners actually know and hear that?
- Do sequences of notes, chords, motives and form structures represent genres and styles? How?

I care about [all musical cultures](https://github.com/vpavlenko/study-music): not only the classics and not only Western. For me, music theory is 95% theoretical linguistics and 5% mathematics.

I don't care about black box automatic music generation.

# How to start?

Browse topics below. Pick one or design your own. [Reach out to me](https://t.me/vitalypavlenko) to brainstorm over the possible work plan. Start. Iterate.

# Work principles

- Do corpus-based research: choose from 100 to 100k pieces and analyze them to find patterns
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

For the research and DS/ML, you may use any available ML tools and libraries. For visualizing the results, I personally use Githup Pages + React + TypeScript and I often ask GPT4 for help. I'm happy to help you with this stack (or any other).

Things will be faster if you have some background in music theory. You most likely have one if you've learned to play some instrument before. It's probably enough if you have an idea of what chords are, what's major/minor, what's an octave and a fifth, and if you can potentially play some songs given the chords - maybe on piano, guitar, ukulele or in the DAW. Or at least if you understand how others do that.

The curve to learn other useful concepts like Roman numerals, seventh chords, cadences and modulation can be steep. However, I'm very happy to navigate you through learning it as you proceed with your research.

# Topics

Below I give topics which I care about. I'm happy to work out any other research topics based on your personal interests. It's way better if you scratch your own itch and tackle the questions you can't stand being unanswered anymore. Let's make music structure uncovered, understood and clearly visualized, one question at a time.

## Jazz harmony

Jazz harmony is pretty regular. Chords can be grouped into [blocks](https://github.com/vpavlenko/study-music/blob/main/parts/lego.md) like ii-V-I.

- Can we trace birth and death of certain blocks across history?
- Do composers and subgenres of jazz have certain preferences?
- Can we [visualize](https://openaccess.city.ac.uk/id/eprint/28140/1/Visualization_of_Harmonic_Structure%20Camera%20Ready%20Copy.pdf) harmony of all jazz standards at a single page? Instantly playable and navigable?

## Jazz solos

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

A pianist improvises by controlling velocities and onsets of all notes written out by composer, without changing the order of the notes. The actual rendition is a product of:
- muscle abilities and limitations
- composer's marks on a music sheet
- cultural inertia of how should a certain piece sound
- composer's consistent taste across the pieces
- composer's approach to this individual piece

Can we decompose a certain piano rendition onto these axes?

Can we visualize the real expressiveness of a certain recording right on the score?

What are the patterns of expression for certain pieces/composers/styles in terms of volumes/onsets? How can we simplify and visualize it?

## Pan-Western

 - harmonic evolution across everynoise (v vs V, minor vs major, harmonic rhythm, progressions)
     - can we easily explain how certain genres are different from the others? is this due to instrumentation / production (plugins) or harmony?
       can we extend the everynoise map to include this information?
     - in which genres do certain countries actually have their national fingerprint / style?

## Rock harmony

## Video game music

## Film music

    - movie music
        - can we reliably identify NRT transitions in the soundtrack?
        - is there evolution of usage of them over time?
        - do all composers use them in the same way?
        - do they have stable semantic load? (can we separate "positive"/"negative", sorts of magic?)


## Barbershop quartets

## Balkan music

## Arabic music

## Adhans

## Persian music

## Gamelan

