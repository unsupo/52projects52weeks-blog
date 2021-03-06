---
ID: 62
post_title: >
  Non Musical Engineer Attempts to Make
  Original Song
author: jarndt
post_excerpt: ""
layout: post
permalink: >
  https://52projects52weeks.com/2019/01/13/non-musical-engineer-attempts-to-make-original-song/
published: true
post_date: 2019-01-13 23:05:17
---
<!-- wp:heading {"level":3} -->

### Introduction

<!-- /wp:heading -->

<!-- wp:paragraph -->

My initially thought of doing this through neural networks using TensorFlow, but i figured a lot of people had done that and most people weren’t doing it using simple logic.  The idea is to use general patterns to create the song and using randomness to make the song interesting. It won’t be straight up random though, i’ll use lots of other songs to tell my program what “Sounds Good”.  The “Sounds Good” metric will be achieved by looking at a lot of songs and counting the frequency of when notes appear after another note. For instance if an A comes after a C 90 times and a B comes after a C 10 times then there is a 90% chance the program will pick the A after the C, but a much smaller 10% chance for a B.

<!-- /wp:paragraph -->

<!-- wp:heading -->

## The "Sounds Good" Map

<!-- /wp:heading -->

<!-- wp:paragraph -->

To create the “Sounds Good” mapping, I needed lots of midi files to parse and work with.  Thankfully reddit saved me by provided several gigs of [midi files][1]. Then all that was left was to parse those midi files, which two great python library allowed me to do [mido][2] and [python-midi][3]. Next I'd need to loop over the song and create the sounds good mapping.  Midi files contain a separate track for each instrument and each sound that happens at the same time, so we need to loop over each track as well. 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

In the downloaded zip of midi files, there are 119,502 midi files, so even multithreaded, this process will take a long time to complete.  By simply timing how many json files it completes in a minute, which turns out to be 4 every second, i can come to the conclusion that it will take 29,212 seconds or 8 hours and 20 minutes to parse the entire collection.  For this reason i’ve decided not to make the sounds good map out of all the songs available, instead i'll take a random assortment of songs of a hundred songs and make the map from that random collection.

<!-- /wp:paragraph -->

<!-- wp:image {"id":95,"width":135,"height":261} --><figure class="wp-block-image is-resized">

<img src="https://52projects52weeks.com/wp-content/uploads/2019/01/json-mapping-pitch-frequency.png" alt="A completed parsing of a midi file will look like this for each trac" class="wp-image-95" width="135" height="261" /><figcaption>A completed parsing of a midi file will look like this for each track</figcaption></figure> <!-- /wp:image -->

<!-- wp:paragraph -->

Then all the tracks will be summed up.  Using this resulting map i can show that the top 10 most played pitches are, where the first number is the midi pitch and the second is the count of that pitch in all the songs i analyzed:

<!-- /wp:paragraph -->

<!-- wp:html -->

72: 2586  
60: 2596  
65: 2624  
74: 2740  
64: 2779  
62: 2990  
67: 3066  
0: 3120  
69: 3271  
42: 3523  


<!-- /wp:html -->

<!-- wp:paragraph -->

Where 42 pitch can be [translated][4] to F#   


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

And then the top pitches for each pitch:

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

70: 143375  
51: 144476  
69: 183338  
37: 218422  
40: 228779  
54: 291835  
38: 570542  
35: 595757  
36: 663489  
42: 3179845  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

I've decided to limit pitch ranges between 10 and 100 to not get odd pitches that only work for some songs and not most.

<!-- /wp:paragraph -->

<!-- wp:heading -->

## Creating the Song

<!-- /wp:heading -->

<!-- wp:paragraph -->

Since creating the notes is only half the battle for creating a song, I'll use a seed song. A seed song in this context is simply an existing song (midi file) chosen at random to act as the when (when to play a note). I'll then modify the seed song's notes with a weighted random note picked from the map. 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

The first note will be weighted random based off of who has the most linked notes. In other words the note played count. Then all other notes will be a weighted random lookup from the sounds good map. Lastly save the it as a midi file and check the results. 

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

I've decided to try results from weighted random and sounds good mapping to compare to each other as well as generate 10 songs each run in hopes at least one might have something useful in it.

<!-- /wp:paragraph -->

<!-- wp:heading -->

## The Results

<!-- /wp:heading -->

<!-- wp:paragraph -->

It seems the songs generated by the sounds good map more often create a better song than just the random mapping, but not by too much. Both don't generate great songs as a whole. However, they do generate good bits of songs and those bits can be used as inspiration for an artist or simply sections that be stringed along to generate good songs from there.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

All in all, the sounds generated aren't very good, but a few of them show enough potential that this might need to be revisited. Most of the song does sound very random, but the few interesting parts leave me with hope.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

This was my first introduction to music in general. This was my first introduction to midi files as well. I feel like in this week's project, i've accomplished what i've set out to and left enough to be done in the future.

<!-- /wp:paragraph -->

<!-- wp:core-embed/soundcloud {"url":"https://soundcloud.com/jonathan-arndt-574431440/sets/generated-random-songs","type":"rich","providerNameSlug":"soundcloud","className":"wp-embed-aspect-4-3 wp-has-aspect-ratio"} --><figure class="wp-block-embed-soundcloud wp-block-embed is-type-rich is-provider-soundcloud wp-embed-aspect-4-3 wp-has-aspect-ratio">

<div class="wp-block-embed__wrapper">
  https://soundcloud.com/jonathan-arndt-574431440/sets/generated-random-songs
</div></figure> 

<!-- /wp:core-embed/soundcloud -->

<!-- wp:heading -->

## Future Improvements

<!-- /wp:heading -->

<!-- wp:paragraph -->

Use the sounds good map to generate the melody based solely on the “Sounds Good” map, but use the melody as a basis for the rest of the song.  


<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Songs appear to be mostly repeating scales as the melody and a portion of that is the intro and a portion of that is the outro.  Melodies appear to have lots of stepping with some skips and few leaps. So, to generate a song, i’ll randomly pick a scale and it’s length several times to create the melody.  For instance maybe it’ll pick, C,D,E,F then F,E,D, then G,A. This will produce my melody base, then using my mapping generated by the “Sounds Good” parsing of files i made described above, i’ll randomly change a subset of the notes.

<!-- /wp:paragraph -->

<!-- wp:paragraph -->

Hopefully this might create a more structured song.

<!-- /wp:paragraph -->

<!-- wp:heading -->

## Code

<!-- /wp:heading -->

<!-- wp:html -->

<script src="https://gist.github.com/unsupo/e98b01cee320b64590cada91bbb67813.js"></script> <!-- /wp:html -->

<!-- wp:preformatted -->

<pre class="wp-block-preformatted"></pre>

<!-- /wp:preformatted -->

 [1]: https://www.reddit.com/r/WeAreTheMusicMakers/comments/3ajwe4/the_largest_midi_collection_on_the_internet/
 [2]: https://mido.readthedocs.io/en/latest/
 [3]: https://github.com/vishnubob/python-midi
 [4]: http://www.inspiredacoustics.com/en/MIDI_note_numbers_and_center_frequencies