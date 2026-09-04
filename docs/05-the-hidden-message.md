# 05 — the message: 2,418 bytes that no `strings` pass could ever have found

*Measure: one region of the unpacked image, offsets 16,157 to 18,575, in which
**every byte is one of exactly three kinds** — a CP437 character XORed with
0xAA (2,355 of them), a literal line feed (7), or one of seven copies of the
literal ASCII token `23016745` (56). 2,355 + 7 + 56 = 2,418, residue **+0**.*

## What it is

Behind the EXEPACK image of chapter 04, `popcorn.exe` carries a hidden credits
scroller: two and a half thousand characters in which the two authors say who
wrote what, thank a coffee machine, and argue with each other. `popcorn.doc`
lists ten function keys and the tenth is

> `- F10 : Touche spéciale pour employés.`

— *special key for employees.* This is almost certainly what it shows, and that
sentence is an inference from the manual and not a measurement, because nothing
is executed here.

**None of it is a string.** A printable-run scan over the shipped `popcorn.exe`
returns 512 runs and this text is in none of them, because every letter has had
bit 7 flipped and half its other bits with it. The previous object's lesson was
that the year, the company and the only person named were all drawn in pixels
and none was a string; **this is the same lesson with two locks on the door** —
a packer outside and a one-byte XOR inside — and neither lock was put there to
keep anyone out.

## The encoding, which has exactly three kinds of byte

    char ^ 0xAA     a CP437 character. 0x8A is a space; 0xCF is 'e'
    0x0A            a literal line feed, not XORed
    '23016745'      eight literal ASCII digits, not XORed

`tools/popmsg.py` finds the region by anchoring on one encoded sentence and
growing outwards while every byte is one of the three, so it reports honestly
when a different build has nothing. The character class it grows through is
ASCII `0x20..0x7E` plus the CP437 accented band `0x80..0x97`, and **both edges
of that range were found by being wrong**:

* too wide, at first — anything decoding to `0x20` or above admits `0x00`,
  because `0x00 ^ 0xAA` is `0xAA`, which is a printable CP437 character. The
  region grew from 2,418 bytes to 5,203 by eating the zero padding on both
  sides;
* too narrow, next — stopping at `0x8F` cut the message off after 746 bytes at
  the *ù* of *"où les nuits"*, because French also needs `0x93`, `0x96` and
  `0x97`.

It stops at `0x97` deliberately: the eight digits of the token decode to exactly
`0x98..0x9F`, and admitting those would let the token be absorbed as text
instead of counted as a token. One byte of left-edge fuzz remains and is
visible in the output as a stray `ò` — the greedy scan takes one byte more than
the message, and saying so is cheaper than trimming it by hand.

## `23016745` was not a permutation and is not a telephone number

The pre-briefing recorded `23016745` as *"eight digits, each of 0..7 exactly
once. A permutation table, in the middle of a CGA game, repeated. Unread."*

It occurs **seven times, each followed by a literal line feed**, and the
evidence for what it is comes from grammar rather than from arithmetic. Two of
the seven sit where the game's own title belongs in sentences that otherwise
have no subject:

> `<TITLE>` est un FREEWARE qui vous est grâcieusement offert par LACRAL
> software.

> … nous vous laissons découvrir les secrets de `<TITLE>`

**It is a substitution token the scroller replaces with the title.** Five of the
seven come first, one per line, which is the shape of a multi-line title drawn
at the head of the scroll; the other two are inline.

And it is not a telephone number, which matters because there *is* a telephone
number in this message, twenty lines further on, and it is written
`nn.nn.nn.nn` — the French eight-digit form of 1988, in a completely different
shape. The two are not confusable once both are on the page, and only one of
them is published. See chapter 09.

## What the message says, and what is quoted here

The full text is 2,418 bytes of the authors' own prose. **Chapter 09 sets out
why the parts of it that are contact details are not reproduced in this
repository**, and `tools/popmsg.py` redacts them by default: `--raw` is
available to a reader working on their own copy of the object.

What is quoted is what the object could not otherwise say about itself.

> Ce programme a été écrit entièrement en **ASSEMBLEUR** par **LACAZE
> Christophe**. Les graphismes et animation ont été réalisées par **RAYNAL
> Frédérick** grâce au programme **NEO sur Atari ST**.

Three facts, none of which is anywhere else in the object:

1. **It is hand-written assembler.** The pre-briefing's finding that none of
   the three executables carries a compiler copyright string was correct and
   had no explanation; here is the explanation, from the program itself. It
   also explains a 103 KB real-mode image with a single segment for code and
   data and 35 relocations;
2. **the division of labour.** Lacaze wrote the code; Raynal did the graphics
   and animation. The object is a documented first credit and it says which
   credit;
3. **the tool, and it is on another machine entirely.** The CGA artwork in this
   MS-DOS game was drawn with **NEO** — NEOchrome — **on an Atari ST**, and then
   moved across. That is a fact about 1988 practice that no amount of measuring
   the bytes would have produced.

The two authors also sign themselves with handles — **CAZOU** for Christophe
and **SHIFT** for Frédérick — and the message is partly a dialogue, marked
`>C:` and `>S:`, in which they interrupt each other:

> `>S:` D'abord son jeu a été pompé dans un bouquin, même pas de mérite…
> `>C:` Ouais c'est ca, et le bouquin c'est toi qui l'a écrit peut-être…

They record that POP-CORN took **four months** of work, that the nights were
longer than the days, and that a coffee machine died during it. And they say,
in the sentence that turns out to be a measurement:

> `>C:` … vous arriverez peut-être au bout des **50 tableaux**…

**Fifty.** The shipped `POPTAB.PPC` holds forty-nine. Chapter 06 finds the
fiftieth.

## Where the names are, re-derived

`grep -aoc` over the nine files reproduces the pre-briefing's geometry exactly:

| token | files | counts |
| --- | --- | --- |
| `LACRAL` | 4 | `popcorn.exe` 2, `popgen.exe` 1, `ltf.ppc` 1, `poptab.ppc` 1 |
| `RAYNAL` | 1 | `popcorn.doc` 2 |
| `LACAZE` | 1 | `popcorn.doc` 2 |

**And the geometry is now wrong, in the only way that matters.** Both surnames
are also inside `popcorn.exe` — once each, in this message — and `grep` cannot
see them because they are packed and then XORed. The pre-briefing's *"the
studio name is in four files and the two people are in one"* becomes **the two
people are in two files, and the second one needed a decoder to say so.**

That correction cuts against this repository's own convenience: it makes the
personal-data question larger rather than smaller. It is in chapter 12 for that
reason.
