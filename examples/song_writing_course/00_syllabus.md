# Song Writing: From Idea to Finished Song

## Overview

This course teaches songwriting through the lens of computational thinking. Each chapter pairs a core songwriting concept with Python code that makes the concept concrete and inspectable. You will build chords from frequency ratios, generate melodies from scale patterns, analyze lyric structures with string processing, and visualize arrangements as timelines. By the end, you will have both the musical vocabulary and a toolkit of small programs to support your songwriting practice.

The course is designed for people who are curious about both music and programming. You do not need to play an instrument or read sheet music, but some basic familiarity with musical terms (notes, chords, beats) will help. On the programming side, comfort with Python variables, loops, lists, and functions is assumed.

## Prerequisites

- **Music**: Familiarity with basic concepts (notes, chords, rhythm, verse/chorus). No instrument proficiency required.
- **Python**: Variables, lists, loops, functions, f-strings. Experience with numpy and matplotlib is helpful but not required.

## Chapters

| # | Notebook | Title | Summary | Depends on |
|---|----------|-------|---------|------------|
| 1 | `ch01_building_blocks.ipynb` | The Building Blocks of a Song | Song structure (verse, chorus, bridge), common forms (AABA, verse-chorus), section analysis | -- |
| 2 | `ch02_melody.ipynb` | Melody: The Hook That Sticks | Intervals, scales, melodic contour, stepwise vs. leapwise motion, sine-wave playback | Ch 1 |
| 3 | `ch03_harmony.ipynb` | Harmony and Chord Progressions | Building chords from intervals, diatonic harmony, common progressions, frequency ratios | Ch 2 |
| 4 | `ch04_rhythm.ipynb` | Rhythm and Groove | Time signatures, rhythmic patterns, syncopation, matching rhythm to lyrics | Ch 1 |
| 5 | `ch05_lyrics.ipynb` | Lyrics: Writing Words That Sing | Rhyme schemes, syllable counting, phonetic rhyme finding, lyric prosody | Ch 4 |
| 6 | `ch06_arrangement.ipynb` | Arrangement and Production Thinking | Layering instruments, dynamics, intros/outros, transitions | Ch 1-5 |
| 7 | `ch07_capstone.ipynb` | Capstone: Writing a Complete Song | End-to-end song creation combining all previous concepts | Ch 1-6 |

## Suggested Reading Order

The chapters are numbered in the recommended order. Chapters 2-3 (melody and harmony) and Chapter 4 (rhythm) can be studied in either order after Chapter 1, but both paths should be completed before Chapter 5 (lyrics). Chapter 6 (arrangement) draws on all preceding material. Chapter 7 (capstone) is the culmination.

```
Ch 1 (Structure)
 |        \
Ch 2       Ch 4
(Melody)   (Rhythm)
 |            |
Ch 3       Ch 5
(Harmony)  (Lyrics)
  \         /
   Ch 6
   (Arrangement)
      |
   Ch 7
   (Capstone)
```

## Tools Used

- **Python 3.10+**
- **numpy** -- array operations, frequency calculations, signal generation
- **matplotlib** -- all visualizations
- **Standard library** -- string processing, itertools, collections

No external music libraries are required. Everything is built from first principles.
