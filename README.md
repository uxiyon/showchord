# pianochords
Drawing a piano keyboard with chord positions.

![cdim7.png](examples/cdim7.png)

## Motivation
As you play keyboard by auto-learning and do not have music theory skills (you can not read scores), you may need to draw chords positions on a keyboard to memorise them. Pianochords is a program to help doing that work and renders chord drawings as SVG and PNG files.
As I was talking to a friend of chord positions, I could not find any program to help me generate theses little piano chords pictures, so I wrote it to compose [this document](examples/triads.pdf).
I hope pianochords could be useful to others. Please let me know if you use it :-)

## Development
Pianochords is developed with python as a language learning exercise.
My goal is first to make pianochords a usable tool in Linux CLI point of view. The idea behind it is to be able to automate piano chord drawings from few information: the notes of the chord.

### Depencies
1. Python modules
    - os
    - sys
    - subprocess
    - argparse
    - collections (namedtuple)

2. External programs
    - [Inkscape](https://inkscape.org/) is needed to transform SVG to PNG with --export option
    - If you are running Linux and do not want to install Inkscape, then consider using [librsvg](https://wiki.gnome.org/Projects/LibRsvg) instead, for exporting (rsvg-export command line tool)

## Features

  * Draw an empty 2 octaves keyboard - eventually with a title
  * Draw any chord you can imaging (on a 2 octave keyboard) by giving notes name. The chord is represented by round marks on the keys
  * Print a title above the keyboard
  * Print note names below the marked keys
  * Export to bitmap (PNG) file (by default, resulting SVG file is written on stdout)
  * Force output filename
  * Provide zoom value to change the (SVG) drawing size
  * Generate many chords at once from informations given in a CSV file (stream mode)


## Examples of use

Basic usage is:
```bash
pianochords --chord "C E G B"
```
That will print an SVG file content on standart output, representing a 2 scales piano keyboard with marks on the keys of the chord notes:
[basic.svg](examples/basic.svg)

To put this output into a file, use system redirection
```bash
pianochords --chord "C E G B" > c_maj7.svg
```
This creates the SVG file [c_maj.svg](examples/c_maj7.svg)

From now you can visualize the chord in a modern browser by pointing to the URL `file:///path-to-my-chord/c_maj7.svg`
If you have `inkscape` installed on your system, you probably have `inkview` tool too. Both allow you to view SVG files.
```bash
inkview c_maj7.svg         # view svg file in an X window
```

If you are running Linux, you may also consider using [librsvg](https://wiki.gnome.org/Projects/LibRsvg) and its `rsvg-view-3` command line tool.
```bash
rsvg-view-3 c_maj7.svg     # view svg file in an X window
```

As most word processor prefer bitmap images to svg files, it is possible to export the result SVG file to PNG raster image with `-e` (`--export`) option
```
pianochords --export -c "C E G B"
```
This example produces automatically SVG (`C-E-G-B.svg`) and PNG (`C-E-G-B.png`) files:

[C-E-G-B.svg](examples/C-E-G-B.svg)

![C-E-G-B.png](examples/C-E-G-B.png)

You may need to name the chord, you can do it with `-n` (`--chordname`) option
```
pianochords -c "C E G B" --chordname "Cmaj7" -f cmaj7 -e
```
This creates both SVG and PNG files:

[cmaj7.svg](examples/cmaj7.svg)

![cmaj7.png](examples/cmaj7.png)

If you need notes name to appear below the keybord, then use the `-p` (`--printkey`) option
```
pianochords -c "C E G B" --chordname "Cmaj7" -f c_maj7 -e
```
This creates both SVG and PNG files:

[c_maj7.svg](examples/c_maj7.svg)

![c_maj7.png](examples/c_maj7.png)

You may want to prepare many chords in text file and draw them in one shot. The `-s` (`--stream`) option allows you to read chords from a file and draw one chord per row.

A row must be of the form `chord;chordname` e.g: `C E G B;Cmaj7`.

Say we have the file `minor-chords-1.txt` containing minor chords at root position:

```
cat examples/stream/minor-chords-1.txt
C Eb G;Cm
C# E G#;C#m
Db E Ab;Dbm
D F A;Dm
D# F# A#;D#m
Eb Gb Bb;Ebm
E G B;Em
F Ab C;Fm
F# A C#;F#m
Gb A Db;Gbm
G Bb D;Gm
G# B D#;G#m
Ab B Eb;Abm
A C E;Am
A# C# F;A#m
Bb Db F;Bbm
B D F#;Bm
```

To generate the drawing of each chords, we use the following command:

```
pianochords -e -p -s < minor-chords-1.txt
```

And we obtain the following files:

SVG files

[examples/stream/minor/Cm.svg](examples/stream/minor/Cm.svg)

[examples/stream/minor/Csharpm.svg](examples/stream/minor/Csharpm.svg)

[examples/stream/minor/Dm.svg](examples/stream/minor/Dm.svg)

[examples/stream/minor/Dsharpm.svg](examples/stream/minor/Dsharpm.svg)

[examples/stream/minor/Em.svg](examples/stream/minor/Em.svg)

[examples/stream/minor/Fm.svg](examples/stream/minor/Fm.svg)

[examples/stream/minor/Fsharpm.svg](examples/stream/minor/Fsharpm.svg)

[examples/stream/minor/Gm.svg](examples/stream/minor/Gm.svg)

[examples/stream/minor/Gsharpm.svg](examples/stream/minor/Gsharpm.svg)

[examples/stream/minor/Am.svg](examples/stream/minor/Am.svg)

[examples/stream/minor/Asharpm.svg](examples/stream/minor/Asharpm.svg)

[examples/stream/minor/Bm.svg](examples/stream/minor/Bm.svg)


PNG files

![examples/stream/minor/Cm.png](examples/stream/minor/Cm.png)

![examples/stream/minor/Csharpm.png](examples/stream/minor/Csharpm.png)

![examples/stream/minor/Dm.png](examples/stream/minor/Dm.png)

![examples/stream/minor/Dsharpm.png](examples/stream/minor/Dsharpm.png)

![examples/stream/minor/Em.png](examples/stream/minor/Em.png)

![examples/stream/minor/Fm.png](examples/stream/minor/Fm.png)

![examples/stream/minor/Fsharpm.png](examples/stream/minor/Fsharpm.png)

![examples/stream/minor/Gm.png](examples/stream/minor/Gm.png)

![examples/stream/minor/Gsharpm.png](examples/stream/minor/Gsharpm.png)

![examples/stream/minor/Am.png](examples/stream/minor/Am.png)

![examples/stream/minor/Asharpm.png](examples/stream/minor/Asharpm.png)

![examples/stream/minor/Bm.png](examples/stream/minor/Bm.png)


