# 12 — corrections: nine, of which four are the pre-briefing's and three are this session's own

*Measure: every claim corrected here was published somewhere before this
session and is wrong. Four came from `_pre\`, two from the previous
repository, three from this session's own working.*

## From the pre-briefing

**1. `86.2 %` and `about 13.8 %` are both wrong, and they were arithmetic.**
`_pre\neighbours.txt` states *"86.2 % of the object is three executables"* and
*"the coverage figure here is capped at about 13.8 %"*.
`103,848 + 42,354 + 1,132 = 147,334`, and `147,334 / 169,530 = 86.9073 %`, so
the ceiling is **13.0927 %**. Caught before any file of the object was opened,
declared in `docs/00-predictions.md` §A, and it set the target for clause C37.

**2. The `.ppc` block is not a 16-byte header and a 16 × 10 grid.** It is an
**8-byte header and a 12 × 14 grid**, and at that geometry the lead byte agrees
with the grid on 98 of 98 blocks instead of 1 of 3. The pre-briefing said so
itself — *"the 16 × 10 is a hypothesis with one confirmation and two
refutations"* — and it was right to doubt it. See chapter 06.

**3. The five leading non-zero bytes in blocks 0 and 10 of `poptab.ppc` are not
an anomaly.** They are the header's `n9` count and its position slots doing
their job: those two blocks have three type-9 cells each, so bytes 1 through 4
are used and the rest are zero. The `3` in the second position of both, which
the pre-briefing noticed and could not explain, is the count. The real anomaly
is elsewhere and is one block, not two: **block 14 carries stale bytes in slots
its own count says are unused.**

**4. `popcorn.hsc/` has no trailing slash.** `_pre\executable.txt` reads
*"`popcorn.hsc/` appears with a trailing slash, which is what a filename built
by string concatenation against a path separator looks like."* Unpack the file
and the string is `popcorn.hsc\0`. The `/` is a byte of the EXEPACK command
stream sitting against the end of a literal run. **It is a reasonable inference
from a compressed file and it is an inference about a compression artefact.**

## From the previous repository

**5. `title.exe`, `xmm.exe`, `setblast.exe` and `uninstal.exe` of
`pc-linksthechallengeofgolf-doc` are Microsoft EXEPACK images.** Its
`docs/13-leftovers.md` records the first as *"compressed, by an unidentified
packer"* and the other three as *"their code is not [read]"*. The full text of
the correction is in chapter 10 and **that repository has not been edited.**

**6. The same document contains the trap that cost this session ninety
minutes**: *"No `LZEXE`, `PKLITE` or `EXEPACK` signature was searched for by
name and none announced itself."* `EXEPACK` is the name of Microsoft's tool. It
appears in the tool. **A search for it can only return zero**, and this
pre-briefing repeated the search and reported the zero. See chapter 04.

## This session's own

**7. The privacy geometry was wrong, in the direction that costs this
repository something.** `_pre\formats.txt` measured *"the studio name is in
four files and the two personal names are in one"* and the whole privacy
argument was built on that asymmetry. Both surnames are **also inside
`popcorn.exe`**, once each, invisible to `grep` because they are EXEPACK'd and
then XORed with 0xAA. **The names are in two files and the telephone number is
in two files.** Chapter 09 is written on the corrected geometry.

**8. `tools/popmsg.py`'s character class was wrong twice, in opposite
directions**, and both drafts produced a plausible-looking region:

* accepting anything decoding to `0x20` or above admits `0x00`, because
  `0x00 ^ 0xAA` is `0xAA`, a printable CP437 character. The message grew from
  2,418 bytes to **5,203** by eating the zero padding on both sides;
* stopping at `0x8F` cut it off after **746** bytes, at the *ù* of *"où les
  nuits"*.

Both are in the tool's docstring, because the range that survived — ASCII plus
`0x80..0x97` — looks arbitrary until you know it has to exclude `0xAA` at one
end and the token's digits at the other.

**9. `tools/dosimage.py` printed `resid -512` on three files `mz.py` reports at
`+0`.** `e_cp`/`e_cblp` declare the size of the whole file including the header,
not the size of the load image, and the first draft subtracted the header
twice. **It was caught by disagreeing with a tool that had already been right
three times**, which is the argument for keeping the old tool's output beside
the new tool's.

## The prescriptions this session leaves

**On signature searches — the new one, and it generalises past packers:**

> **Search for what the producer writes, never for what the producer is
> called.** A tool's name lives in the tool. `EXEPACK` appears in no EXEPACK'd
> file; `RB` at `entry − 2` and `Packed file is corrupt` appear in all of them.
> A search that can only return zero is not a search, and its zero is not
> evidence. This is the fourth session in a row bitten by a control that could
> not fire.

**On position versus presence, which is the other half of the same coin:**

> **A short marker is a claim about a position, not about a file.** `RB` occurs
> once in `golf.exe` too, and `golf.exe` is not an EXEPACK image. What
> identifies is that the marker sits where the format says it sits and that a
> length field derived from that position closes on the file.

**On denominators, restated because it has now been corrected twice running:**

> **A census that sweeps one root loses the others, and a denominator that does
> not know what it is counting is wrong inside the right root too.** The figure
> is 122 documentation repositories on two roots, 84 with a `notes\`. Publish
> what it corrects, not only what it is.

**On the label prescription, which is withdrawn no further:** it reproduced a
fifth time here — see chapter 14 — and the same caveat applies. **The label
measures how hard the assertion is, not how good the intuition was.**

**And the one this session would give itself:**

> **When four independent indicators all point one way and no signature is
> found, the signature search is the thing to doubt, not the indicators.** Four
> measurements agreeing is a strong prior. Eight names returning zero is a weak
> refutation, and it was treated as the stronger of the two for ninety minutes.
