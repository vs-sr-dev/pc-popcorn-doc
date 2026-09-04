# 14 — prediction scoring: 9.775 of 13 inherited, 24.50 of 47 open

*Measure: 60 clauses written before any byte of the object was opened. **41
hits, 7 halves, 10 misses, 2 unresolved.** Inherited **9.775 of 13** against
10.95 predicted; open **24.50 of 47** against 33.80 predicted. The two totals
are never added together.*

Counted with `python tools/checkscore.py`. Verdicts and tags are not bolded, so
the tool sees them; fractional scores are in the third column, which is the
convention the previous session established.

## §C — the inherited clauses

| tag | verdict | score | predicted | what happened |
| --- | --- | --- | --- | --- |
| C01 | hit | 0.90 | 0.90 | 9 files, 169,530 bytes, 9 distinct sha1; all nine digests match `_pre\` |
| C02 | hit | 0.90 | 0.90 | one distinct mtime over nine files, `1996-12-24 23:32:00` |
| C03 | hit | 0.85 | 0.85 | all three MZ rows reproduce, residue +0 on 3 of 3, `e_lfanew` 0, zero relocations |
| C04 | hit | 0.85 | 0.85 | 6.1130 / 3.5168 / 3.9324 exactly |
| C05 | hit | 0.80 | 0.80 | 405/405/1, 165/125/39, 4/4/1 |
| C06 | hit | 0.90 | 0.90 | `LACRAL` + 8,624 = 49 × 176 on 2 of 2, no remainder |
| C07 | half | 0.375 | 0.75 | the two halves reproduce in direction and not in value — see below |
| C08 | hit | 0.85 | 0.85 | 180 bytes, all printable, 10 × 18, record 0 `LTF` / `000546` |
| C09 | hit | 0.85 | 0.85 | `LACRAL` 1/1/2/1 in four files; `RAYNAL` and `LACAZE` 2 each in `popcorn.doc` |
| C10 | hit | 0.85 | 0.85 | `POPCORN %1` in 13 bytes, `popcorn lltf` in 16, two Ls, no `lltf.*` present |
| C11 | hit | 0.80 | 0.80 | all eight packer names 0 occurrences, case-sensitive and case-insensitive |
| C12 | miss | 0.00 | 0.80 | the anomaly is not two blocks of forty-nine — see below |
| C13 | hit | 0.85 | 0.85 | 436 `.py` at the start; `toolscan.py` 0 findings, all three controls fire |
| — | — | **9.775** | **10.95** | inherited: **9.775 obtained** against 10.95 predicted, out of a maximum of 13 |

**C07.** The stride scan reproduces its shape and not its numbers. `ltf.ppc`
agrees **0.987** at 176 — above the 0.95 the clause claimed — but `poptab.ppc`
gives **0.321** where the clause said below 0.15 and the pre-briefing said
0.085, and 175 and 177 on `ltf.ppc` give **0.686** where both said about 0.5.
The qualitative claim — one file periodic, the other not, with the neighbours
of 176 clearly lower — holds on every value. The quantities do not, in the
pre-briefing's figures or in the clause that re-asserted them, and neither
document says how the agreement was normalised. **Half.**

**C12, and it is the session's most useful miss.** `_pre\formats.txt` states
that *"Blocks 0 and 10 of `poptab.ppc` carry five non-zero leading bytes where
every other block carries one"*, and C12 re-asserted it. Counted:
**seventeen of `poptab.ppc`'s forty-nine blocks carry more than one non-zero
header byte**, with four, five, six, seven and eight of them, and the reason is
chapter 06's: the header's second byte is a count of type-9 cells and the next
six are their positions, so every block with a type-9 cell has a populated
header. The pre-briefing looked at two blocks and generalised to forty-nine;
this clause repeated the generalisation without counting. **Re-derive the count
counting** is rule 6, and this is what it is for.

## §D — the open clauses

| tag | verdict | score | predicted | what happened |
| --- | --- | --- | --- | --- |
| C14 | hit | 0.85 | 0.85 | `dosimage.py` over 13 binaries from 3 publishers, count by command |
| C15 | miss | 0.00 | 0.75 | **4 of 13 reach d/b 1.000**, not one — see below |
| C16 | half | 0.30 | 0.60 | two regimes exist (min 2.73, max 6.82) but the stated 7.0 threshold is not met |
| C17 | miss | 0.00 | 0.55 | the smallest span holding 90 % of the runs is **62.0 %** of the image, not under half |
| C18 | miss | 0.00 | 0.55 | it **is** a whole-image packed executable |
| C19 | miss | 0.00 | 0.70 | the widened sweep returned **two** markers, which is the finding |
| C20 | miss | 0.00 | 0.60 | it contains **fifty** 176-byte blocks and the second `LACRAL` is their header |
| C21 | half | 0.40 | 0.80 | `popgen.exe` is ordinary on all four; `popspeed.exe` on three of four |
| C22 | hit | 0.85 | 0.85 | 2 of 2 files, 98 of 98 blocks, residue +0, refusal control run first |
| C23 | hit | 0.50 | 0.50 | 16 × 10 refuted; both the header width and the grid width changed |
| C24 | hit | 0.45 | 0.45 | the lead-byte rule holds on **98 of 98**, not the 50-of-98 the clause required |
| C25 | hit | 0.60 | 0.60 | `ltf.ppc` is 48 identical copies of one block plus its own block 0 |
| C26 | hit | 0.50 | 0.50 | the two files share exactly one block |
| C27 | hit | 0.70 | 0.70 | explained: it is the `n9` count and its position slots |
| C28 | hit | 0.90 | 0.90 | 180 = 10 × 18, 10 of 10 printable, residue +0 |
| C29 | unresolved | 0.00 | 0.70 | he ran the game and confirmed the screen shows `LTF` / 546 — which verifies the reader and not the prompt |
| C30 | unresolved | 0.00 | 0.50 | depends on C29; seeing a name displayed is not seeing it typed |
| C31 | hit | 0.85 | 0.85 | the clause is written as a rule with two corollaries and its generating case |
| C32 | hit | 0.80 | 0.80 | names printed; address and number reported as a shape, no digits, no town |
| C33 | hit | 0.75 | 0.75 | `LACRAL` = LACaze + RAynaL is nowhere in the object; published as an inference |
| C34 | miss | 0.00 | 0.70 | see below — the method was right and the conclusion was false |
| C35 | half | 0.30 | 0.60 | not a telephone number, on stated grounds — but it did not go to leftovers, it closed |
| C36 | hit | 0.70 | 0.70 | one denominator, argued from the absence of a container |
| C37 | hit | 0.55 | 0.55 | 22,196 / 169,530 = 13.0927 %, exactly the ceiling |
| C38 | hit | 0.85 | 0.85 | lowest in the series by eleven points, presented with the rule that caps it |
| C39 | hit | 0.85 | 0.85 | seven roots, 82 repositories, 128,756 tokens, 0 crossings |
| C40 | half | 0.35 | 0.70 | 122 and 83 → 84 correct; the directory count moved to 243, not 242 |
| C41 | hit | 0.85 | 0.85 | 32 at 22:32:00 and 9 at 23:32:00, exactly 3,600 seconds |
| C42 | hit | 0.80 | 0.80 | both readings written, alternative first, no choice made |
| C43 | miss | 0.00 | 0.70 | the decision went the other way: four of four hold and the checklist is adopted |
| C44 | hit | 0.80 | 0.80 | 121 CRLF lines, manifest of six against nine |
| C45 | hit | 0.80 | 0.80 | both passages present and quoted; chapter 03 |
| C46 | half | 0.375 | 0.75 | the fossil reproduces in three places; the value-passing **resolved** |
| C47 | hit | 0.55 | 0.55 | `lltf` unsettled, and for exactly the stated reason: no `.PPC` string to read |
| C48 | hit | 0.80 | 0.80 | nine readers refuse; `sbank.py` refuses a single 176-byte block |
| C49 | hit | 0.75 | 0.75 | refused on the 26-byte arithmetic, before anything new was written |
| C50 | hit | 0.85 | 0.85 | eleven schemes at zero, positive control on 5 of 9 files, `MARKERS` 12 rows |
| C51 | hit | 0.70 | 0.70 | two new defects, both in `crossall.py`; the list goes from six to eight |
| C52 | hit | 0.85 | 0.85 | rewritten for a no-archive object; its output is chapter 01's table |
| C53 | half | 0.425 | 0.85 | 443 by command — but `cga.py` has no refusal control, because it identified nothing |
| C54 | hit | 0.85 | 0.85 | twice, 0 findings, three controls each time |
| C55 | hit | 0.95 | 0.95 | nine sha1 identical at the end against the digests taken at the start |
| C56 | hit | 0.90 | 0.90 | empty, with a positive control that fires |
| C57 | miss | 0.00 | 0.70 | `_work\` is **3,566,054** bytes — see below |
| C58 | miss | 0.00 | 0.70 | fifteen documents, and fifteen is not fewer than fifteen |
| C59 | hit | 0.70 | 0.70 | three corrections produced for `pc-linksthechallengeofgolf-doc`, none applied |
| C60 | hit | 0.50 | 0.50 | nothing rendered; the CGA data is located and not decoded |
| — | — | **24.500** | **33.80** | open: **24.50 obtained** against 33.80 predicted, out of a maximum of 47 |

## The six misses that matter

**C15, C18, C19 and C20 are one miss with four heads, and it is the session's
main result.** Every one of them bet that `popcorn.exe` was *not* a packed
image, on the strength of two arguments: 512 legible French strings, and an
entropy of 6.11 that is low for an LZ packer. Both arguments were wrong for the
same reason. **EXEPACK compresses runs and not phrases**, so it leaves text
verbatim and lands near 6 bits rather than near 8. The two things that looked
like evidence against packing were symptoms of the packer.

C15 is the most instructive of the four, because being wrong is what made the
measurement worth making. The clause said `popcorn.exe`'s d/b of 1.000 would be
unique among thirteen binaries. **Four reach it**, and the four sort themselves
by two other columns without being asked: every 1.000 in the table has zero
relocations in its MZ header and an entry point within 900 bytes of EOF, and
nothing else does. A unique outlier would have been an anecdote. A cluster of
four, one of which is a confirmed LZEXE image identified by another session, is
a test — and it is what made `exepack.py` worth writing and found four more
packed images in a neighbour's object.

**C34 is the miss to keep.** It said the sweep for personal names would be done
by enumerating every printable run rather than by a regex — the right method,
and the previous session's lesson — and that it would find no personal name
outside `popcorn.doc`. **The method was right and would still have found
nothing**, because both surnames inside `popcorn.exe` are EXEPACK'd and then
XORed with 0xAA, and no printable-run scanner reaches them. Enumeration is
better than a regex and neither is enough. **The lesson generalises: a complete
sweep of the readable bytes is still a sweep of the readable bytes.**

**C43** predicted the MS-DOS checklist would be declined on two of four items.
Both failing items held once their wording was repaired — "identify the
toolchain" rather than "find a compiler string", "third-party code" rather than
"a third-party file" — and the checklist is adopted with five items in
chapter 10. Wrong prediction, and the reasoning that made it wrong is written
down where the next MS-DOS object will find it.

**C57 is a miss this session chose.** `_work\` is 3,566,054 bytes, above the
2,235,430 that would have made it a new smallest. **3,236,310 of that is WAV**,
rendered because the owner of this machine asked to hear the sound. Without the
audio it would be **329,744 bytes** and a new smallest by a factor of seven.
The clause is scored as written and the reason is on the record.

**C58 is a miss taken deliberately.** Fifteen documents. Two could have been
merged to make the count — the sound chapter into the program chapter, or the
manual into the object — and neither merge would have been honest. The previous
session set the precedent: leave the clause at zero rather than reshape the
repository around it.

## The three predictions worth having made

**C24 at 0.45.** The lowest-scored clause in the document, written low
deliberately because the previous session lost four clauses to guessing *how*
after correctly guessing *that*. It asked only that some rule be found holding
on more than half the blocks. The rule holds on **98 of 98**. Pricing a hard
bet honestly is not the same as making a timid one.

**C22 and C23 held apart on purpose**, at 0.85 and 0.50. The container closed
and the geometry was refuted, exactly as the split expected, and neither
outcome contaminated the other's score.

**C31 at 0.85** was the clause the document called the hard part, and it is the
one the session would keep if it could keep one.

## The calibration, and a correction to the series itself

*Predicted minus obtained*, on the open column, thirteen objects:

    +10.5  +7.5  +5.0  +2.0  −14.0  −2.0  +9.0  0.0  +19.75  +5.25  −4.10  −3.40  **+9.30**

**The published mean of the first twelve is wrong.** The brief for this session
states *"media +3,35"*. Those twelve sum to **35.50** and 35.50 / 12 =
**+2.958**. With this object's +9.30 the thirteen sum to 44.80, mean **+3.446**.
Both figures are re-derived here by addition rather than carried forward.

**The standing prescription — do not apply a global offset — was followed and
this object is the argument for it.** The two preceding entries were negative
and of similar size, and a session that had "corrected" for them by scoring
higher would have been wrong by more than nine points instead of nine. The
range is now 33.75 points across thirteen objects and the mean is smaller than
the spread of any three consecutive entries. **There is nothing in this series
to offset against.**

## The label effect, a fifth time, and larger

| label | obtained | predicted | share |
| --- | --- | --- | --- |
| open `method`, 17 clauses | 12.475 | 13.90 | **89.7 %** |
| open `content`, 30 clauses | 12.025 | 19.90 | **60.4 %** |

**A gap of 29.3 points, the largest yet**, against 18.3 last session and about
15 before that. And the caveat stands unchanged, because it is visible in the
table above: the two `method` clauses that fell short — C16 on a threshold and
C53 on a tool that identified nothing — cost 0.775 points between them, while
the `content` column lost 9.30 points on **four clauses that made a single
substantive bet about what `popcorn.exe` was**, and got it wrong for a reason
this repository now documents in a chapter.

**The label measures how hard the assertion is, not how good the intuition
was**, and the prescription stays half-withdrawn. A session that wrote fewer
`content` clauses here would have scored better and found less: C18 is a zero,
and chasing it produced chapters 04, 05, 06 and 08.
