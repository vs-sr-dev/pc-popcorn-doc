# 06 — the levels: a grid that is twelve wide, and the fiftieth board

*Measure: `LACRAL` + 49 × 176 on 2 of 2 files at residue **+0**, and inside
each 176-byte block an 8-byte header and a **12 × 14** grid whose three header
fields agree with the grid on **98 of 98, 98 of 98 and 98 of 98** blocks. One
block of the ninety-eight carries stale bytes in a field its own count says are
unused.*

## The container, which was already open

Both `.ppc` files are 8,630 bytes and both begin with the six ASCII bytes
`LACRAL` — the studio's own name, used as a magic. `8,630 − 6 = 8,624 = 49 × 176`
exactly, on 2 of 2, with no remainder and no count field anywhere.

`popgen.exe` carries *"Ce Fichier n'est pas un Fichier des Tableaux POP-CORN"*
and `popcorn.exe` carries *"****** Ce fichier n'est pas un fichier de Tableaux
******"*, so that magic is what both programs test.

    python tools/ppc.py --validate game/popcorn.hsc game/popgen.exe game/pop.bat
    popcorn.hsc  REFUSED: magic is b'    LT', not b'LACRAL'
    popgen.exe   REFUSED: magic is b'MZr\x01S\x00', not b'LACRAL'
    pop.bat      REFUSED: magic is b'POPCOR', not b'LACRAL'
    ppc.py: 0 of 3 inputs parsed        (exit 1)

The refusal is run before the census, on a specimen that must fail, and
`pop.bat` is the interesting refusal of the three: it begins `POPCOR`, so a
reader that tested five bytes instead of six would have accepted it.

## The grid is twelve wide, not sixteen

The pre-briefing read each block as a 16-byte header and a **16 × 10** grid, on
the strength of one block whose lead byte matched its non-zero cell count, and
recorded that two other blocks refused it in both directions. It refused
because the grid is not sixteen wide.

**It is 12 × 14 with an 8-byte header, and 8 + 12 × 14 = 176.**

The evidence is not arithmetic — several factorisations of 168 exist — but
symmetry. At width 12 the blocks come out as pictures:

    python tools/ppc.py game/poptab.ppc --render 3

    block 3: 90 bricks, 0 type-9 at []
         0  1  2  3  4  5  6  7  8  9 10 11
     0   2  2  2  2  2  2  2  2  2  2  2  2
     1   2  1  1  1  1  1  1  1  1  1  1  2
     2   2  1  2  2  2  2  2  2  2  2  1  2
     3   2  1  2  .  .  .  .  .  .  2  1  2
     4   2  1  2  .  .  .  .  .  .  2  1  2
     5   2  1  2  .  .  .  .  .  .  2  1  2
     6   2  1  2  .  .  .  .  .  .  2  1  2
     7   2  1  2  .  .  .  .  .  .  2  1  2
     8   2  1  6  6  6  6  6  6  6  6  1  2
     9   .  .  .  .  .  .  .  .  .  .  .  .
    10   .  .  .  .  .  .  .  .  .  .  .  .
    11   6  6  6  6  6  6  6  6  6  6  6  6
    12   .  .  .  .  .  .  .  .  .  .  .  .
    13   .  .  .  .  .  .  .  .  .  .  .  .

A nested rectangle, left-right symmetric on every row. At width 16 those same
bytes straddle two rows and read as noise. Block 2 is five clean full-width
rows of alternating types 2 and 7; block 1 is a wall four cells wide beside a
field seven wide.

**Bricks are four cells wide**, so a row of twelve holds three of them, which
is what the runs `1 1 1 1`, `8 8 8 8`, `6 6 6 6` in every block are.

## The lead byte, which the pre-briefing could not make agree

It is not the count of non-zero cells. Read that way it agrees on 12 of 49 in
`poptab.ppc` and 0 of 49 in `ltf.ppc`.

**It is the count of non-zero cells that are neither type 3 nor type 9.**

| rule | agrees on |
| --- | --- |
| `header[0]` == non-zero cells − type-3 cells − type-9 cells | **98 of 98** |
| `header[1]` == number of type-9 cells in the grid | **98 of 98** |
| `header[2..7]` == the grid indices of those cells, zero-padded to six | **97 of 98** |

So the whole eight-byte header is named:

    +0   1   bricks   destructible cells: non-zero, and not type 3 or type 9
    +1   1   n9       how many type-9 cells, 0..6
    +2   6   slots    their grid indices, zero-padded

Types 3 and 9 are the two kinds of cell that are **not a brick the player has
to clear**. That is almost certainly the rule `popgen.exe` enforces when it
refuses to save with *"Sauvegarde Impossible. Erreur de Conception du Tableau
n"* — a layout whose brick count is zero can never be finished, so the editor
has to compute exactly this number before it writes. **The disagreeing lead
byte and the design-error message were the same question**, as the brief
guessed, and the answer is that the lead byte is a playability check.

`popgen.exe` also carries *"Choisissez avec quel Tableau vous voulez faire la
Permutation."* — the editor can swap two boards within a set — which is why the
format has no per-block index: position in the file **is** the board number.

## The one block that disagrees, and it is a dirty buffer

    NOTE: block 14: unused slots carry [162, 163] -- a dirty buffer

Block 14 of `poptab.ppc` says `n9 = 4` and its grid has four type-9 cells at
63, 68, 161 and 162. Its six slot bytes read `63, 68, 161, 162, 162, 163`. The
first four are right; the last two are **left over from a state in which the
board had six**.

A reader that trusts `n9` never sees it, which is why `tools/ppc.py` tests the
unused slots separately and reports 97 of 98 rather than folding it into a
pass. The previous object had the same effect in its archive directory, where
short member names carried the tail of the previous name; this is the same
editor bug in a different decade and a different country. **Somebody deleted
two special cells from board 14 and saved, and the editor rewrote the count and
the first four slots and not the other two.**

Those bytes are still in a named field. The field is `slots[4..5]`, its width is
known and its meaning is known; what it holds is stale. The file therefore
still closes at residue zero, and chapter 01 counts both `.ppc` files as
identified — with this said out loud rather than quietly.

## What is in the two files

`tools/ppc.py` over both:

    poptab.ppc  8630 bytes, magic LACRAL, 49 blocks x 176, residue +0
    ltf.ppc     8630 bytes, magic LACRAL, 49 blocks x 176, residue +0

    distinct blocks in poptab.ppc : 48 of 49
    distinct blocks in ltf.ppc    :  2 of 49
    blocks the two files share    :  1

**`ltf.ppc` is a degenerate level set.** Its block 0 is its own; **blocks 1
through 48 are forty-eight identical copies of `poptab.ppc`'s block 1.** That is
why a stride scan agrees 0.980 at 176 on `ltf.ppc` and 0.085 on `poptab.ppc` —
the near-perfect periodicity was not a property of the format, it was a
property of one file being almost empty. Somebody opened `POPGEN`, drew one
board, and saved; the editor filled the other forty-eight slots with whatever
was in the buffer.

`poptab.ppc` has one duplicate pair of its own: **blocks 7 and 22 are the same
board**, which is 48 distinct of 49.

The cell-type census over all 16,464 cells of the ninety-eight blocks:

| type | cells | share | notes |
| --- | --- | --- | --- |
| 0 | 7,528 | 45.72 % | empty |
| 1 | 2,551 | 15.49 % | |
| 2 | 3,580 | 21.74 % | the commonest brick |
| 3 | 1,118 | 6.79 % | **not counted as a brick** |
| 5 | 345 | 2.10 % | |
| 6 | 261 | 1.59 % | |
| 7 | 380 | 2.31 % | |
| 8 | 495 | 3.01 % | |
| 9 | 61 | 0.37 % | **not counted as a brick**, and indexed in the header |
| 10 | 91 | 0.55 % | |
| 16–21 | 9 each | 0.05 % each | six types, each exactly nine times, in nine blocks |

**There is no type 4 and no type 11 in either file**, and type 11 turns up in
exactly one place in the object — see below. Types 16 to 21 always appear as
adjacent pairs (16/17, 18/19, 20/21), which is the shape of a two-cell object
with a left half and a right half. Naming any of the sixteen types would be
guessing and none is named here.

Eighteen of ninety-eight blocks carry a type-9 cell at all, sixty-one cells in
total; eighty-four of ninety-eight carry a type 3. **The header's six slot bytes
are sized for the worst case and the worst case is six**, which is the largest
`n9` in the object.

## The fiftieth board, which is not in any file

The hidden message of chapter 05 says:

> `>C:` … vous arriverez peut-être au bout des **50 tableaux**…

`POPTAB.PPC` holds forty-nine. The other one is inside the program.

At offset **50,284** of the unpacked image — immediately after twelve bytes
reading `LACRALLACRAL`, which is the six-byte magic stored twice — there are
**fifty consecutive 176-byte blocks that satisfy all three header rules**, and
the fifty-first does not.

    consecutive valid blocks from 50284 : 50  (8800 bytes)
    block 50 header: 00 00 54 54 a8 a8 5c 7c   -- fails: n9 is 0 and the slots are not

That region is the game's **built-in level set**, sitting in the buffer a
loaded `.PPC` is read into — which is also why `LACRAL` occurs exactly twice in
`popcorn.exe`: once as the literal the file is compared against, once as the
header of the set already in the buffer.

Against the shipped file:

    embedded block k == poptab block k   : 42 of 49
    embedded blocks also in poptab (any) : 45 of 49
    embedded blocks also in ltf   (any)  :  0 of 49

**Forty-two of the forty-nine match position for position.** So `POPTAB.PPC` is
a near-copy of the built-in set with seven boards changed — *"Le jeu de Tableaux
d'origine modifiable avec POPGEN"*, as the manual calls it — and the fiftieth
board never left the executable.

The fiftieth is **168 cells of type 11**: the whole 12 × 14 grid solid, one
type, no gaps, lead byte 168. Nothing in either `.ppc` uses type 11 at all.
What it is for is not settled here; a full board of a type the editor never
writes, at the end of the set, is the shape of an end screen, and that is an
inference and is in the leftovers.
