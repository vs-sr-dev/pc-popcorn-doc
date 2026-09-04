# 11 — the tools: seven written, one rewritten, and a self-skip that skipped nothing

*Measure: **436 Python files at the start of the session and 443 at the end**,
by `ls tools/*.py | wc -l` both times. Seven new; `account.py` rewritten in
place for the second session running and therefore not adding to the count.
`toolscan.py` returns **0 findings with all three positive controls firing**,
run at the halfway point and again at the end.*

## The seven written here

Every one of them was made to refuse a specimen that must fail **before** it
was allowed to census anything, and the refusal is on the record in chapter 02.

| tool | what it does | its refusal control |
| --- | --- | --- |
| `dosimage.py` | the four packing indicators for a real-mode MZ image in one table: block census with the constant-byte blocks separated, entropy, relocation count, entry-point distance from EOF, printable fraction | `--refuse-check` asserts a file is **not** an MZ and exits 1 if it is |
| `exepack.py` | identifies, validates and unpacks a Microsoft EXEPACK image; accounts for every byte of the tail including the packer's own relocation table | `--refuse` on 5 files, 5 of 5 refused, exit 0 |
| `popmsg.py` | extracts the XOR-0xAA credits message and accounts for every byte of it as one of three kinds | `--refuse` on `popgen.exe` and `poptab.ppc`, both refused |
| `ppc.py` | reads a `.PPC` level set: magic, 49 × 176, and the three header rules against the 12 × 14 grid | `--validate` on 3 non-`.ppc` files, 0 of 3 parsed, exit 1 |
| `hsc.py` | reads POP-CORN's high-score table, 10 × 18 ASCII | `--validate` on 3 files, 0 of 3 parsed, exit 1 |
| `pcspk.py` | reads a PC-speaker `(pitch, duration)` table and renders it to WAV as a square wave | refuses an offset that is not a table, exit 1 |
| `cga.py` | renders a byte region as CGA 320 × 200, four colours, both bank layouts; `--scan` reports the flat-byte fraction per window | nothing was identified with it — see chapter 13 |

Two design notes worth carrying forward.

**`dosimage.py` has a stated threshold and prints it.** A file of four blocks
reaches distinct-over-blocks 1.000 by having four different blocks, which is
arithmetic and not evidence; `MIN_BLOCKS = 32` is a module constant and the
summary line says *"counted only at >= 32 blocks"* rather than quietly dropping
`popspeed.exe` from the list.

**`popmsg.py` redacts by default and `--raw` is the opt-in.** The default should
be the safe one. See chapter 09.

## `account.py`, rewritten for the second session running

The inherited version walked `_work/members` and allocated archive share
proportionally across fifteen containers. **This object has no container**, so
none of that applies and none of it survives.

What replaced it is a table mapping each of the nine files to the reader that
closes it and to a sentence saying what the reader proved, plus a loud failure
if the directory and the table disagree in either direction:

    account.py: <name> is in game and not in the READERS table
    account.py: <name> is in the READERS table and not in game

**A silently skipped file is how a coverage figure becomes a lie.** The tool
exits 2 rather than printing a percentage it cannot justify.

## The negative controls, which cost one command each

The nine readers written for Copysoft's engine by the previous session are a
free negative control on a different publisher, a different decade and a
different country. Every one refuses:

| tool | result |
| --- | --- |
| `lid.py --validate` | 9 of 9 did not validate |
| `pcx.py --validate` | 9 of 9 failed |
| `mkb.py --mkb` | 9 of 9 did not close |
| `bpr.py --validate` | 9 of 9 did not close |
| `vce.py --validate` | 9 of 9 did not close |
| `ltab.py` | 9 of 9 tables did not close |
| `tds.py` | 9 of 9 carry no readable symbol table |
| `sbi.py` | 8 of 9 not a whole number of slots; the ninth opened and was refused on a range test |
| **`sbank.py --validate`** | 9 of 9 did not close — **and it refuses a single 176-byte `.ppc` block too** |

`sbank.py` was the one worth trying in both directions. It walks a chain of
`u16 w, u16 h, u16 n` headers, and a `.ppc` block is a header followed by a
grid, so the shapes are close enough that a false positive was possible. Given
`_work/ppc-block-02.bin` — one block, extracted, 176 bytes — it reports
*"1 of 1 members did not close"*. The refusal is the measurement.

From further afield: `mdmd.py --validate` refuses all nine, `steve.py` finds its
magic nowhere and refuses 9 of 9, `ne.py` refuses with a message and `pe.py`
refuses with a traceback.

`gamedata.py --hi` refuses `popcorn.hsc` on the arithmetic — *"180 bytes is not
a whole number of 26"* — and that refusal was put on the record before `hsc.py`
was written.

## What does not apply, said after looking

**The entire optical half is inert for the third session running**, and this
time there is no archive either: `iso9660.py`, `mode1.py`, `cdxa.py`,
`subch.py`, `toc.py`, `leadout.py`, `sectormap.py` — no medium, no image, no cue
sheet, no filesystem, no container. One line, as promised.

`wavcheck.py` had no audio to check until this session made some; the WAV files
in `_work/wav` are this repository's output and not the object's, so checking
them would be checking `pcspk.py` against itself. The fifteen Android tools,
the four AVI tools and the Tales tools have nothing here.

## The inherited defects, which are now eight

Six were on the standing list. **Two more were found here.**

| # | tool | defect | status |
| --- | --- | --- | --- |
| 1 | `bmp.py` | never reports how many files it opened | inherited, unfixed |
| 2 | `pe.py` | refuses a non-PE with a traceback instead of a message | inherited, reproduced here |
| 3 | `wavcheck.py` | lower-cases the filename but not the `--ext` argument | inherited, unfixed |
| 4 | `checkscore.py` | skips bolded table rows in silence | inherited, worked around here |
| 5 | `controltat.py` | `IndexError` on any file shorter than 199 bytes | inherited, **reproduced**: it dies on `pop.bat` |
| 6 | `mdmd.py` | prints two different verdict words, so `grep -c REFUSED` under-counts | inherited, avoided here |
| 7 | **`crossall.py`** | **its docstring says the repository being measured is skipped; `--skip` defaults to the empty string and nothing is skipped.** The only warning is a line reading `skipping : (nothing)` | **new** |
| 8 | **`crossall.py`** | `repositories swept` counts only repositories in which a 40-hex token was found, so a root full of documentation with no hash lists reports `0` and looks empty | **new** |

Defect 7 cost this session a wrong answer, not just a command: the first sweep
of root 7 reported **nine crossings**, every one of them this repository's own
hash listing matching itself, and a session in a hurry could have published it.
It is the same tool that cost the previous session a `PermissionError`, and the
same docstring that promises behaviour the code makes optional.

None of the eight is fixed here. Fixing an inherited tool silently is worse
than reporting it, because the next object's session reads the list and not the
diff.

## The scan

    python tools/toolscan.py

    files scanned                      : 443
    files with a forbidden control byte: 0

    === POSITIVE CONTROLS: each must be reported ===
      0x00  NUL, below 9         -> reported
      0x01  SOH, below 9         -> reported
      0x1B  ESC, inside 14..31   -> reported
    all three fired.

Run once at the halfway point of the session and once at the end, over `.py`,
`.md` and `.txt`, without being asked. Both runs: 0 findings, three controls.
