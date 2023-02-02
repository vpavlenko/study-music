# How do we visualize the language of common practice?

I.e. the era of the tonal system from 1650 to 1900. 

## Individual piece

### Harmony

At the level of individual bars and beats, we can assign [an annotation of Roman numerals](https://sites.google.com/view/musicalharmonysite/part-ii-harmony-theory-and-analysis/complete-harmony-analyses/chopins-prelude-no-9-in-e-major):

<img width="1191" alt="Screenshot 2023-02-02 at 10 13 01" src="https://user-images.githubusercontent.com/1491908/216246068-6b58bfee-47bb-4b0e-b223-8e4084af26b7.png">

The Roman numerals are below, the guitar-like chord symbols are above. We use Roman numerals to make the same analysis for any minor or major mode, regardless of its tonic pitch.

In which sense are Roman numerals "real", do we hear them? Are they the actual structure of the piece or are they some esoteric concepts helping us to make sense of a complete noise and chaos?

On a picture above, every red-circled note doesn't belong to any of the chord pitches. That is, all other notes belong to a local chord. That is, out of all 12 pitch classes, for every beat or several beats a composer selects exactly 3 or 4 and tries to locally shape all melodic and textural lines using that pre-selected pitch classes. This helps a composer to tell a story both in motives/texture (using rhythm, melodic direction, rests etc.) and simultaneous story about the progression of chords.

All red-circled notes are not random. They are all classified, and we can [annotated them in different colours](https://kaitlinbove.com/nonharmonic-tones):

![image](https://user-images.githubusercontent.com/1491908/216248115-cea16e59-9f29-46a5-9cb6-af617aabeac1.png)

Alternatively, for every given chord [we can assign](https://musescore.com/user/39031562/scores/9034154) twelve colors to all pitch classes relative to it (eg. in a rainbow order). We hope to see more of [0, 4, 7] colors for major chords (red, bright green, blue) and [0, 3, 7] colors (red, yellow, blue) for minor chords:

<img width="789" alt="Screenshot 2023-02-02 at 10 37 15" src="https://user-images.githubusercontent.com/1491908/216250123-3cbf4d84-8237-4951-a621-d20684415067.png">

Chords in turn [can be colored](https://www.hooktheory.com/theorytab/view/ludwig-van-beethoven/piano-sonata-no-14-moonlight-1st-movement) in a rainbow order. Also, the score can be represented as a piano roll rather than a music sheet:

<img width="1216" alt="Screenshot 2023-02-02 at 10 42 54" src="https://user-images.githubusercontent.com/1491908/216251163-8cf6e7e4-ba38-4826-845e-c689911434a2.png">

#### Chord transition probabilities

At the lowest level, we can then ask, which chords are followed by which ones? Are there any patterns?

To do that, we first need [to annotate a corpus of scores](https://transactions.ismir.net/articles/10.5334/tismir.63/) - say, all piano sonatas by Mozart. Then we can build a chord transition matrix:

<img width="1671" alt="Screenshot 2023-02-02 at 10 52 03" src="https://user-images.githubusercontent.com/1491908/216252762-e22c47ea-a732-48ff-ac91-1d8c28f653b3.png">


### Form

A complete piece has a hierarchical structure with several levels, with each level using the structures one level below: 
- level 1 (usually 4 bars long): _antecedent, consequent, presentation, continuation, extended cadential phrase_
- level 2 (usually 8 bars long): _period, sentence, hybrid theme_
- level 3: _small ternary form, small binary form, subordinate theme, retransition, coda_
- level 4: _exposition, development, capitulation, menuet_
- level 5, highest level of a movement: _rondo, sonata-allegro, menuet and trio, theme with variations, concerto_

This [can be drawn](https://books.google.ge/books/about/Musical_Form_Forms_Formenlehre.html) separate from the score as a tree:

<img width="1437" alt="formenlehre" src="https://user-images.githubusercontent.com/1491908/216260232-4044d6c9-1822-4223-9de4-65ec84256070.png">

I'm using a language of Caplin who published [an outstanding study book](http://www.music.mcgill.ca/acf/), where he draws the some levels of that structure over countless examples from Haydn, Mozart and Beethoven. (The fewer composers you take into your theory, the better your theory works to describe them.)

<img width="1088" alt="99" src="https://user-images.githubusercontent.com/1491908/216260615-20ecbc5c-b58b-4de3-aad3-ad9685f384a4.png">

There are other theories for the same material, three of them [debate in a single book](https://books.google.ge/books/about/Musical_Form_Forms_Formenlehre.html)

We can also [overlay that structure above a music score](https://transactions.ismir.net/articles/10.5334/tismir.27/):

<img width="634" alt="Screenshot 2023-02-02 at 10 59 28" src="https://user-images.githubusercontent.com/1491908/216254093-d8da9061-5bbf-496c-8912-1ae85a2c4964.png">

We can [compare relative lengths](https://transactions.ismir.net/articles/10.5334/tismir.27/) of those structures across a set of pieces:

<img width="1167" alt="Screenshot 2023-02-02 at 11 03 29" src="https://user-images.githubusercontent.com/1491908/216254799-48ae3212-68d7-4a91-9508-5632f7db3389.png">




The borders of sentences and periods are defined by means of cadences. 


### Modulations

For every piece of that period we have a music sheet. It gives us some information: through key signature we can understand the mid-level division into keys. 

Local modulations aren't usually notated. We can apply a rough statistical technique to get some (not very accurate) [approximation of local tonalities](https://ccrma.stanford.edu/~craig/keyscape/) throughout the piece:

<img width="899" alt="Screenshot 2023-02-02 at 10 07 34" src="https://user-images.githubusercontent.com/1491908/216245190-89170eb6-408e-4e5a-839a-4b85f77cdfee.png">




Also, at the very local level there's [a "tonicization vs. modulation" dichotomy](https://transactions.ismir.net/articles/10.5334/tismir.63/):

![image](https://user-images.githubusercontent.com/1491908/216252124-e25212bc-9461-4a16-93ad-c2b9a60332dd.png)


## Language of a composer / style / epoch




### Major vs minor mode
