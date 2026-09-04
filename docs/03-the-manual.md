# 03 — the manual: a construction set, a gift, and three files that are not on the list

*Measure: `popcorn.doc` is 4,727 bytes of code-page-437 text, **121 lines, 121
of them CRLF-terminated**, read end to end with no residue. Its own file
manifest names **six** files; the directory holds **nine**.*

## The document

Fifty-eight lines of prose under a hand-drawn banner in box-drawing characters
spelling POP and CORN, then a second banner in block characters spelling LACRAL
with `────────software───────` ruled under it. Above both, on the first two
lines, the year and the two authors.

It is the only file in the object that is prose, the only one that carries the
year 1988, and — until chapter 05 unpacked the program — the only one that
named a person.

## The distribution model, preserved whole and pointing the other way

The previous object in this series devoted a quarter of itself to an order
form: twenty pages of distributors in twenty countries, a price, and the
signature of a chairman. **This object devotes a quarter of itself to a level
editor**, and its manual has a paragraph headed:

> `COMMENT DONNER CE JEU A VOS AMIS ?`
>
> (Car, bien sûr, il est permis, même recommandé, voire obligé de DONNER ce
> super jeu à un maximum de vos relations. )
>  La disquette n'est pas protégée, donc vous pouvez utiliser la commande
> `COPY A:*.* B:` ( ou `C:` si vous avez un disque dur) ou faire une copie de
> disquette avec `DISKCOPY A: A:` .

*How to give this game to your friends.* The disc is not protected, and the
manual prints the two DOS commands that copy it. Chapter 11 records that
`tools/protscan.py` finds zero markers for eleven copy-protection schemes
across all nine files, which is not a discovery: **it is the object doing
exactly what its own documentation says it does**, and the value of running the
scan is that the claim is now measured rather than believed.

Set against the same repository's neighbour, the two models are opposites and
both are complete: one product's commercial machinery survives in full, and
this one's refusal of any survives in full. Neither is inferred.

## What the manual states

* **CGA only.** *"Ce jeu ne fonctionne qu'avec une carte CGA."* Keyboard, or any
  Microsoft-compatible mouse with its driver loaded — *"en général MOUSE.COM"*;
* **an 8086 at 8 MHz**, with `POPSPEED` for anything else and a default value of
  **110**. Chapter 07 finds that 110 in the binary;
* **ten function keys.** F1 play · F2 demonstration · F3 mouse · F4 keyboard ·
  F5 redefine keys · F6 view the high scores · F8 select a colour palette ·
  F9 sound on/off · **F10 `Touche spéciale pour employés`** · Esc quit or pause.
  There is no F7. F8 is why chapter 13 records that the object uses more than
  one of CGA's palettes and that this session did not recover an image to test
  it on;
* **that `POPGEN` writes `.PPC` files** and that `POPCORN <name>` plays them:
  *"lancez le jeu en tapant: POPCORN POPTAB puis <RETURN>"*.

## The editor, which is a quarter of the object

`popgen.exe` is 42,354 bytes and 69 printable runs of eight characters or more.
It is not a level editor with a save button; it is a **disc-based application**
with a file browser drawn in box characters, tabs reading `FICHIERS`, `TABLEAUX`
and `INDICATIONS`, and fields for `Disque:`, `Répertoire:` and `Fichier:`.

    'Nom Fichier ... Sauvergarder ? :          .PPC'
    'Nom Fichier ... Lire ? :          .PPC'
    'Nom du Fichier ... EFFACER ? :'
    'Voulez-vous vraiment EFFACER ce Fichier ? (O)ui'
    'Catalogue ? :'   'Nouveau Disque ? :'   'Nouveau Répertoire ? :'
    'Répertoire inexistant. Appuyez sur une Touche'
    'Porte de disquette non prête ou Disque protégé contre l'effacement.'
    'Sauvegarde NON FAITE. Répertoire plein.'
    'Sauvegarde NON FAITE. Disque plein.'
    'Choisissez avec quel Tableau vous voulez faire la Permutation.'
    'Sauvegarde Impossible. Erreur de Conception du Tableau n'
    'Les Tableaux ont été modifiés. Voulez-vous SORTIR ? (O)ui'

It catalogues discs, creates directories, deletes files after asking twice,
detects a write-protected disc and a full one, swaps two boards within a set,
and refuses to save a board it considers unplayable. **In 1988, shipped free,
in the same 360 KB box as the game.** `Sauvergarder` is the authors' typo and
is quoted as it stands.

`LACRALLACRAL` occurs as twelve consecutive bytes in `popgen.exe` — the magic
pooled twice, adjacent, which is what a program that both writes and verifies a
header looks like. The same twelve bytes are in `popcorn.exe`; chapter 06 shows
that there the second copy is the header of the built-in level set.

## The manifest gap

`popcorn.doc` says: *"Cette disquette doit contenir les fichiers suivants"* and
lists six.

| the manual's six | present | the directory's other three |
| --- | --- | --- |
| `POPCORN.DOC` | yes | `pop.bat` |
| `POPCORN.EXE` | yes | `ltf.bat` |
| `POPCORN.HSC` | yes | `ltf.ppc` |
| `POPSPEED.EXE` | yes | |
| `POPGEN.EXE` | yes | |
| `POPTAB.PPC` | yes | |

**Somebody added a second level set and two batch files to this disc after the
manual was written**, and there is no evidence either way about who. What can
be said is that `ltf.ppc` is the degenerate set of chapter 06 — one board drawn,
forty-eight copies of somebody else's — which is what a first attempt with
`POPGEN` looks like, not what a shipped product looks like.

## The two batch files, and the one that cannot have worked

    pop.bat   13 bytes   POPCORN %1
    ltf.bat   16 bytes   popcorn lltf

`pop.bat` is **the manual's own example, minus one line**. The manual's recipe
for a batch file is:

>         SPEED votre valeur      <RETURN>
>         POPCORN %1              <RETURN>

`pop.bat` is the second line and not the first, which means it was typed by
somebody following the manual who had no need of the speed setting.

`ltf.bat` passes **`lltf`, with two Ls**, and the file on the disc is
`ltf.ppc`. Either the leading `l` is a flag the manual does not document, or
the batch file has a typo and never worked. **This session cannot settle it**:
the string `.PPC` does not occur anywhere in `popcorn.exe`, packed or unpacked,
so the game builds its filename at runtime and reading the argument parser needs
a disassembler this pipeline does not have. It is in chapter 13.

## `SPEED` and `POPSPEED.EXE`, a rename fossil in three places

1. the utility's own help text says **`Tapez: SPEED suivi d'un nombre`**;
2. the manual's batch recipe says **`SPEED votre valeur`**;
3. the file on the disc is **`POPSPEED.EXE`**.

The manual followed the program's help text rather than the filename. Anybody
who typed the manual's recipe verbatim got `Bad command or file name`, which is
a documentation bug that survived to the shipped disc and costs nothing to
report. How the utility actually passes its value is measured in chapter 07,
and the answer explains the manual's `110`.
