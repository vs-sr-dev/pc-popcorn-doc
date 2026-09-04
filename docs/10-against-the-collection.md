# 10 — against the collection: zero over seven roots, one hour, and a checklist that is now due

*Measure: **0 of 9 hashes** cross with any other repository, over **seven roots,
82 repositories with hash records, 359 list files and 128,756 hash tokens**. The
collection denominator re-measures to **243 directories, 122 `*-doc`, 84 with a
`notes\`** — and 84 rather than 83 because this repository is one of them.*

## The hash crossing, and its denominator published first

`tools/crossall.py` takes a hash listing and a collection root. It was run seven
times, once per root, with the listing at `notes/hashes.txt`.

| root | repositories with hash records | crossings |
| --- | --- | --- |
| 1 | 0 | 0 |
| 2 | 0 | 0 |
| 3 | 1 | 0 |
| 4 | 0 | 0 |
| 5 | 0 | 0 |
| 6 | 0 | 0 |
| 7 | **82** | 0 |

**359 list files swept, 128,756 hash tokens read, 0 of my 9 distinct sha1 found
anywhere.** The empty-file sha1 trap fired as designed and is reported
separately: 32 occurrences in 12 repositories, excluded from the crossings.

The expected answer was zero and it is zero. A French public-domain game from
1988 shares no byte with anything else on this machine, which is exactly what
should happen and is worth one line rather than a chapter.

**The tool's own self-skip is a trap and it caught this session.** Its docstring
says *"The repository being measured is skipped"*; in the code `--skip` defaults
to the empty string, so the first run over root 7 reported nine crossings, every
one of them this repository's own `notes/hashes.txt` matching itself. The only
warning is a line reading `skipping : (nothing)`. That is a new inherited-tool
defect and it is in chapter 11.

## The denominator, corrected for the second session running

Every session from the forty-eighth to the fifty-third published a figure
between 112 and 115 for "the collection". Measured by command at the start of
this session and again at the end:

| root | directories | `*-doc` | with a `notes\` |
| --- | --- | --- | --- |
| 1 | 6 | 0 | 0 |
| 2 | 6 | 0 | 0 |
| 3 | 4 | 0 | 0 |
| 4 | 4 | 0 | 0 |
| 5 | 34 | 0 | 0 |
| 6 | **74** | **11** | 2 |
| 7 | 115 | **111** | **82** |
| **TOTAL** | **243** | **122** | **84** |

**The published figure was wrong twice over**: it counted four directories in
root 7 that are not documentation repositories, and it missed eleven in root 6
that are. Roots 1 to 5 hold homebrew development projects and contain no `-doc`
repository at all.

The correct figure is **122 documentation repositories on two roots, of which
84 have a `notes\`.** Six repositories carry the old number in their
`docs/10`; the correction is published here rather than quietly applied there.

Two sessions running have now corrected the same measurement — the previous one
found the second root, this one finds that the count inside the roots was also
wrong — and **the common cause is that nobody had ever asked what the
denominator was supposed to be counting.** The prescription that follows is in
chapter 12.

The population moved during this session, as it has during each of the last
four: root 6 gained a directory between the first measurement and the last, and
`notes\` went from 83 to 84 because **this repository created one**. Both
figures above are the closing measurement.

## The Christmas Eve, which has two readings and only one conclusion

Re-derived today, from both objects, on the same filesystem with the same
command:

    python -c "...Counter(mtime for each file)..."
    pc-popcorn-doc/game                     : {'1996-12-24T23:32:00': 9}
    pc-linksthechallengeofgolf-doc/...      : {'1996-12-24T22:32:00': 32}

**Nine files at 23:32:00 and thirty-two files at 22:32:00, on the same
Christmas Eve, to the second, exactly 3,600 seconds apart.** Two different games
by two different publishers, six and eight years after their own internal dates.
`pc-linksthechallengeofgolf-doc/docs/01-the-object.md` line 68 records its
figure independently and this session did not take it from there; it re-measured
the neighbour's object directly.

**The alternative, stated before the conclusion.** One hour is also exactly the
size of a timezone or daylight-saving reinterpretation of a FAT timestamp. Both
directories are read from the same filesystem by the same tool today, so any
systematic offset applied at *read* time would apply equally to both and cancel.
But whether the two sets of files were *written* under the same interpretation
— whether one came off a FAT volume and the other off an archive that stored
local time, or through two different tools on the same evening — is not knowable
from here.

**So there are two readings and this session declines to choose:**

1. **archived an hour apart**: somebody sat at a machine on 24 December 1996
   and copied two games off two floppies, an hour between them;
2. **archived together and recorded an hour apart**: one pass, two files' worth
   of timestamp interpretation, and the hour is an artefact of the copy.

Either way it is a fact about the **collector**, not about either product, and
this collection has never been able to state one before. It is also the reason
the mtimes are worth writing down even when they are destroyed: nine identical
timestamps say nothing on their own, and say something the moment there is a
second object to put them beside. **A single-value mtime is not noise; it is a
one-bit measurement waiting for a neighbour.**

## The MS-DOS checklist, which is decided here and not deferred again

`pc-skunnybacktotheforest-doc/docs/10-against-the-collection.md` declined to
create a checklist on a sample of two, wrote down four recurring items, and
said: *"The four items are written down here so that a third MS-DOS object can
decide whether they are a pattern."*

**This is the third MS-DOS object. The decision is to adopt the checklist, and
to reword two of the four, because both of those two failed on this object as
written and held once the question was asked properly.**

| # | as written | on this object |
| --- | --- | --- |
| 1 | MZ header arithmetic with the residue printed rather than assumed | **holds.** +0 on 3 of 3 |
| 2 | a compiler identification | **failed as written** — no compiler string in any of the three |
| 3 | a conventional-memory or hardware claim in the shipped documentation | **holds**, richly: CGA only, 8086 at 8 MHz, Microsoft mouse |
| 4 | a third-party component shipped inside the game directory | **failed as written** — there is no separate third-party file |

Item 2 failed because it looked for a *string*. The object states its own
toolchain in prose — *"écrit entièrement en ASSEMBLEUR"* — and that is a better
answer than a Borland copyright line, because it also explains the single
segment and the 35 relocations. **The question is "identify the toolchain", and
a compiler string is one way to answer it.**

Item 4 failed because it looked for a *file*. `popcorn.exe` contains Microsoft
EXEPACK's unpacker stub, error string and relocation table — 376 bytes of
somebody else's code, linked into the binary rather than shipped beside it.
**The question is "is there third-party code in here", and a separate file is
one way for the answer to be yes.** On that reading this is the third object in
a row whose most precisely identifiable component belongs to a third party:
Access Software's, then Mystic Software's WORX toolkit and LZEXE, now Microsoft
EXEPACK.

**The checklist, adopted, five items:**

1. **MZ arithmetic, with the residue printed.** `e_cp`/`e_cblp` against the file
   length. `+0` means nothing is appended; anything else is a chapter.
   `tools/mz.py`, `tools/dosimage.py`.
2. **Identify the toolchain, by any route.** A compiler copyright string is the
   cheap route and it is not the only one; its absence is itself a finding and
   points at hand-written assembler.
3. **Is the image packed, and by what — tested by position, not by name.**
   `tools/dosimage.py` for the four indicators (block census with the
   constant-byte blocks separated, entropy, relocation count, entry-point
   distance from EOF); then a signature test that checks *where* a marker sits.
   **Never search for the packer's own name.** See chapter 04.
4. **The hardware and memory claims in the shipped documentation**, quoted from
   the document rather than inferred from the binary.
5. **Third-party code, whether it is a file or a stub inside one.**

Item 3 is this object's addition and it is the one that would have saved this
session ninety minutes.

## Two corrections owed to a neighbour, produced and not applied

Both belong to `pc-linksthechallengeofgolf-doc`. **This session has not edited
that repository.** The text is here for its owner to apply or reject.

> **For `docs/13-leftovers.md`.** The entry reading *"`golf.exe` … and
> `title.exe` …: compressed, by an unidentified packer. No `LZEXE`, `PKLITE` or
> `EXEPACK` signature was searched for by name and none announced itself"*
> should be split. **`title.exe`, `xmm.exe`, `setblast.exe` and `uninstal.exe`
> are Microsoft EXEPACK images** — four of the six executables. Each carries the
> two bytes `RB` at `entry − 2` and a 16-byte header whose `exepack_size` closes
> exactly on the file length, and `tools/exepack.py` unpacks them to 29,504,
> 2,592, 2,448 and 1,280 bytes. `golf.exe` and `systype.exe` are not EXEPACK and
> remain unidentified.
>
> And the sentence itself contains the trap: **searching for the string
> `EXEPACK` can only ever return zero**, because it is the name of Microsoft's
> tool and appears in the tool, not in its output.

> **For `docs/07-the-programs.md`.** The claim *"Zero of 285 member names occur
> in any of the six executables … It does not contain them in the clear, because
> it is packed"* is now testable on four of the six rather than assumed on all
> six, because those four can be unpacked. The conclusion may well survive —
> `golf.exe`, the one most likely to hold the names, is not among them — but the
> reasoning currently rests on an untested premise and one command would settle
> it.

> **For `docs/01-the-object.md`.** The `1996-12-24 22:32:00` on its
> thirty-two files now has a partner: `pc-popcorn-doc` records
> `1996-12-24 23:32:00` on all nine of its files. Exactly one hour, same
> evening, two publishers. Both readings are set out above and neither
> repository should assert the first without the second.

The standing correction that repository already had — on the PWM speaker,
produced by the previous session and not applied — is unaffected by anything
here and is still owed.

## One cross-reference, which is not a correction

`pc-wackywheels-doc/docs/09-skunny-kart.md` records six `.HSC` files as AdLib
tracker music. `popcorn.hsc` is a high-score table and its manual says so.
**Both are right.** Chapter 07 documents the collision from this side; that
repository needs no change, and the pair is the collection's cleanest
demonstration that an extension is not a format.
