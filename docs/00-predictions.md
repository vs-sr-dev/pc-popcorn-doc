# 00 — predictions: what is left to measure when 86.9 % of the object is a program

*Measure: 60 clauses written before any byte of the object was read, 13 of them
re-deriving figures the pre-briefing handed over and 47 of them open; the two
totals, counted by `tools/predcount.py`, are inherited 10.95 of 13 and open
33.80 of 47.*

Written before opening anything. What had been done first, and only this:

* `ls -la game\` — **nine files**, and the byte counts and mtimes the directory
  listing prints;
* `ls tools/*.py | wc -l` — **436**;
* the collection roots counted at the moment of writing this line, by command:
  **seven roots, 242 directories, 122 `*-doc`, 83 of those with a `notes\`**;
* the six `_pre\` files and `prompt.txt` read end to end;
* `tools/blockrepeat.py` read, because the brief says to look at it first;
* `tools/predcount.py` and `tools/checkscore.py` read for their input shapes;
* four files of *other* repositories read for citation:
  `pc-linksthechallengeofgolf-doc/docs/01-the-object.md` for the coverage rule
  and its `1996-12-24 22:32:00`, `pc-skunnybacktotheforest-doc/docs/00-predictions.md`
  for the clause format, and the two repositories' `.gitignore` and `README.md`
  for the house style.

**No file of the object has been opened.** Not a `.ppc`, not the `.hsc`, not an
`.exe`, not `popcorn.doc`, not a `.bat`. The listing above is a directory
listing and nothing more. The `git check-ignore` and `git add -n` passes
touched no product byte and are reported in chapter 02.

---

## §A — the pre-briefing, which is worth zero points

Everything in this section came from `prompt.txt` and `_pre\`. It is reported
so the clauses below can be read against it, and **it scores nothing**.

**The object.** `POP-CORN`, LACRAL software, MS-DOS, CGA, French, **© 1988**,
public domain by its own statement. A directory installed on a hard disc: no
image, no cue sheet, no filesystem, **no medium**, for the third session
running — and **no archive either**, which is new. Nine files, 169,530 bytes,
nine distinct sha1. It is one twelfth of the object before it and the smallest
thing this series has documented.

**The dates are destroyed and say something anyway.** All nine files carry the
identical mtime `1996-12-24 23:32:00`, one second resolution, no fraction.
`pc-linksthechallengeofgolf-doc/docs/01-the-object.md` line 68 records
`1996-12-24 22:32:00` on all thirty-two files of a different game by a
different publisher. **One hour apart on the same Christmas Eve** — and one
hour is also the size of a timezone or daylight-saving reinterpretation of a
FAT timestamp. Two readings, and the brief requires both.

**Where the bytes are.** `popcorn.exe` 103,848 · `popgen.exe` 42,354 ·
`ltf.ppc` 8,630 · `poptab.ppc` 8,630 · `popcorn.doc` 4,727 · `popspeed.exe`
1,132 · `popcorn.hsc` 180 · `ltf.bat` 16 · `pop.bat` 13.

**And the pre-briefing's own arithmetic on that, which is wrong twice.**
`_pre\neighbours.txt` says *"86.2 % of the object is three executables"* and
*"capped at about 13.8 %"*. 103,848 + 42,354 + 1,132 = **147,334**, and
147,334 / 169,530 = **86.9073 %**, so the cap is **13.0927 %** and not 13.8 %.
Both figures are stated in the document that handed them over and both are
wrong; this is recorded here rather than claimed as a finding, because the
division was done before this document was written. **It sets the ceiling for
C37 and it goes in the corrections chapter.**

**`.ppc`.** Two files, 8,630 bytes each, both opening with the six ASCII bytes
`LACRAL` — the studio name — and 8,630 − 6 = 8,624 = **49 × 176**. A stride
scan gives 0.980 at 176 and at 352 on `ltf.ppc` against 0.535 at 175, 177, 351
and 353, and 0.085 at 176 on `poptab.ppc`. Read as a sixteen-byte header plus
a **16 × 10 grid of one-byte cell types**, the blocks look like brick layouts
four cells wide. **Block 2 of `poptab.ppc` has 60 non-zero cells and a lead
byte of 60; block 1 has 93 against 88; block 3 has 82 against 90.** One
confirmation, two refutations, in both directions. Blocks 0 and 10 of
`poptab.ppc` carry five non-zero leading bytes where the others carry one.

**`.hsc`.** 180 = 10 × 18: a 12-byte name and a 6-byte ASCII decimal score.
Record 0 is `LTF` / `000546`; nine records are twelve hyphens and `000000`.
The manual says it is the high-score file. **`.HSC` is also an AdLib tracker
music format and `pc-wackywheels-doc` records six of them inside Skunny Kart**
— same extension, same collection, unrelated formats.

**The three MZ files.** Header 512 on all three; images 103,336 / 41,842 / 620;
**residue +0 on 3 of 3**; `e_lfanew` 0 on all three, so no NE, LE, LX or PE; no
compiler copyright string in any of them. Entry points 1923:0010, 0008:0000
and 0000:0000.

**`popcorn.exe` repeats nothing.** 256-byte census counting distinct blocks and
separating the constant-byte ones: **405 blocks, 405 distinct, 1 constant**,
against `popgen.exe`'s 165 / 125 / 39 and `popspeed.exe`'s 4 / 4 / 1. Add
entropy **6.1130** against 3.5168 and 3.9324, **zero relocations in 103 KB**,
and an entry point **360 bytes from the end of the file**. Four indicators say
packed. `LZ09`, `LZ91`, `PKLITE`, `diet`, `EXEPACK`, `RJSX`, `WWPACK` and
`TINYPROG` occur **zero times each**. And there are **512 printable runs** of
five or more characters, in French, which a uniformly compressed image does not
have. `23016745` occurs seven times in a row.

**`popgen.exe` is a level editor** with 141 strings, a file browser, and
*"Sauvegarde Impossible. Erreur de Conception du Tableau n"* — so it validates
a layout before saving, so a `.ppc` block has a rule to satisfy.
`LACRALLACRAL` occurs as twelve consecutive bytes.

**`popspeed.exe` calls itself `SPEED`** in its own help text, ships as
`POPSPEED.EXE`, and the manual's batch recipe says `SPEED`. A rename fossil in
three places. Documented range 0..30000, default 110, and `$65534` = 0xFFFE in
its strings. **No fourth file exists for it to write its value to.**

**The two batch files.** `pop.bat` is 13 bytes, `POPCORN %1`, which is the
manual's own example. `ltf.bat` is 16 bytes, `popcorn lltf`, **with two l's**,
against `ltf.ppc` on the disc.

**The manifest gap.** `popcorn.doc` lists six files; the directory holds nine.
The three extra are `pop.bat`, `ltf.bat` and `ltf.ppc`.

**The privacy geometry, handed over.** `grep -aoc` over the nine files:
`LACRAL` in four files (`ltf.ppc` 1, `poptab.ppc` 1, `popcorn.exe` 2,
`popgen.exe` 1); `RAYNAL` twice in `popcorn.doc` and nowhere else; `LACAZE`
twice in `popcorn.doc` and nowhere else. **The studio name is in four files and
the two people are in one.** `popcorn.doc` also carries a postal address, a
Minitel service number and two mailbox handles.

**The coverage rule is inherited and cited from its source**,
`pc-linksthechallengeofgolf-doc/docs/01-the-object.md` line 121: *a record
counts as identified when a reader in `tools/` parses it end to end with zero
residue and every byte lands in a named field.* Reading a file as text counts.
**Reading an MZ header and stopping does not.** That repository reported
91.4640 % on D1 and 95.4061 % on D2.

**The thesis column, from each repository's own `docs\`:** 96.4344 · 95.8047 ·
91.4640 · 73.1869 · 43.2720 · 24.8524.

**The tools.** 436 `.py`. Run already: `mz.py`, `entropy.py --tree`,
`hashall.py`. Not run and applicable: `protscan.py`, `crossall.py`, `ne.py`,
`pe.py`, `toolscan.py`, `predcount.py`, `checkscore.py`, `redactnames.py`,
`blockrepeat.py`, `account.py`. Six inherited defects on the standing list:
`bmp.py` never says how many files it opened; `pe.py` refuses with a traceback;
`wavcheck.py` lower-cases the filename but not `--ext`; `checkscore.py` skips
bolded rows in silence; `controltat.py` dies with `IndexError` under 199 bytes
and four files here are shorter; `crossall.py` gives `PermissionError` on a
directory; and `mdmd.py` prints two verdict words so `grep -c REFUSED`
under-counts.

**The budget.** The last seven sessions recorded 14,039,770,841 /
1,408,855,740 / 754,254,358 / 482,238,888 / 18,368,483 / 5,378,762 /
**2,235,430** bytes of `_work\`.

---

## §B — the calibration, and why it is still not an offset

Twelve objects of *predicted minus obtained* on the open column:

    +10.5  +7.5  +5.0  +2.0  −14.0  −2.0  +9.0  0.0  +19.75  +5.25  −4.10  −3.40

Mean **+3.35**, range 33.75. **The standing prescription is not to apply a
global offset**, and it is followed here. The eleventh and twelfth entries are
the first same-signed pair after four positives; two points are not a trend and
nothing is subtracted for them.

The label prescription — that `content` clauses score ten to fifteen points
worse than `method` ones — **remains half-withdrawn upstream** and is treated
that way. It reproduced a fourth time yesterday at full size (85.0 % against
66.7 %, an 18.3-point gap) and all nine misses had substantive causes, two of
them on `method` clauses. **The label measures how hard the assertion is, not
how good the intuition was.** Clauses below are labelled by what they are.

**The new prescription, which is the one that cost four clauses yesterday:**

> **When a clause names a mechanism, ask whether a shape would do.** Four
> clauses of nine guessed *that* a format would open and got *how* wrong.

It is applied deliberately below and it is visible: **C22 and C28 claim that
the two families close end to end, and say nothing about what the fields
mean.** The meanings are separate clauses — C23, C24, C25, C30 — at separate
and much lower scores, because they are separate bets and one should not sink
the other.

**And the prescription the collection produced rather than the object:**

> **A census that sweeps one root loses the others, and a denominator that
> does not know what it is counting is wrong inside the right root too.**

Two sessions running corrected the same measurement. This one publishes the
corrected figure **and what it corrects** (C40), and the figure was measured
by command before this line was written rather than copied from `_pre\`.

**One structural warning about this object's shape.** 86.9073 % of it is
executable and the inherited rule counts an executable as unidentified however
much of it is read. **The coverage number is capped by construction and every
open clause that could raise it is capped with it.** So the open column here
is weighted towards *measurements* rather than towards *coverage*, and C38
says outright that the interesting result is not the percentage. If the low
number is the only thing this repository is remembered for, the session was
written badly and not measured badly.

---

## §C — the inherited clauses, which re-test the pre-briefing

Thirteen clauses. Each re-derives a figure `_pre\` handed over, by a command,
against the real bytes. **The pre-briefing says of itself that it should be
treated as `[unverified]` line by line, and §A above has already caught one
arithmetic error in it without opening anything.**

**C01** `method` `inherited` — `tools/hashall.py` over `game\` reproduces
**nine files, 169,530 bytes and nine distinct sha1**, and all nine digests in
`_pre\object.txt` match byte for byte. *Predicted: 0.9*

**C02** `method` `inherited` — all nine mtimes read as the single value
`1996-12-24 23:32:00`, to the second, with **one distinct value over nine
files**. *Predicted: 0.9*

**C03** `method` `inherited` — `tools/mz.py` re-run reproduces all three rows:
header 512 on 3 of 3, images 103,336 / 41,842 / 620, **residue +0 on 3 of 3**,
`e_lfanew` 0 on 3 of 3, and **zero relocations on `popcorn.exe`**.
*Predicted: 0.85*

**C04** `method` `inherited` — `tools/entropy.py` reproduces **6.1130**,
**3.5168** and **3.9324** on the three executables, each within 0.0005.
*Predicted: 0.85*

**C05** `content` `inherited` — the 256-byte census reproduces exactly:
`popcorn.exe` 405 blocks / 405 distinct / **1 constant-byte**, `popgen.exe`
165 / 125 / 39, `popspeed.exe` 4 / 4 / 1. *Predicted: 0.8*

**C06** `method` `inherited` — both `.ppc` open with the six ASCII bytes
`LACRAL`, and 8,630 − 6 = 8,624 = 49 × 176 **exactly, on 2 of 2**, with no
remainder. *Predicted: 0.9*

**C07** `content` `inherited` — the stride scan reproduces its two halves: at
stride 176 `ltf.ppc` agrees above 0.95 and `poptab.ppc` below 0.15, and 175 and
177 on `ltf.ppc` land near 0.5 rather than near 0.98. *Predicted: 0.75*

**C08** `content` `inherited` — `popcorn.hsc` is 180 bytes, entirely printable
ASCII, and reads as ten 18-byte records of a 12-byte name and a 6-digit ASCII
score; **record 0 is `LTF` with `000546` and the other nine are twelve hyphens
and `000000`**. *Predicted: 0.85*

**C09** `content` `inherited` — the `grep -aoc` geometry reproduces exactly:
`LACRAL` in four files at 1 / 1 / 2 / 1, `RAYNAL` twice in `popcorn.doc` and
zero elsewhere, `LACAZE` twice in `popcorn.doc` and zero elsewhere.
*Predicted: 0.85*

**C10** `content` `inherited` — `pop.bat` is exactly `POPCORN %1` in 13 bytes
and `ltf.bat` is exactly `popcorn lltf` in 16 bytes, **with two l's**, and no
file named `lltf.*` exists in the directory. *Predicted: 0.85*

**C11** `method` `inherited` — all eight packer strings — `LZ09`, `LZ91`,
`PKLITE`, `diet`, `EXEPACK`, `RJSX`, `WWPACK`, `TINYPROG` — occur **zero times
each across all nine files**, re-derived case-insensitively as well as
case-sensitively. *Predicted: 0.8*

**C12** `content` `inherited` — the header anomaly reproduces: **blocks 0 and
10 of `poptab.ppc` carry five non-zero leading bytes** where the other
forty-seven carry one, both with `3` in the second position, and block 0 of
`ltf.ppc` carries four. *Predicted: 0.8*

**C13** `method` `inherited` — `ls tools/*.py | wc -l` gives **436** at the
start of the session, and `tools/toolscan.py` returns **0 findings** over the
`.py`, `.md` and `.txt` sets with all three positive controls firing.
*Predicted: 0.85*

---

## §D — the open clauses, which are this session's own work

### The executable that repeats nothing

**C14** `method` `open` — a tool in `tools/` reports block count, distinct
blocks, constant-byte blocks, entropy and relocation count **in one table**,
and is run over this object's three binaries plus every MS-DOS binary reachable
in `pc-linksthechallengeofgolf-doc` and `pc-skunnybacktotheforest-doc`. **The
number of binaries is stated by command and is at least twelve, from three
publishers.** *Predicted: 0.85*

**C15** `content` `open` — on that table `popcorn.exe`'s distinct-over-blocks
ratio is **1.000 and is the only 1.000 in the set**; no other MS-DOS binary
measured reaches it at 256 bytes. *Predicted: 0.75*

**C16** `method` `open` — a windowed entropy scan of `popcorn.exe` at a stated
window size shows **at least two regimes**: some window at or above 7.0 and
some window at or below 5.0. A uniformly packed image would show neither.
*Predicted: 0.6*

**C17** `content` `open` — the 512 printable runs are **not spread evenly**:
the smallest contiguous span of the file that contains 90 % of them is **under
half the image**. *Predicted: 0.55*

**C18** `content` `open` — the session reaches a stated verdict on the packing
question with numbers behind it, and the verdict is that **`popcorn.exe` is not
a whole-image packed executable**; the four indicators are given a common
alternative cause. *Predicted: 0.55*

**C19** `content` `open` — the packer sweep is widened past the eight names to
a stated longer list and **still returns zero on all nine files**.
*Predicted: 0.7*

**C20** `content` `open` — `popcorn.exe` does **not** contain an embedded
8,624-byte `49 × 176` region; its two `LACRAL` occurrences are both string
constants and neither begins a level image. *Predicted: 0.6*

**C21** `content` `open` — `popgen.exe` and `popspeed.exe` behave like ordinary
DOS binaries on all four indicators and are used as **internal controls**, so
the outlier claim about `popcorn.exe` never rests only on external objects.
*Predicted: 0.8*

### The level files

**C22** `method` `open` — a `.ppc` reader written this session validates
**2 of 2 files and 98 of 98 blocks** at residue 0, on the magic and the
49 × 176 arithmetic alone, and it is made to refuse at least one specimen that
must fail before the census is run. *Predicted: 0.85*

**C23** `content` `open` — the `16 × 10` reading **is refuted**, and the
corrected reading changes at least one of {header width, grid width, cell
size}. *Predicted: 0.5*

**C24** `content` `open` — a rule the lead byte satisfies is found, and it
holds on **more than 49 of the 98 blocks**; the number is stated in both
directions, satisfied and violated. *Predicted: 0.45*

**C25** `content` `open` — `ltf.ppc` is a **degenerate** level set: its
forty-nine blocks are near-identical to one another, which is why its stride
agreement is 0.980 and `poptab.ppc`'s is 0.085. *Predicted: 0.6*

**C26** `content` `open` — the two `.ppc` files share **at least one identical
176-byte block**. *Predicted: 0.5*

**C27** `content` `open` — the five-byte anomaly in blocks 0 and 10 of
`poptab.ppc` either gets an explanation or goes to the leftovers chapter with
its count stated as *n* of 98. *Predicted: 0.7*

### The user state, and the three letters in it

**C28** `method` `open` — a `.hsc` reader written this session validates
**180 = 10 × 18** with 10 of 10 records fully printable and residue 0.
*Predicted: 0.9*

**C29** `content` `open` — the owner of this machine answers whether the game
prompts for a name at the high-score screen, and the answer is recorded as
**his observation, attributed to him**, not as this session's measurement.
*Predicted: 0.7*

**C30** `content` `open` — `LTF` turns out to be a **person's initials typed at
a prompt** rather than a level-set label the program writes by itself.
*Predicted: 0.5*

### The names, and the door

**C31** `content` `open` — the missing clause of the criterion is **written as
a rule**, with the case that generated it beside it, and placed where a later
session on a different object will find it — not buried in prose.
*Predicted: 0.85*

**C32** `content` `open` — the decision is **names published, contact details
not**: the surnames and given names of both authors are printed, and the
address, the Minitel number and the two handles are reported as a shape —
*"a postal address in a French town, a Minitel service number and two mailbox
handles"* — with no digits and no street. *Predicted: 0.8*

**C33** `content` `open` — `LACRAL` = `LACaze` + `RAynaL` is **stated nowhere
in the nine files** and is published as an inference labelled as one.
*Predicted: 0.75*

**C34** `method` `open` — the sweep for personal names is done by **enumerating
every printable run of the nine files and reading them**, not by a name regex,
because a check that cannot fail is not a check; and it finds **no personal
name outside `popcorn.doc`**. *Predicted: 0.7*

**C35** `content` `open` — `23016745` is **not a telephone number**, and the
session says on what grounds rather than asserting it; its meaning goes to
leftovers. *Predicted: 0.6*

### The accounting

**C36** `content` `open` — this object is given **one denominator and not
two**, and the decision is argued from the absence of a container rather than
inherited from previous sessions. *Predicted: 0.7*

**C37** `content` `open` — the coverage figure lands at exactly the ceiling,
**22,196 / 169,530 = 13.0927 %**, because every one of the four non-executable
families closes. *Predicted: 0.55*

**C38** `content` `open` — that figure is **the lowest in the series** — below
24.8524 % — and the repository presents it with the rule that caps it, in
chapter 01 and in the README, without apologising for it and without touching
the rule. *Predicted: 0.85*

### Against the collection

**C39** `method` `open` — `tools/crossall.py` run **once per root, seven
times**, reports **zero** shared hashes between these nine files and every
other repository in the collection. *Predicted: 0.85*

**C40** `content` `open` — the denominator re-measures to **242 directories,
122 `*-doc`, 83 with a `notes\`**, and **moves to 84 during the session**
because this repository gains a `notes\`; both the figure and what it corrects
are published. *Predicted: 0.7*

**C41** `method` `open` — re-measured from both objects on this filesystem
today, `pc-linksthechallengeofgolf-doc`'s thirty-two files give a single mtime
of `1996-12-24 22:32:00` and this object's nine give `1996-12-24 23:32:00`,
**a difference of exactly 3,600 seconds**. *Predicted: 0.85*

**C42** `content` `open` — **both readings of that hour are written, the
alternative before the conclusion**, and the session declines to choose between
"archived an hour apart" and "archived together and recorded an hour apart".
*Predicted: 0.8*

**C43** `content` `open` — the MS-DOS platform checklist is **decided in this
session and not deferred again**: two of the four recurring items hold on this
third specimen, and the decision is not to create the checklist.
*Predicted: 0.7*

### The manual, and the two models of distribution

**C44** `method` `open` — `popcorn.doc` is **121 lines** of code-page-437 text,
and its own file manifest names **six** files against the nine present.
*Predicted: 0.8*

**C45** `content` `open` — the object's distribution model is written from the
manual itself: the *"domaine public"* sentence and the *"COMMENT DONNER CE JEU
A VOS AMIS ?"* paragraph are both present and both quoted, and the chapter sets
them against the previous object's twenty pages of distributors.
*Predicted: 0.8*

**C46** `content` `open` — the `SPEED` / `POPSPEED.EXE` rename fossil
reproduces in **three places**, and **how the utility passes its value stays
unresolved** and is written as unresolved. *Predicted: 0.75*

**C47** `content` `open` — `lltf` is **not settled** in this session, because
settling it needs a disassembly of the argument parser and the strings do not
carry it; it goes to leftovers with that reason. *Predicted: 0.55*

### The tools

**C48** `method` `open` — the nine Copysoft readers written last session are
run as free negative controls and **refuse everything they are given**, and
`sbank.py` in particular is fed a `.ppc` block and refuses it — a measurement
in both directions, on the record. *Predicted: 0.8*

**C49** `method` `open` — `tools/gamedata.py --hi` **refuses `popcorn.hsc`** on
its 26-byte record arithmetic against this file's 18-byte records, and the
refusal is recorded before any new reader is written. *Predicted: 0.75*

**C50** `method` `open` — `tools/protscan.py --all-files` reports **zero
markers over the nine files**, and its `MARKERS` table re-derives as **12
rows**: eleven schemes and one positive control. *Predicted: 0.85*

**C51** `method` `open` — **at least one new defect in an inherited tool** is
found and written down, taking the standing list from six to seven or more.
*Predicted: 0.7*

**C52** `method` `open` — `tools/account.py` is **rewritten a second session
running**, for an object with no archive, and its output is the coverage table
that chapter 01 prints. *Predicted: 0.85*

**C53** `method` `open` — the tool count at the end is **above 436**, stated by
command, and every new tool refuses a specimen that must fail before it
censuses anything. *Predicted: 0.85*

**C54** `method` `open` — `tools/toolscan.py` over `.py`, `.md` and `.txt`
returns **0 findings with all three positive controls firing**, run **twice** —
once at the halfway point and once at the end, without being asked.
*Predicted: 0.85*

### The hygiene

**C55** `method` `open` — the nine sha1 re-derive **identical at the end of the
session**: no byte of the object was modified, and the comparison is made
against the digests recorded at the start rather than against `_pre\`.
*Predicted: 0.95*

**C56** `method` `open` — `git ls-files | grep -Eiv "^(README|docs/|notes/|tools/|\.gitignore)"`
is **empty**, and a positive control constructed to match **fires**.
*Predicted: 0.9*

**C57** `content` `open` — `_work\` is measured before deletion and is **a new
smallest, under 2,235,430 bytes**. *Predicted: 0.7*

**C58** `content` `open` — the repository ships **fewer than fifteen
documents**, because nine files and 169 KB do not support fifteen chapters, and
no two chapters are merged merely to make a target. *Predicted: 0.7*

**C59** `content` `open` — **at least one correction is produced for a
neighbour repository** — most likely `pc-linksthechallengeofgolf-doc` on the
Christmas Eve mtime — and it is handed over as text with a stated destination,
**without editing that repository**. *Predicted: 0.7*

**C60** `content` `open` — **nothing is rendered.** No CGA image is recovered
from `popcorn.exe` this session, and the object's pictures stay behind the
executable rule. *Predicted: 0.5*

---

## What this document is betting

Three bets are worth naming so that scoring can find them.

**The first is that the packing question is answerable without a
disassembler**, by windowed entropy and a cross-publisher histogram rather than
by finding a signature that eight searches have already failed to find. C16,
C17 and C18 stand or fall together and they total 1.70.

**The second is that `.ppc` closes as a container and does not close as a
grid.** C22 at 0.85 and C23, C24 at 0.5 and 0.45 are deliberately far apart,
because yesterday four clauses died of guessing *how* after correctly guessing
*that*.

**The third is that the low coverage number is the easy part and the clause in
C31 is the hard part.** A repository that prints 13.0927 % and does not write
the rule has done the arithmetic and skipped the session.

Every clause above carries `method` or `content` and `inherited` or `open`, and
the two totals are never added together.
