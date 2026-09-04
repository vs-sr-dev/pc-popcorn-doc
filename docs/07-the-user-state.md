# 07 — the user state: 180 bytes, three letters, and a number passed in an interrupt vector

*Measure: `popcorn.hsc` is **180 = 10 × 18** bytes, every one of them printable
ASCII, ten records of a 12-byte name and a 6-digit score, residue **+0**. Nine
records are the default; **one is not**. The same 180-byte default sits inside
`popcorn.exe` at offset 15,938 of the unpacked image.*

## The extension is not the format

`.HSC` is a well-known AdLib tracker music format, and this collection already
documents it as one: `pc-wackywheels-doc/docs/09-skunny-kart.md` records
`MENU.HSC`, `WKTRACK1.HSC` and four more as music inside Skunny Kart, two
objects ago.

`popcorn.hsc` is a high-score table, and the object says so itself, in its own
manifest:

> `- POPCORN.HSC  : Le fichier des High Scores.`

**Two products in one collection, one extension, two unrelated formats.** The
trap was disarmed before this session started; the reason it is a chapter and
not a footnote is that this is the cheapest demonstration the collection will
ever get that an extension is a naming convention and not a claim about bytes.

`tools/hsc.py` refuses on the shape, not on the name:

    python tools/hsc.py --validate game/poptab.ppc game/popcorn.exe game/pop.bat
    poptab.ppc   REFUSED: 8630 bytes is not a whole number of 18-byte records
    popcorn.exe  REFUSED: 103848 bytes is not a whole number of 18-byte records
    pop.bat      REFUSED: 13 bytes is not a whole number of 18-byte records
    hsc.py: 0 of 3 inputs parsed        (exit 1)

And `tools/gamedata.py --hi`, the high-score reader written two sessions ago for
a 26-byte record, refuses this file for the same kind of reason and was made to
say so on the record before anything new was written:

    popcorn.hsc  REFUSED: 180 bytes is not a whole number of 26

## The format

    +0   12   name,  ASCII, space-padded and centred
    +12   6   score, ASCII decimal, zero-padded
    x10

No header, no count, no terminator, no binary field anywhere. The empty slot is
twelve `-` and `000000`.

    popcorn.hsc      180 bytes = 10 x 18, residue +0, 1 of 10 slots filled
        0  name '    LTF     ' score 000546   <-- filled
        1  name '------------' score 000000
        ...
        9  name '------------' score 000000

**`LTF` is centred**: four spaces, three letters, five spaces. Something wrote
those twelve bytes as a unit.

## The default table is inside the program

A search of the unpacked `popcorn.exe` for the empty-record pattern finds it at
offset **15,938**, repeated ten times in a row: **180 bytes of `------------`
and `000000`**, immediately before `LACRAL software` and the hidden message of
chapter 05.

So the file the game ships is the file the game writes when nobody has played
it, and the game does not need `popcorn.hsc` to exist. That also settles the
one thing the pre-briefing inferred from the string `popcorn.hsc/`:

    packed   : b'popcorn.hsc/\x00\xb2'   at 589
    unpacked : b'popcorn.hsc\x00\x00\x00'  at 5148

**There is no trailing slash.** The `/` is a byte of the EXEPACK command stream
that happens to sit against the end of a literal run, and it disappears the
moment the file is decompressed. The pre-briefing's reading — *"what a filename
built by string concatenation against a path separator looks like"* — was a
reasonable inference from a compressed file and it is wrong. It is in
chapter 12.

## `LTF`, which is the object's live personal-data question

`LTF` is also the stem of `ltf.ppc` and of `ltf.bat`. So it is either

* **somebody's initials**, typed at a high-score prompt, in which case it is
  user state belonging to whoever typed it, or
* **the name of a level set** that the program writes into the table by itself.

Two measurements bear on it and neither closes it.

**For initials.** The program's own play field carries the string
`' JOUEUR 1: ------------   COMPUTER  '` — a twelve-character name field beside
`JOUEUR 1`, defaulting to the same twelve hyphens as the high-score table. A
program that displays a twelve-character player name has somewhere to get one
from.

**Against a level-set label.** Nothing in the object writes a set name into the
score file, and the built-in set has no name at all. But `ltf.ppc` and `ltf.bat`
were both added to this disc after the manual was written (chapter 03), by the
same hand, at the same time as the score was set.

## The reader, verified end to end by a human

**The owner of this machine ran the game and reports that the high-score screen
shows `LTF` with 546 points.** That is his observation, attributed to him, and
this session executed nothing.

It is the only end-to-end verification that exists on `hsc.py`, and it is worth
more than it looks. Everything above is an argument that 180 bytes of ASCII
divide into ten 18-byte records of a 12-byte name and a 6-digit score — an
argument from arithmetic and from the shape of the default row, with no
independent witness. **The witness is the game itself**: the bytes at offsets 0
to 17 of `popcorn.hsc` render on a CGA screen as the name and the number this
reader says they are. A wrong record width, a wrong field split or a wrong
denominator would have shown up there and did not.

The same role was played on the previous object by the owner listening to twelve
extracted WAV files and confirming they matched their names, and on this one by
his verdict on the seven sound tables in chapter 08. **Three objects running,
the cheapest verification available has been a person looking at the thing.**

## What it does not settle

It confirms that the file the game reads is the file this repository parsed. It
does not say **who or what wrote `LTF` into it**, which is the live question:
seeing a name displayed is not seeing it typed.

**The remaining measurement is one step further on**: beat 546 and see whether
the game asks for a name. If it prompts, `LTF` is somebody's initials and is
user state belonging to whoever typed it; if the new score simply appears with
a label the program chose, it is not. Until then chapter 09 decides what this
repository publishes, which is the conservative thing, and chapter 13 records
the question as open. **No name is printed here that the object does not print
about itself**, and `LTF` is three letters that could be initials, so it is
treated as if it were.

## What `POPSPEED` writes, and it is not a file

The pre-briefing asked how a program that *"ne modifie pas la vitesse réelle de
l'ordinateur mais mémorise la valeur donnée"* passes its value, and noted there
is no fourth file on the disc for it to write to. There is no file because it
does not use one.

`popspeed.exe` has 620 bytes of load image. The last four instructions before it
exits are:

    8b d3        mov dx, bx        ; bx = the number parsed from the command line
    b8 68 25     mov ax, 2568h     ; DOS 25h: Set Interrupt Vector, vector 68h
    cd 21        int 21h
    b8 00 4c     mov ax, 4C00h
    cd 21        int 21h

**It stores the value as the offset word of interrupt vector 68h** — four bytes
at `0000:01A0`, a vector DOS and the BIOS do not use — and exits. There is
exactly one matching read in the whole object:

    06           push es
    b8 68 35     mov ax, 3568h     ; DOS 35h: Get Interrupt Vector, vector 68h
    cd 21        int 21h           ; -> ES:BX
    83 fb 01     cmp bx, 1
    74 09        je  ...
    0b db        or  bx, bx
    75 0b        jnz ...
    bb 6f 00     mov bx, 006Fh     ; the default: 111
    ...
    4b           dec bx            ; 111 - 1 = 110

at offset 131,745 of the unpacked `popcorn.exe`. **`0x6F` is 111, the `dec`
makes it 110, and `popcorn.doc` says the default is 110.** A constant in a
1988 binary and a sentence in its manual, agreeing exactly, with the
decrement in between explaining the off-by-one.

That is a whole inter-process protocol between two programs on the same disc,
carried in four bytes of the interrupt vector table, with a defaulting rule and
a documented value. It also explains why the `SPEED` / `POPSPEED` rename of
chapter 03 never broke anything: whoever typed `SPEED` and got `Bad command`
simply got the default.

**It is the only mechanism in this object that is genuinely of its decade** and
would not be legal on any protected-mode system built since.
