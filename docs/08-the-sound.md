# 08 — the sound: one engine, 131 bytes, and the tune that is not there

*Measure: the whole audio content of POP-CORN is **seven tables, 131 bytes, 59
notes**, at offsets 109,600 to 109,730 of the unpacked image. There are two
`out 42h`, one `out 43h` and six `out 61h` in the entire 133,296-byte program,
all of them in one routine, and no eighth table anywhere.*

## The engine, read out of the code

`popcorn.doc` lists `F9 : Son on/off`, so the object has sound. Finding it took
locating the only code in the image that touches the speaker hardware. At image
offset 109,731:

    b0 b6           mov al, 0B6h        ; PIT channel 2, mode 3, square wave
    e6 43           out 43h, al
    e4 61 0c 03     in al,61h / or al,3 ; gate and speaker on
    e6 61           out 61h, al
    c3              ret
    e4 61 24 fc     in al,61h / and al,0FCh
    e6 61 c3        out 61h, al / ret   ; and off

and the tick handler above it:

    8b 36 f6 00     mov si, [00F6]      ; the note pointer
    ad              lodsw               ; AL = pitch, AH = duration
    0b c0  74 37    or ax,ax / jz       ; a zero word ends the table
    89 36 f6 00     mov [00F6], si
    88 26 f5 00     mov [00F5], ah      ; duration, in timer ticks
    8a e0           mov ah, al
    b0 01  e6 42    mov al,1 / out 42h  ; the PIT divisor's LOW byte is always 1
    8a c4  e6 42    mov al,ah / out 42h ; its HIGH byte is the table's

**A note is two bytes: a pitch byte and a duration byte, and the pitch byte is
the high half of the PIT divisor.** The low half is hard-wired to 1, so

    divisor   = pitch * 256 + 1
    frequency = 1193182 / divisor

That is a coarse instrument on purpose. Pitch 5 gives 931 Hz, pitch 20 gives
233 Hz, and there are fifteen values in between — steps of a whole tone at the
top and a minor third at the bottom. **It cannot play a chromatic scale**, which
turns out to matter.

Further down, a second entry point takes a sound number in `AL`, doubles it,
adds `00F8` and reads a pointer out of the resulting table. `DS:00F8` is all
zero in the shipped image, so that pointer array is built at run time and this
session cannot say which table is which game event.

## The seven tables

`tools/pcspk.py` reads them, and the byte counts close: seven tables and seven
terminators occupy 109,600 to 109,731, where the code begins.

| offset | notes | seconds | contour |
| --- | --- | --- | --- |
| 109,600 | 4 | 1.54 | 233 → 259 → 333 → 466 Hz, lengthening |
| 109,610 | 4 | 1.54 | 582 → 291 → 388 → 582 Hz |
| 109,620 | 4 | 1.54 | 931 → 358 → 518 → 931 Hz |
| 109,630 | **19** | 4.06 | three descending-then-ascending arcs, each shorter |
| 109,670 | 12 | 4.50 | 518 Hz falling to 93 Hz in twelve steps |
| 109,696 | 11 | 1.21 | alternating 466/39, 311/47, 466/58, 931/47 Hz — a warble |
| 109,720 | 5 | 2.42 | 93 → 78 → 58 → 47 → 39 Hz, the last held twenty ticks |

**59 notes.** The longest is nineteen. Durations are in timer ticks; the stock
rate of 18.2064 Hz is assumed and stated rather than measured, so the pitches
are right and the tempo is only right if the game leaves timer channel 0 alone.

    python tools/pcspk.py _work/popcorn.unpacked.bin --all _work/wav \
        --from 109600 --to 109740

writes one WAV per table, plus all seven in sequence, as square waves — which
is literally what PIT mode 3 produces, so the rendering makes no choice the
hardware did not make. A short linear fade at each edge keeps the clicks out;
the hardware had the clicks and this is a rendering, not an emulation.

## The tune that is not there

The object is called POP-CORN and the obvious guess is that it plays Gershon
Kingsley's *Popcorn*. **It does not, and the negative is measured four ways.**

1. **No chromatic table.** A search of all 133,296 bytes for any run of six or
   more `u16` values in successive ratios of 1.04 to 1.08 — the shape of a
   note-frequency lookup — returns **zero**;
2. **No long note table.** A scan of the whole image for runs of `(pitch,
   duration)` pairs terminated by a zero word finds nothing longer than
   **nineteen notes** anywhere in the program's own segment. The longer hits it
   reports elsewhere are the default high-score table (hyphens and zeros read as
   pairs) and the level blocks of chapter 06;
3. **No second engine.** Two `out 42h`, one `out 43h`, six `out 61h`, five
   `in 61h` in the whole image, all in the one routine above. There is nowhere
   else for music to come from;
4. **The instrument cannot play it.** With the divisor's low byte nailed to 1,
   the available pitches are 931, 776, 665, 582, 518, 466, 424, 388, 358, 333,
   311, 291, 274, 259, 245, 233 Hz. That is not a scale, and *Popcorn* is a
   melody with semitones in it.

**And the owner of this machine listened to all seven and reports: they are
sounds, and none of them is a recognisable melody.** That is his observation,
attributed to him, and it is the only end-to-end verification that exists on
this reader — the same role his ear played on the twelve `.VCE` files of the
previous object. It agrees with all four measurements.

So the seven tables are what they look like: a bounce, a brick, a lost life, a
level cleared, and a game over. **A Breakout game named after a pop tune, which
never plays it.**

## What this does not settle

Which table belongs to which event. The pointer array at `DS:00F8` is filled at
run time and the code that fills it was not located; the contours above are
descriptions of shape, not labels. It is in chapter 13.
