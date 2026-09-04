# 04 — the program: four indicators, eight failed searches, and a two-byte signature

*Measure: `popcorn.exe` is a Microsoft EXEPACK image. Its container parses to
residue **+0 in both directions** — 16 + 236 + 22 + 102 = 376 bytes of tail, and
a decompression that reads all 102,960 packed bytes and writes all 133,296
destination bytes with nothing left over at either end.*

## The question, as it was handed over

The pre-briefing put four measurements on the table and refused to conclude:

| indicator | `popcorn.exe` | `popgen.exe` | what it is usually taken to mean |
| --- | --- | --- | --- |
| 256-byte blocks / distinct / constant | 405 / **405** / 1 | 165 / 125 / 39 | nothing repeats: packed |
| entropy | **6.1130** | 3.5168 | high: packed |
| relocations in the MZ header | **0** | 1 | none: packed |
| entry point, distance from EOF | **360** | 41,714 | a stub at the end: packed |

All four reproduce exactly. And against them:

* `LZ09`, `LZ91`, `PKLITE`, `diet`, `EXEPACK`, `RJSX`, `WWPACK`, `TINYPROG` —
  **zero occurrences each, in all nine files**, case-sensitive and
  case-insensitive;
* **512 printable runs of five or more characters**, in French, which the
  pre-briefing recorded as evidence *against* a packed image.

## The search that could not fire

**Seven of those eight names are strings a packed file really does contain.
The eighth is the name of a tool.**

`EXEPACK` is what Microsoft called the program. It appears in the program. It
does not appear in the program's output, and no version of it ever wrote its
own name into a file it produced. Searching for it can only return zero, and
the zero means nothing at all.

What an EXEPACK'd image does contain is:

* the two bytes `RB` — `0x4252` — as the last field of a header that sits
  **immediately before the entry point**, so at `entry - 2`;
* the error string **`Packed file is corrupt`**, in the clear.

Both are in `popcorn.exe`. Neither was searched for.

    python -c "d=open('game/popcorn.exe','rb').read(); print(d.count(b'Packed file is corrupt'), d[103486:103488])"
    1 b'RB'

**`RB` on its own proves nothing** — two bytes turn up by chance in 100 KB, and
`golf.exe` next door contains `RB` once and is not an EXEPACK image. The claim
is about the position and about the arithmetic that follows from it, and
`tools/exepack.py` refuses on either.

This is the fourth session in a row to be bitten by the same shape of error.
The previous object's was *"0 of 433 identifiers are personal names"* from a
filter that discarded every all-caps identifier. **A control that cannot fail
is not a control**, and the specific variant here is new and worth naming: *a
signature search that looks for the producer's name rather than for what the
producer writes.*

## The container, parsed

    python tools/exepack.py game/popcorn.exe

    file bytes                 : 103848
    MZ header / declared / res : 512 / 103848 / +0
    relocations in MZ header   : 0
    entry point                : 1923:0010 = file offset 103488 (360 from EOF)
    EXEPACK header             : 16 bytes at 103472, signature 'RB' at 103486
    exepack_size               : 376, and 103848 - 103472 = 376  -- closes
    original CS:IP  SS:SP      : 1AC2:0113  1AA2:0200
    dest_len                   : 8331 paragraphs = 133296 bytes
    packed region              : [512, 103472) = 102960 bytes
    compression ratio          : 1.2946  (unpacked over packed)
    'Packed file is corrupt'   : 1 occurrence(s), at 103724
    unpacker stub              : 236 bytes
    packer relocation table    : 35 entries in groups 0x1000:31, 0x2000:4
    tail accounting            : 16 hdr + 236 stub + 22 msg + 102 reloc = 376, residue +0

Two things in that block deserve to be said out loud.

**`exepack_size` is 376 and `103,848 − 103,472` is 376.** A field in the file
predicts the file's own length from a position derived from the entry point.
That is the difference between "there is an `RB` here" and "this is an EXEPACK
image": the header has to close on the file, and it does.

**The zero relocations were never an anomaly.** EXEPACK moves the relocation
table out of the MZ header and into its own tail, as sixteen groups of one
`u16` count and that many `u16` offsets, one group per 0x1000 of segment. The
table has **35 entries** in two groups and it ends at byte 103,848 — the exact
end of the file, trailing zero. So the honest form of indicator three is not
*"zero relocations in 103 KB, which is unusual"* but *"zero in the MZ header
and thirty-five in the packer's own table, which is what this packer does"*.

## The decompression, which is the proof

EXEPACK is a run-length coder read backwards: skip the `0xFF` padding, then
take a command byte, a `u16` length, and either one byte to repeat (`0xB0`) or
that many bytes to copy (`0xB2`), with bit 0 of the command marking the last
one.

    python tools/exepack.py --unpack _work/popcorn.unpacked.bin game/popcorn.exe

    unpacked                   : 133296 bytes
    fill / copy commands       : 981 / 932
    destination bytes never written at the head : 0
    packed bytes left unread   : 0

**Residue zero at both ends.** 1,913 commands consume every one of the 102,960
packed bytes and fill every one of the 133,296 destination bytes declared by
`dest_len`. Two independent numbers, from opposite ends of a stream neither of
them describes, meeting exactly.

## And the 512 French strings were never evidence

They were the pre-briefing's best argument against packing and they are worth
nothing, for a reason that is a fact about this packer and not about this game.

**EXEPACK compresses runs, not phrases.** It has no dictionary and no back
references: a byte sequence that does not repeat is stored verbatim. Text does
not repeat, so text survives packing byte for byte, and the entropy of the
whole image lands near **6.11** rather than the 7.9 an LZ packer produces. Both
the legible strings and the modest entropy are *symptoms of EXEPACK*, and the
pre-briefing read both as arguments against it.

The receipt is that `tools/popmsg.py`, whose anchor is one encoded sentence
sixteen kilobytes into the *unpacked* image, finds that same sentence in the
*packed* file at offset 2,012 — because those bytes were copied through
untouched.

## The unpacked image behaves like an ordinary DOS binary

    python tools/dosimage.py _work/popcorn.unpacked.bin

    file                    bytes    H    blocks distinct const   d/b  print
    popcorn.unpacked.bin   133296  5.0655   520     463     58  0.890  0.043

Against `popcorn.exe`'s 405 / 405 / 1 and 6.1130. **Every one of the four
indicators moves to the ordinary side once the file is unpacked**, which is the
strongest available confirmation that packing caused all four.

The image splits cleanly in two, and the split is confirmed by the file's own
header rather than by eye. `real_cs` is `0x1AC2`, so the program's own segment
begins at image offset **109,088**; a 2 KB-window entropy scan jumps from about
3 to about 6.85 at 110,592 and stays there to the end.

| region | bytes | share | what it is |
| --- | --- | --- | --- |
| 0 – 109,088 | 109,088 | 81.8 % | data: strings, CGA graphics, the built-in level set (ch. 06), the hidden message (ch. 05) |
| 109,088 – 133,296 | 24,208 | 18.2 % | the program's own segment: code, the sound tables (ch. 08) and the note pointer |

`CS` and `DS` are the same segment: the sound routine sets `DS` with
`mov ax,1AC2h` and that immediate is one of the 35 relocations. A single
segment for code and data is also why a 103 KB program needs only 35 fixups.

## The cross-publisher table, which this collection could not make before

`tools/dosimage.py` puts all four indicators in one row and was run over
**thirteen MS-DOS binaries from three publishers** — this object's three, the
six of `pc-linksthechallengeofgolf-doc` and the four of
`pc-skunnybacktotheforest-doc`.

| file | bytes | H | blocks | distinct | const | d/b | reloc | fromEOF |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `golf.exe` | 60,950 | 7.9680 | 238 | 238 | 0 | **1.000** | 0 | 822 |
| `systype.exe` | 31,710 | 7.3466 | 123 | 123 | 0 | **1.000** | 0 | 31,454 |
| `title.exe` | 22,547 | 6.8918 | 88 | 88 | 1 | **1.000** | 0 | 385 |
| `INSTALL.COM` | 7,259 | 7.6524 | 28 | 28 | 0 | 1.000 | 0 | 333 |
| `xmm.exe` | 2,863 | 6.0107 | 11 | 11 | 1 | 1.000 | 0 | 317 |
| `setblast.exe` | 2,079 | 5.4431 | 8 | 8 | 1 | 1.000 | 0 | 317 |
| `uninstal.exe` | 1,633 | 5.0632 | 6 | 6 | 1 | 1.000 | 0 | 319 |
| **`popcorn.exe`** | 103,848 | 6.1130 | 405 | **405** | 1 | **1.000** | 0 | 360 |
| `HELPME.EXE` | 20,468 | 6.6604 | 79 | 77 | 3 | 0.975 | 81 | 19,444 |
| `popgen.exe` | 42,354 | 3.5168 | 165 | 125 | 39 | 0.758 | 1 | 41,714 |
| `FOREST.EXE` | 89,745 | 5.4291 | 350 | 249 | 102 | 0.711 | 352 | 87,697 |
| `RACE.EXE` | 162,721 | 4.6474 | 635 | 365 | 271 | 0.575 | 432 | 160,161 |
| `popspeed.exe` | 1,132 | 3.9324 | 4 | 4 | 1 | 1.000 | 1 | 620 |

**The prediction that `popcorn.exe`'s 1.000 would be unique was wrong, and being
wrong is what made the table useful.** Four of thirteen reach 1.000 at 32 blocks
or more, and the four sort themselves without being asked: every 1.000 in the
table has **zero relocations in its MZ header and an entry point within 900
bytes of EOF**, and every file that does not reach 1.000 has neither. That is a
cluster, not a coincidence, and one of its members — `INSTALL.COM` — is a
confirmed LZEXE 0.91 image with `LZ91` in its header, identified by the previous
session.

`popspeed.exe` reaches 1.000 with four blocks, which is arithmetic and not
evidence; `tools/dosimage.py` excludes anything under **32 blocks** from the
outlier list and says so in its output rather than hiding the threshold.

**So `popcorn.exe` was never an outlier.** It was a member of a family this
collection had already photographed twice and never named, and the two internal
controls the object supplies — `popgen.exe` and `popspeed.exe` — sit on the
ordinary side of exactly the four measurements that matter.

## What this cost the neighbours, and what is owed back

Running `tools/exepack.py` over the same thirteen:

| file | verdict |
| --- | --- |
| `title.exe` | **EXEPACK**, dest_len 1,844 par = 29,504 B, ratio 1.3639 |
| `xmm.exe` | **EXEPACK**, 162 par = 2,592 B, ratio 1.2857 |
| `setblast.exe` | **EXEPACK**, 153 par = 2,448 B, ratio 1.9870 |
| `uninstal.exe` | **EXEPACK**, 80 par = 1,280 B, ratio 1.6327 |
| `golf.exe` | not EXEPACK — no `RB` at entry−2 |
| `systype.exe` | not EXEPACK |
| `INSTALL.COM` | not EXEPACK — it is LZEXE 0.91 |

**Four of `pc-linksthechallengeofgolf-doc`'s six executables are Microsoft
EXEPACK images.** Its `docs/13-leftovers.md` records `title.exe` as *"compressed,
by an unidentified packer"* and adds *"No `LZEXE`, `PKLITE` or `EXEPACK`
signature was searched for by name and none announced itself"* — the same
sentence, and the same trap, one repository earlier. Chapter 10 writes the
correction out for hand-over and does not edit that repository.
