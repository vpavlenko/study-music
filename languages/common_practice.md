# How do we visualize the language of common practice?

I.e. the era of the tonal system from 1650 to 1900. 

## Chords

At the level of individual bars and beats, we can assign [an annotation of Roman numerals](https://sites.google.com/view/musicalharmonysite/part-ii-harmony-theory-and-analysis/complete-harmony-analyses/chopins-prelude-no-9-in-e-major):

<img width="1191" alt="Screenshot 2023-02-02 at 10 13 01" src="https://user-images.githubusercontent.com/1491908/216246068-6b58bfee-47bb-4b0e-b223-8e4084af26b7.png">

The Roman numerals are below, the guitar-like chord symbols are above. We use Roman numerals to make the same analysis for any minor or major mode, regardless of its tonic pitch.

In which sense are Roman numerals "real", do we hear them? Are they the actual structure of the piece or are they some esoteric concepts helping us to make sense of a complete noise and chaos?

On a picture above, every red-circled note doesn't belong to any of the chord pitches. That is, all other notes belong to a local chord. That is, out of all 12 pitch classes, for every beat or several beats a composer selects exactly 3 or 4 and tries to locally shape all melodic and textural lines using that pre-selected pitch classes. This helps a composer to tell a story both in motives/texture (using rhythm, melodic direction, rests etc.) and simultaneous story about the progression of chords.

As chords build in thirds, we can reorder seven pitch classes as 1-3-5-7-2-4-6 and have [a better visualization of a chord line](https://sites.google.com/view/musicalharmonysite/part-i-general-music-theory/chords/visualization-of-chords):

![image](https://user-images.githubusercontent.com/1491908/216261732-a36bcd83-70d6-462b-93b0-85a5b1f80799.png)


All red-circled notes are not random. They are all classified, and we can [annotated them in different colours](https://kaitlinbove.com/nonharmonic-tones):

![image](https://user-images.githubusercontent.com/1491908/216248115-cea16e59-9f29-46a5-9cb6-af617aabeac1.png)

Alternatively, for every given chord [we can assign](https://musescore.com/user/39031562/scores/9034154) twelve colors to all pitch classes relative to it (eg. in a rainbow order). We hope to see more of [0, 4, 7] colors for major chords (red, bright green, blue) and [0, 3, 7] colors (red, yellow, blue) for minor chords:

<img width="789" alt="Screenshot 2023-02-02 at 10 37 15" src="https://user-images.githubusercontent.com/1491908/216250123-3cbf4d84-8237-4951-a621-d20684415067.png">

Chords in turn [can be colored](https://www.hooktheory.com/theorytab/view/ludwig-van-beethoven/piano-sonata-no-14-moonlight-1st-movement) in a rainbow order. Also, the score can be represented as a piano roll rather than a music sheet:

<img width="1216" alt="Screenshot 2023-02-02 at 10 42 54" src="https://user-images.githubusercontent.com/1491908/216251163-8cf6e7e4-ba38-4826-845e-c689911434a2.png">

## Chord transition probabilities

At the lowest level, we can then ask, which chords are followed by which ones? Are there any patterns?

To do that, we first need [to annotate a corpus of scores](https://transactions.ismir.net/articles/10.5334/tismir.63/) - say, all piano sonatas by Mozart. Then we can build a chord transition matrix:

<img width="1671" alt="Screenshot 2023-02-02 at 10 52 03" src="https://user-images.githubusercontent.com/1491908/216252762-e22c47ea-a732-48ff-ac91-1d8c28f653b3.png">

We can [compare these matrices](https://digitalresearch.bsu.edu/mathexchange/wp-content/uploads/2021/02/Markov-Chains-of-Chord-Progressions_kiefer.peter_.pdf) between different composers to find differences in their languages:

<img width="909" alt="Screenshot 2023-02-02 at 12 02 46" src="https://user-images.githubusercontent.com/1491908/216266000-6ad90af1-28bd-4d54-9a38-c23f6c8c521f.png">

The same idea can be expressed in a graph. Though, theoretical, there may be several origins of that graph. Ideally, you'd get a graph from a statistical computations on an annotated corpus. If no encompassing corpus is available yet, you can build [a graph](https://www.miltonline.com/2018/10/24/tonal-harmony-flowcharts-major-minor/) from your memories as a classically trained musician or by summarizing several theory books:

![image](https://user-images.githubusercontent.com/1491908/216262585-c7cc8082-3eb6-4f79-8bf2-09c1e557aa10.png)

We can [group several edges](http://dmitri.mycpanel.princeton.edu/tonaltheories.pdf) by an interval between the roots of its chords:

<img width="491" alt="Screenshot 2023-02-02 at 11 48 53" src="https://user-images.githubusercontent.com/1491908/216263220-d1843eae-4331-47f6-914a-372346e69e7b.png">

Then, we can go beyond two-chord pairs and speak of [popular progressions of several chords](http://dmitri.mycpanel.princeton.edu/tonaltheories.pdf):

<img width="606" alt="Screenshot 2023-02-02 at 11 51 37" src="https://user-images.githubusercontent.com/1491908/216263723-e8427e84-c547-4ef1-ba12-dcbb437795d9.png">


## Form

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

We can also want to write a program that computationally does some parsing, and so we may [design a formal theory of tonal syntax](https://tu-dresden.de/gsw/phil/ikm/muwi/ressourcen/dateien/lehrveranstaltungen/ws_2015-16-ss2020/ws_2015_2016/s_musik_mathematik_kognition/gsm-rohrmeier-2011.pdf). Though it may lack some creative reading of an intentional composer's ambiguity by a theorist.

<img width="1039" alt="Screenshot 2023-02-02 at 11 56 37" src="https://user-images.githubusercontent.com/1491908/216264771-156b01a3-8ed3-45bd-9d96-37dad6fe98e7.png">

If we are dissatisfied with an ambiguity and fuzziness when defining high level structures, [we may get to a level of cadences](https://transactions.ismir.net/articles/10.5334/tismir.63/). At least they do exist for sure, and we can study their statistical probabilities:

<img width="1416" alt="Screenshot 2023-02-02 at 12 16 33" src="https://user-images.githubusercontent.com/1491908/216268873-f1590c73-cb6f-4339-b0bc-9350d2a6b50c.png">


## Modulation

A common practice piece usually progress through a set of keys. For every piece of that period we have a music sheet. It gives us some information: through key signature we can understand the mid-level division into keys. 

Local modulations aren't usually notated - we may see more sharps and flats inside the score, but not as a key signature change. We can apply a rough statistical technique to get some (not very accurate) [approximation of local tonalities](https://ccrma.stanford.edu/~craig/keyscape/) throughout the piece:

<img width="899" alt="Screenshot 2023-02-02 at 10 07 34" src="https://user-images.githubusercontent.com/1491908/216245190-89170eb6-408e-4e5a-839a-4b85f77cdfee.png">

Also, at the very local level there's [a "tonicization vs. modulation" dichotomy](https://transactions.ismir.net/articles/10.5334/tismir.63/):

![image](https://user-images.githubusercontent.com/1491908/216252124-e25212bc-9461-4a16-93ad-c2b9a60332dd.png)

