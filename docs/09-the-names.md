# 09 — the names: the clause the criterion was missing, and the door it stops at

*Measure: two surnames and two given names, in two files. One postal address,
one eight-digit telephone number given three times across two files, and two
mailbox handles. **The names are printed in this repository. The address and
the number are not.** This chapter is the argument for that line and the rule
that draws it.*

## The criterion, as it stood

Fifty-three sessions carried this, and it did its job every time:

> a name put by its owner inside a product they made and sold to the public is
> published; a pseudonym put by a third party inside a document that is not the
> product is not.

It was written for corporate names, developer credits and symbol tables. Every
previous object resolved by measurement: a symbol table with nobody in it, a
name field of 120 spaces, a chairman signing an order screen. **It has never
been asked about a street address belonging to two named private individuals**,
and applied mechanically to this object it publishes one, because that address
was put there by its owners, inside a product they made and gave to the public.

That is the wrong answer, and the criterion cannot see why.

## The clause

> **C — identity and reach are not the same datum.**
>
> A datum that *identifies* a person — their name, their role, their authorship
> of a work, the handle they signed it with — is admitted by the criterion. A
> datum by which a stranger could *arrive at* a person — a postal address, a
> telephone number, an electronic mail address, a mailbox on a message service,
> a coordinate — is not, however plainly the product printed it and however
> long ago.
>
> Contact details are reported as a **shape**: their kind, their count, and
> where in the object they sit, so that the measurement is on the record and
> reproducible from the object itself, without the digits.
>
> **Why the criterion did not already say this.** "Published" is not one act.
> Publication inside a product is bounded by that product's distribution: a
> street address on a floppy disc passed hand to hand in 1988 reached the people
> holding the disc. The same string in a public repository in 2026 is indexed,
> permanent, and joined by search to every other occurrence of the same name.
> **Republishing is not repeating.** A criterion that cannot separate the two
> treats consent to the first as consent to the second, and no one in 1988 gave
> the second.

Three corollaries, each of which this object generated:

> **C.1 — fame does not enlarge the clause, it tightens it.** A person becoming
> publicly known does not retroactively license their old contact details. It
> makes them *findable*, which is the whole harm, so the more identifiable the
> name the more carefully the reach is withheld.
>
> **C.2 — the burden of proof sits on publication, not on redaction.** Where a
> session cannot tell whether a contact datum is a business address or a home
> address, it does not publish it. "It might be a company" is not a finding.
>
> **C.3 — a name inside a file the program writes belongs to whoever typed it.**
> It is neither the product's authorship nor the publisher's. Until it is known
> which, it is treated as a person's, not as a label.

The generating case, so the clause travels with its evidence: **POP-CORN,
LACRAL software, 1988 — a public-domain game whose manual ends with an
invitation to write in, and gives the two authors' postal address so that a
reader could.**

## The count, which is the whole measurement

| datum | where | occurrences | published here |
| --- | --- | --- | --- |
| `LACRAL software`, the studio | `popcorn.exe` ×2, `popgen.exe` ×1, both `.ppc` as magic ×1 each; also in the hidden message | 4 files | **yes** |
| `LACAZE Christophe`, author | `popcorn.doc` ×2; `popcorn.exe` ×1, packed then XORed | 2 files | **yes** |
| `RAYNAL Frédérick`, author | `popcorn.doc` ×2; `popcorn.exe` ×1, packed then XORed | 2 files | **yes** |
| who did what | the hidden message only | 1 file | **yes** |
| the handles `CAZOU` and `SHIFT` | `popcorn.doc` ×1 each; the hidden message ×2 and ×4, plus 6 `>C:` and 7 `>S:`/`>s:` speaker marks | 2 files | **yes** — see below |
| a postal address: two surnames, a trading-style name, a street number, a street, a postcode and a town | `popcorn.doc`, once, in the last ten lines | 1 file | **no** |
| an eight-digit French telephone number for a message service the authors ran | `popcorn.doc` ×1, the hidden message ×2 | 2 files | **no** |
| `LTF`, in the user state | `popcorn.hsc`, record 0 | 1 file | see chapter 07 |

**And the pre-briefing's geometry was wrong in the direction that costs this
repository something.** It measured, correctly, that `RAYNAL` and `LACAZE`
occur in `popcorn.doc` and nowhere else, and built the privacy case on that
asymmetry. Chapter 05 unpacked `popcorn.exe` and found both names inside it —
invisible to `grep` because they are EXEPACK'd and then XORed with 0xAA. The
names are in **two** files, not one, and the telephone number is in two files,
not one. Correcting it enlarges the question rather than shrinking it, which is
why it is corrected here and in chapter 12 rather than left alone.

## The three judgements this chapter makes, and their reasons

**The names are published.** They are authorship. They are on the product's
first page, put there by their owners, above their own copyright line, and they
are the reason the object is worth documenting at all. A repository that
described this disc as "by an anonymous French studio" would be describing a
different object. This is the criterion working exactly as written.

**The address is not published, and not even in part.** The obvious middle
course — name the town, withhold the street — was considered and declined. A
town is not a digit, and on its own it is biography rather than reach; but two
surnames plus a town of that size is a very short list, and the clause is about
what a stranger could do with the sum, not about any one field. The address is
therefore reported as *"a postal address in a French town"* and that is the
whole of it.

The second line of that address block carries a trading-style word which is
**not** `LACRAL`. It is not printed either. Under the criterion a company name
is a publication and not a person — but in that block it is functioning as part
of a locator, and this session cannot establish that it was ever a registered
business rather than a letterhead. **C.2 applies: where it cannot be told, it
is not published.**

**The handles are published.** `CAZOU` and `SHIFT` are pseudonyms put by their
owners inside the product, and in the hidden message they are how the two
authors sign their own dialogue — `>C:` and `>S:` — so they carry authorship,
which is the thing the criterion admits. They are also mailbox names on the
message service, which is reach. The judgement is that a mailbox on a service
whose number is redacted and which has not existed for three decades reaches
nobody, while the attribution of half a hidden message is the object's own
content. **That is a judgement and not a deduction**, and it is written down
here so a later session can disagree with it.

## `LTF`, and the category the criterion has never had

`popcorn.hsc` record 0 holds `LTF` and a score of 546. It is either three
initials typed by a person or a label written by a program, and chapter 07 sets
out the evidence both ways without closing it.

**C.3 is written for exactly this and it is applied here.** Until the owner of
this machine reports whether the game prompts for a name, `LTF` is treated as
if it belonged to somebody: it is printed because the object prints it and
because three letters identify nobody, and no inference is drawn from it about
who played this copy or when.

**This is the first user state in this series with a name in it.** The previous
object's high-score file held 120 bytes of spaces and the question closed by
measurement; the one before that held names typed by the present owner of the
machine. This one holds three letters typed in 1988 or 1996 or later by
somebody nobody can now identify, and the criterion had no row for it.

## What is not claimed

`LACRAL` looks like `LACaze` + `RAynaL`. **The object never says so.** The
string does not appear beside either surname anywhere in the nine files or in
the unpacked image, and the hidden message names the studio and the two people
in the same sentence without connecting them. It is an inference, it is
labelled one, and it is not used to support anything else.
