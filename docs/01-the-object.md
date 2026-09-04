# 01 — the object: nine files, one denominator, and 13.0927 % said without apology

*Measure: 169,530 bytes in nine files; 22,196 of them identified by a reader in
`tools/` at residue zero, which is **13.0927 %** and is exactly the ceiling the
coverage rule allows, because 86.9073 % of this object is executable.*

## What it is

`POP-CORN`, a Breakout game for MS-DOS, CGA only, in French, **© 1988**, by
**LACAZE Christophe** and **RAYNAL Frédérick**, trading as **LACRAL software**.
It says of itself, in the first paragraph of its own manual:

> Ce programme fait parti du domaine public. Il ne doit servir à aucune fin
> commerciale sans accord préalable de l'auteur.

It is a directory installed on a hard disc. **No image, no cue sheet, no
filesystem, no medium** — the third object running without one — and, for the
first time in this series, **no archive either**. Nine files, none of which is
a container.

    name           bytes        sha1
    ltf.bat           16  76e0619e6dba7775f1f54da5867af548a70294d4
    ltf.ppc        8,630  c3dc207ff6d7098cc15581d6af1ba5720cecaef7
    pop.bat           13  83e7e3bfa9670a5fb370ccadc7f3f8a7d2394aef
    popcorn.doc    4,727  1e21b16124421812ee914feac591326a381fdff7
    popcorn.exe  103,848  a8b4a8e1402290c5bef3dba2e0781ba63c1cc8a1
    popcorn.hsc      180  0ea9555dd5762dc1433d97097ffccab28a7a5cee
    popgen.exe    42,354  bdff1d49db14a2e35f44247f708c17469d464175
    popspeed.exe   1,132  6742cc4f429cb4a7960f904da47c14c1759f9b30
    poptab.ppc     8,630  c09fe7f8d0141ebfa7db97a065c825ad4be18c19

**Nine files, 169,530 bytes, nine distinct sha1**, re-derived with
`tools/hashall.py` at the start of the session and again at the end, identical
both times. It is the smallest object this series has documented, one twelfth
of the one before it.

## One denominator, and the decision is the interesting part

Every previous object in this series had two denominators and every one of them
inherited the second from a container: D1 was the files, D2 was the archive
members plus the files that were not archives. **This object has no container,
so the two are the same number and there is only one.**

    D1 = 169,530 bytes, the nine files as they sit in the directory.

There was one candidate for a second. `popcorn.exe` is a Microsoft EXEPACK
image and chapter 04 unpacks it from 103,336 bytes of load image to **133,296
bytes** of program. **That number is deliberately not a denominator.** Making
it one would mean coverage rose whenever a session decompressed something,
which measures effort and not bytes explained. The decision is recorded in
`tools/account.py`'s docstring so the next object inherits the reasoning rather
than the number.

## The coverage rule, and the ceiling it puts on this object

The rule is inherited verbatim from
`pc-linksthechallengeofgolf-doc/docs/01-the-object.md` line 121:

> a record counts as identified when a reader in `tools/` parses it end to end
> with zero residue and every byte lands in a named field.

Reading a file as text counts. **Reading an MZ header and stopping does not.**

    147,334 of 169,530 bytes = 86.9073 % is executable
    which leaves a ceiling of  22,196 = 13.0927 %

`tools/account.py` prints the table:

| file | bytes | counted | why |
| --- | --- | --- | --- |
| `popcorn.doc` | 4,727 | **identified** | code-page-437 text, 121 CRLF lines |
| `poptab.ppc` | 8,630 | **identified** | `ppc.py`: `LACRAL` + 49 × 176, residue 0 |
| `ltf.ppc` | 8,630 | **identified** | `ppc.py`: `LACRAL` + 49 × 176, residue 0 |
| `popcorn.hsc` | 180 | **identified** | `hsc.py`: 10 × 18 ASCII records, residue 0 |
| `ltf.bat` | 16 | **identified** | text, one command line |
| `pop.bat` | 13 | **identified** | text, one command line |
| `popcorn.exe` | 103,848 | no | MZ header and EXEPACK container read; the program is not parsed |
| `popgen.exe` | 42,354 | no | MZ header read |
| `popspeed.exe` | 1,132 | no | MZ header read |

**COVERAGE ON D1: 22,196 / 169,530 = 13.0927 %**, and every non-executable byte
in the object closes. There is nothing left to identify that the rule permits.

## The number is low and that is the rule working

    1992   96.4344 %   Sherlock Holmes: Consulting Detective   (VIS)
    1992   95.8047 %   Race the Clock                          (VIS)
    1990   91.4640 %   Links: The Challenge of Golf            (MS-DOS)
    1993   73.1869 %   Skunny: Back to the Forest              (MS-DOS)
    1992   43.2720 %   Links: The Challenge of Golf            (VIS)
    2026   24.8524 %   DISSIDIA FF / DISSIDIA DUELLUM          (Android)
    1988   **13.0927 %**   POP-CORN                            (MS-DOS)

**This is the lowest figure in the series by eleven points and it is not a
failure.** The object before this one got 47.5675 points of its 73.1869 free
from a published ZSoft PCX specification and had to say so in three places.
**This object contains no public format at all** — every byte identified here
was identified by measuring, and the seventh column is what is left when
nothing arrives for free and five sixths of the object is a program.

**The rule was not touched to make the figure larger**, and the two obvious
ways to touch it were both available and both declined: counting the unpacked
image as a denominator, and counting an executable as identified because its
container was parsed to residue zero. Chapter 04 parses `popcorn.exe`'s EXEPACK
container to residue zero in both directions and the file still scores no.

**And the percentage is not the result of this session.** The result is in
chapters 04, 05 and 06: a packer identified where eight searches had found
nothing, 2,418 bytes of hidden text that no `strings` pass could reach, and a
level format whose header agrees with its own grid on 98 of 98 blocks. None of
those moves the percentage by a single byte.

## What the object keeps

* **its authorship, twice over.** The manual names both authors on its first
  page; the program carries a hidden message that names them again and says
  which of them did what — see chapter 05. That is more than most commercial
  products in this collection managed;
* **its own construction set.** A quarter of the object is `popgen.exe`, the
  level editor the authors shipped with the game, with a disc browser, a
  catalogue and a validation rule — see chapter 03;
* **both of its level sets**, and the built-in one inside the program;
* **its user state**, 180 bytes with one name in it — see chapter 07;
* **its distribution model whole**, in a paragraph headed *"COMMENT DONNER CE
  JEU A VOS AMIS ?"*

## What the object loses

* **its dates.** All nine files carry the identical mtime **`1996-12-24
  23:32:00`**, one distinct value over nine files, one-second resolution. That
  is an archiving pass, eight years after the product's own year. Chapter 10
  reads it against a neighbour and gets one hour, two ways;
* **its manifest.** `popcorn.doc` lists six files and the directory holds nine;
* **five sixths of itself to the coverage rule**, and one of those three
  executables gave up a great deal anyway.
