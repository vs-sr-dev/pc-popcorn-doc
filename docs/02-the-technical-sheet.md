# 02 — the technical sheet: every figure with the command that remakes it

*Measure: forty-eight figures, each with the command that produces it. Every
number anywhere in this repository appears here or is derived from something
that does.*

All commands are run from the repository root with `game\` present. **No
command in this document writes to `game\`** and none executes any file of the
object.

## The object

| figure | value | command |
| --- | --- | --- |
| files, bytes, distinct sha1 | 9 · 169,530 · 9 | `python tools/hashall.py game` |
| mtimes | 9 of 9 at `1996-12-24 23:32:00` | `python -c "import glob,os,datetime,collections; print(dict(collections.Counter(datetime.datetime.fromtimestamp(os.path.getmtime(p)).isoformat() for p in sorted(glob.glob('game/*')))))"` |
| the neighbour's mtimes | 32 of 32 at `1996-12-24 22:32:00` | same, over `pc-linksthechallengeofgolf-doc`'s object directory |
| entropy by extension | `.EXE` 5.3499 · `.PPC` 2.3160 · `.DOC` 4.7748 · `.HSC` 1.4333 · `.BAT` 3.3830 | `python tools/entropy.py --tree game` |
| bytes that are executable | 147,334 = 86.9073 % | `python tools/account.py` |
| **coverage on D1** | **22,196 / 169,530 = 13.0927 %** | `python tools/account.py` |
| no product byte modified | 9 of 9 sha1 unchanged | `python tools/hashall.py game` at start and at end, `diff` |

## The three MZ images

| figure | value | command |
| --- | --- | --- |
| header / image / residue, all three | 512 / 103,336 / **+0** · 512 / 41,842 / **+0** · 512 / 620 / **+0** | `python tools/mz.py game/*.exe` |
| `e_lfanew` | 0 on 3 of 3 — no NE, LE, LX or PE | `python tools/mz.py game/*.exe` |
| relocations in the MZ header | 0 · 1 · 1 | `python tools/mz.py game/*.exe` |
| entry points | `1923:0010` = 103,488 · `0008:0000` = 640 · `0000:0000` = 512 | `python tools/mz.py game/*.exe` |
| entropy | 6.1130 · 3.5168 · 3.9324 | `python tools/entropy.py game/*.exe` |
| 256-byte census (blocks / distinct / constant) | 405 / **405** / 1 · 165 / 125 / 39 · 4 / 4 / 1 | `python tools/dosimage.py game/*.exe` |
| printable runs ≥ 5 | 512 · 141 · 16 | `python -c "import re;print(len(re.findall(rb'[\x20-\x7e]{5,}',open('game/popcorn.exe','rb').read())))"` |
| eight packer names, all nine files | 0 occurrences each | `python -c "..."`, see chapter 04 |
| the cross-publisher table, 13 binaries | 4 reach d/b 1.000 at ≥ 32 blocks | `python tools/dosimage.py game/*.exe <ten neighbour binaries>` |

## `popcorn.exe` as an EXEPACK image

| figure | value | command |
| --- | --- | --- |
| `RB` at `entry − 2` | bytes 103,486–103,487 | `python tools/exepack.py game/popcorn.exe` |
| `Packed file is corrupt` | 1 occurrence, at 103,724 | as above |
| EXEPACK header | 16 bytes at 103,472 | as above |
| `exepack_size` against the file | 376, and 103,848 − 103,472 = **376** | as above |
| original `CS:IP` / `SS:SP` | `1AC2:0113` / `1AA2:0200` | as above |
| `dest_len` | 8,331 paragraphs = **133,296 bytes** | as above |
| packed region | `[512, 103,472)` = 102,960 bytes | as above |
| ratio | 1.2946 | as above |
| tail accounting | 16 + 236 + 22 + 102 = 376, residue **+0** | as above |
| packer relocation table | **35** entries, groups `0x1000`:31 and `0x2000`:4 | as above |
| unpack | 981 fills + 932 copies; **0** destination bytes unwritten, **0** packed bytes unread | `python tools/exepack.py --unpack _work/popcorn.unpacked.bin game/popcorn.exe` |
| the unpacked image | 133,296 B · H 5.0655 · 520 / 463 / 58 · d/b 0.890 | `python tools/dosimage.py _work/popcorn.unpacked.bin` |
| the code/data split | `real_cs` `0x1AC2` → offset 109,088; entropy jumps at 110,592 | header, plus a 2 KB windowed entropy scan |
| the four Links EXEPACK images | `title` · `xmm` · `setblast` · `uninstal` | `python tools/exepack.py <the six Links binaries>` |
| refusal control | 5 of 5 refused | `python tools/exepack.py --refuse game/popgen.exe game/popspeed.exe game/poptab.ppc game/popcorn.doc game/popcorn.hsc` |

## The hidden message

| figure | value | command |
| --- | --- | --- |
| region, unpacked image | 16,157 … 18,575 = **2,418 bytes** | `python tools/popmsg.py _work/popcorn.unpacked.bin --accounting` |
| byte census | 2,355 `^0xAA` + 7 LF + 7 × 8 token = 2,418, residue **+0** | as above |
| the same message inside the packed file | 850 contiguous bytes at 2,039, residue +0 | `python tools/popmsg.py game/popcorn.exe --accounting` |
| refusal controls | `popgen.exe`, `poptab.ppc` refuse | `python tools/popmsg.py game/popgen.exe --refuse` |
| surnames inside `popcorn.exe` | 1 each, only after unpacking and decoding | chapter 05 |

## The level files

| figure | value | command |
| --- | --- | --- |
| magic and geometry | `LACRAL` + 49 × 176, residue **+0** on 2 of 2 | `python tools/ppc.py game/poptab.ppc game/ltf.ppc` |
| header field 1: bricks | agrees on **98 of 98** | as above |
| header field 2: type-9 count | agrees on **98 of 98** | as above |
| header field 3: type-9 positions | agrees on **98 of 98** used slots; unused slots zero on **97 of 98** | as above |
| distinct blocks | `poptab` 48 of 49 · `ltf` **2 of 49** · shared 1 | as above |
| `poptab` duplicate pair | blocks 7 and 22 | `python tools/ppc.py game/poptab.ppc --census` |
| cell types over 16,464 cells | 16 types; none is 4 or 11 | chapter 06 |
| built-in level set | **50** blocks at offset 50,284 of the unpacked image | chapter 06 |
| built-in vs shipped | 42 of 49 equal at the same index; 45 of 49 present anywhere | chapter 06 |
| refusal controls | 0 of 3 parsed, exit 1 | `python tools/ppc.py --validate game/popcorn.hsc game/popgen.exe game/pop.bat` |

## The user state

| figure | value | command |
| --- | --- | --- |
| shape | 180 = 10 × 18, all printable, residue **+0** | `python tools/hsc.py game/popcorn.hsc` |
| slots filled | 1 of 10; record 0 is `    LTF     ` / `000546` | as above |
| the default table inside the program | 180 bytes at offset 15,938 of the unpacked image | `python -c "import re;print([m.start() for m in re.finditer(rb'-{12}0{6}',open('_work/popcorn.unpacked.bin','rb').read())])"` |
| `popcorn.hsc/` has no slash | packed `popcorn.hsc/` vs unpacked `popcorn.hsc\0` | chapter 07 |
| refusal controls | `hsc.py` 0 of 3; `gamedata.py --hi` refuses | `python tools/hsc.py --validate game/poptab.ppc game/popcorn.exe game/pop.bat` |
| `POPSPEED` writes vector 68h | `mov ax,2568h` / `int 21h` at image offset 0x7A of its load image | chapter 07 |
| `POPCORN` reads vector 68h | `mov ax,3568h` at 131,745; default `0x6F` then `dec` = **110** | chapter 07 |

## The sound

| figure | value | command |
| --- | --- | --- |
| speaker port instructions in 133,296 bytes | 2 × `out 42h`, 1 × `out 43h`, 6 × `out 61h`, 5 × `in 61h` | `python -c "d=open('_work/popcorn.unpacked.bin','rb').read();print(d.count(b'\xe6\x42'),d.count(b'\xe6\x43'),d.count(b'\xe6\x61'),d.count(b'\xe4\x61'))"` |
| note tables | **7**, at 109,600 … 109,730, **131 bytes, 59 notes** | `python tools/pcspk.py _work/popcorn.unpacked.bin --from 109600 --to 109740` |
| longest table | 19 notes | as above |
| longest note run anywhere in the code segment | 19 | `python tools/pcspk.py _work/popcorn.unpacked.bin --from 109088` |
| chromatic frequency tables | **0** | chapter 08 |
| WAV rendering | 7 files plus one concatenation | `python tools/pcspk.py _work/popcorn.unpacked.bin --all _work/wav --from 109600 --to 109740` |

## The manual

| figure | value | command |
| --- | --- | --- |
| bytes, lines, line endings | 4,727 · 121 · 121 CRLF | `python -c "d=open('game/popcorn.doc','rb').read();print(len(d),d.count(b'\n'),d.count(b'\r\n'))"` |
| manifest | names 6 files; the directory holds 9 | read as CP437 |
| name geometry | `LACRAL` 4 files · `RAYNAL` 2 in `popcorn.doc` · `LACAZE` 2 in `popcorn.doc` | `for f in game/*; do grep -aoc LACRAL "$f"; done` |
| batch files | `POPCORN %1` (13 B) · `popcorn lltf` (16 B) | `cat game/pop.bat game/ltf.bat` |
| `.PPC` as a string | 0 in `popcorn.exe` packed and unpacked; present in `popgen.exe` | `python -c "print(open('game/popcorn.exe','rb').read().count(b'.PPC'))"` |

## Against the collection

| figure | value | command |
| --- | --- | --- |
| collection | 243 directories · **122** `*-doc` · **84** with `notes\` | `python -c "..."`, chapter 10 |
| crossings | **0** of 9, over 7 roots | `python tools/crossall.py notes/hashes.txt --collection <root> --skip pc-popcorn-doc` ×7 |
| root 7 sweep | 82 repositories · 359 list files · 128,756 hash tokens | as above |
| copy protection | 11 schemes × 0 hits; positive control fires on 5 of 9 files; `MARKERS` is 12 rows | `python tools/protscan.py game --all-files` |

## Hygiene

| figure | value | command |
| --- | --- | --- |
| tool count | 436 at the start, **443** at the end | `ls tools/*.py \| wc -l` |
| tool scan | 0 findings, all three positive controls fire, twice | `python tools/toolscan.py` |
| clause count and totals | 60 clauses; inherited 10.95 of 13, open 33.80 of 47 | `python tools/predcount.py` |
| verdict count | see chapter 14 | `python tools/checkscore.py` |
| nothing of the product is tracked | empty, with a positive control that fires | `git ls-files \| grep -Eiv "^(README\|docs/\|notes/\|tools/\|\.gitignore)"` |
