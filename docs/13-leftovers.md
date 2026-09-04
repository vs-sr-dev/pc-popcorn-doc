# 13 — leftovers: what is still closed, and how close each one is

*Measure: **147,334 bytes** counted as unidentified by chapter 01's rule, plus
seven named questions inside them that this session opened far enough to
describe and not far enough to answer.*

## The three executables, 147,334 bytes, 86.9073 %

Counted as unidentified because reading an MZ header and stopping is not
reading a program — and, in `popcorn.exe`'s case, because **parsing an EXEPACK
container to residue zero in both directions is still not reading the program
inside it.** That decision is chapter 01's and it was available to go the other
way; it did not.

What was read of them is in chapters 03 to 08 and is a great deal. What was not
read is all of the code: 24,208 bytes of `popcorn.exe`'s own segment, all of
`popgen.exe` past its 141 strings, and all but about forty bytes of
`popspeed.exe`.

## Seven questions, each with what is known

**1. `lltf`, one byte, and it needs a disassembler.** `ltf.bat` passes `lltf`
and the file is `ltf.ppc`. Either the leading `l` is an undocumented flag or the
batch file never worked. **The string `.PPC` occurs zero times in `popcorn.exe`,
packed and unpacked**, so the game assembles the extension at run time and there
is no string to read the parser off. `popgen.exe` has `.PPC` in two of its
prompts. Settling it means disassembling the argument handler and this pipeline
has no disassembler. **Closer to an answer than it looks and still shut.**

**2. Which sound table is which event.** Chapter 08 reads the engine
instruction by instruction and finds a pointer array at `DS:00F8` indexed by a
sound number. **That array is all zero in the shipped image**, so it is built at
run time, and the code that builds it was not located: no `mov word [00F8],imm`,
no `mov di,00F8` for a block copy. The seven tables are described by contour and
not labelled.

**3. The fiftieth board.** The built-in set ends with a block whose 12 × 14 grid
is **168 cells of type 11**, a type that appears nowhere in either shipped
`.ppc`. A solid board of an otherwise-unused type at the end of a set is the
shape of an end screen. That is an inference and it stays one.

**4. What the sixteen cell types are.** Types 0, 1, 2, 3, 5, 6, 7, 8, 9, 10 and
16–21 occur; 4 and 11 do not. Types 3 and 9 are known **not** to be bricks,
because the header's brick count excludes exactly those two on 98 of 98 blocks.
Types 16–21 always appear as adjacent pairs, which is the shape of a two-cell
object with a left and a right half. **Naming any of them would be guessing and
none is named.** Rendering the game's own brick graphics would settle it, which
leads to:

**5. The CGA graphics, which are found and not decoded.** About 92,000 bytes of
the unpacked image between the strings and the code segment are two-bit-per-
pixel data: `0xAA`, `0x55`, `0xFF` and `0x00` dominate window after window, and
`tools/cga.py --scan` puts the flat-byte fraction between 40 % and 72 % across
that whole span. Rendered at 320 pixels wide, linear and interleaved, both come
out as structured stripes and not as pictures, so **the stride is not 80 bytes**
and the graphics are stored as sprites or tiles rather than as screens. An
autocorrelation over four sample regions gives no single convincing period:
strongest agreements at 24, 8, 32 (region 20,480–24,576), 56 and 112 (32,768–
36,864), 48 and 96 (64,000–72,000), 4 and 8 (86,016–92,160). **That is the shape
of several different sprite sizes in one file**, which is what a Breakout game
needs, and finding them one at a time was not attempted.

`popcorn.doc` says `F8 : Séléctionne une Palette de Couleur`, so both CGA
palettes are in there somewhere; no palette byte was located. `tools/cga.py`
exists, has all four IBM palettes and both bank layouts, and **identified
nothing**. It is left in `tools/` for whoever picks this up.

**6. `popspeed.exe`'s `$65534`.** `0xFFFE`, in a program whose documented range
is 0 to 30,000, at the end of its string table after the `$` that terminates
the last DOS-printed message. The value-passing mechanism is fully read in
chapter 07 and does not use it.

**7. What `LTF` is.** Chapter 07 sets out the evidence in both directions and
chapter 09 decides what to publish while it is open. **The owner of this machine
ran the game and confirmed that the high-score screen shows `LTF` with 546** —
which verifies `hsc.py` end to end and does not say who wrote the name. The
remaining step is one further on: beat 546 and see whether the game asks. This
is still the object's only leftover a human can close in thirty seconds.

## Two that were leftovers and are not any more

Recorded because the pre-briefing listed them as candidates for this chapter and
they closed.

**`23016745`, seven times.** It is a substitution token the credits scroller
replaces with the game's title, and the evidence is grammatical: it occupies the
subject position in *"`<TITLE>` est un FREEWARE…"* and the object position in
*"…les secrets de `<TITLE>`"*. It is not a permutation table and it is not a
telephone number. Chapter 05.

**How `popspeed.exe` passes its value.** Through the offset word of interrupt
vector 68h, written with DOS function 25h and read back with function 35h, with
a default of `0x6F` decremented to **110** — the number `popcorn.doc` prints.
Chapter 07.

## The clause, which is written and not left implicit

The brief allowed for this chapter to have to say *"this session could not
formulate the missing clause, and here is what would be needed."* **It is not
needed.** The clause is written as a rule with two corollaries and its
generating case in chapter 09, and the count of what it admits and refuses is
in the same chapter.

What is left open there is one judgement rather than one rule: **the handles
`CAZOU` and `SHIFT` are published**, on the reasoning that a mailbox on a
message service whose number is redacted and which has not existed for thirty
years reaches nobody, while the attribution of half a hidden message is the
object's own content. That is arguable, it is argued in chapter 09, and a later
session is invited to disagree with it in writing.
