# POP-CORN — a measured directory

A byte-level documentation of one installed MS-DOS game directory: nine files,
169,530 bytes, LACRAL software, France, **© 1988**, public domain by its own
statement. **No product bytes are in this repository** — hashes, formats,
figures and the commands that reproduce them are.

## The short sheet

| | |
| --- | --- |
| object | `POP-CORN`, a Breakout game, LACRAL software, MS-DOS, CGA |
| year | **1988**, stated on the manual's own first line |
| authors | **LACAZE Christophe** (code) and **RAYNAL Frédérick** (graphics), named on the manual's first page and again inside the program |
| medium | **none.** A directory on a hard disc, for the third object running — and the first with **no archive either** |
| files | 9, 169,530 bytes, 9 distinct sha1 |
| denominator | **one, D1 = 169,530.** No container, so no second — decided explicitly, chapter 01 |
| coverage | **D1 13.0927 %**, the lowest in the series, and **exactly the ceiling**: 86.9073 % of the object is executable and the rule counts an executable as unidentified |
| third parties | **Microsoft EXEPACK**, inside `popcorn.exe` — 376 bytes of stub, error string and relocation table |
| the packing question | four indicators said packed, eight signature searches said no. **The searches looked for the packer's name, which appears in no packed file.** `RB` at `entry − 2` and `Packed file is corrupt` are what is actually there |
| unpacked | 103,336 → **133,296 bytes**, residue **+0 at both ends** of the decompression |
| the hidden message | **2,418 bytes**, CP437 XORed with 0xAA, inside the packed image. Names both authors, says who did what, and says the graphics were drawn with **NEO on an Atari ST** |
| `.PPC` | `LACRAL` + 49 × 176, residue 0 on 2 of 2. An **8-byte header** and a **12 × 14** grid; three header fields agree with the grid on **98 of 98** blocks |
| levels | 49 in the shipped file, **50 inside the program** — and the hidden message says fifty |
| `.HSC` | a high-score table, 10 × 18 ASCII. **The same extension is AdLib tracker music elsewhere in this collection** |
| sound | one PC-speaker engine, seven tables, **131 bytes and 59 notes**. A game named after a pop tune that never plays it |
| provenance | **one mtime on nine files**, `1996-12-24 23:32:00` — exactly one hour after the thirty-two files of `pc-linksthechallengeofgolf-doc`. Two readings, chapter 10 |
| personal data | **the names yes, the contact details no.** The criterion gained a clause this session — chapter 09 |
| predictions | 60 clauses written first; inherited **9.775 of 13**, open **24.50 of 47** |
| tools | 436 → **443**; seven written, `account.py` rewritten |

## The clause this repository adds to the criterion

The pipeline's fifty-three-session rule — *a name put by its owner inside a
product they made and sold to the public is published* — had never been asked
about a street address belonging to two named private individuals. **The clause
it was missing, in full, with its corollaries and the case that generated it,
is [docs/09](docs/09-the-names.md):**

> **Identity and reach are not the same datum.** A datum that *identifies* a
> person is admitted by the criterion. A datum by which a stranger could
> *arrive at* a person is not, however plainly the product printed it and
> however long ago. Contact details are reported as a shape — kind, count and
> location — and never as their digits.
>
> Because **"published" is not one act.** Publication inside a product is
> bounded by that product's distribution; the same string in a public
> repository in 2026 is indexed, permanent and joined by search to every other
> occurrence of the same name. **Republishing is not repeating.**

## The chapters

| | |
| --- | --- |
| [00](docs/00-predictions.md) | predictions — 60 clauses, written before anything was opened |
| [01](docs/01-the-object.md) | the object — nine files, one denominator, and 13.0927 % said without apology |
| [02](docs/02-the-technical-sheet.md) | the technical sheet — every figure with the command that remakes it |
| [03](docs/03-the-manual.md) | the manual — a construction set, a gift, and three files that are not on the list |
| [04](docs/04-the-packed-program.md) | the program — four indicators, eight failed searches, and a two-byte signature |
| [05](docs/05-the-hidden-message.md) | the message — 2,418 bytes that no `strings` pass could ever have found |
| [06](docs/06-the-levels.md) | the levels — a grid that is twelve wide, and the fiftieth board |
| [07](docs/07-the-user-state.md) | the user state — 180 bytes, three letters, and a number passed in an interrupt vector |
| [08](docs/08-the-sound.md) | the sound — one engine, 131 bytes, and the tune that is not there |
| [09](docs/09-the-names.md) | the names — the clause the criterion was missing, and the door it stops at |
| [10](docs/10-against-the-collection.md) | against the collection — zero over seven roots, one hour, and a checklist that is now due |
| [11](docs/11-the-tools.md) | the tools — seven written, one rewritten, and a self-skip that skipped nothing |
| [12](docs/12-corrections.md) | corrections — nine, of which four are the pre-briefing's and three are this session's own |
| [13](docs/13-leftovers.md) | leftovers — what is still closed, and how close each one is |
| [14](docs/14-prediction-scoring.md) | prediction scoring — 9.775 of 13 inherited, 24.50 of 47 open |

## The tools

`tools/` holds 443 Python files, standard library only, carried forward across
the collection. The seven written here:

    dosimage.py   the four packing indicators for a real-mode MZ image, in one
                  table, with the constant-byte blocks separated from the
                  repeats and a stated minimum block count
    exepack.py    identify, validate and unpack a Microsoft EXEPACK image, and
                  account for every byte of its tail
    popmsg.py     extract the XOR-0xAA credits message; redacts by default
    ppc.py        read a POP-CORN level set to residue zero
    hsc.py        read POP-CORN's high-score table
    pcspk.py      read a PC-speaker note table and render it to WAV
    cga.py        render a byte region as CGA 320x200 — and it identified
                  nothing here, which is chapter 13

Every one of them was made to refuse a specimen that must fail before it was
allowed to census anything.

## What is not here

The nine files of the object. `game/`, `_pre/`, `_work/` and `prompt.txt` are
in `.gitignore`, verified in both directions with `git check-ignore` and with
`git add -An` before anything was committed. The object's own prose is quoted
only where a measurement needs it, and its authors' contact details are not
quoted at all.
