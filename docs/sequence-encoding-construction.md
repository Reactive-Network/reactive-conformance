# The RNK sequence-certificate and logs-tree encoding — PINNED, with a driven vector

**Status:** the byte-level encoding the signed-sequences upgrade design left `OUTLINED`, resolved and **driven in
two independent implementations**. ⇒ **This document is what `abci/rnk/sequence_encoding_vector.json` names in
its `sourceDocument` field**, and it is the *"single committed encoding artifact"* the upgrade specification
§15.2 and §2.7 require. Every digest in that artifact is transcribed from the tables below, never regenerated —
so a digest that appears to have moved is a finding rather than a value to update, and this file is the reference
it would have moved *from*.
⚠⚠ **READ THE BANNERS BELOW BEFORE ANY NUMBER IN THIS FILE** — the relocation note first, then revision 3, then
revision 2, which is the one that moved bytes. The leaf layout changed on
2026-08-20 and the "two independent implementations" claim above describes **revision 1's** drive; §6.1 splits the
provenance by class.

## ⚠ HOW THE REFERENCES IN THIS FILE WORK

⛔ **`§N` on its own always means a section OF THIS FILE.** Two other numbering systems appear and both are
always written out in words:

- **`RFC 6962 §N`** — the published standard, this construction's upstream normative reference.
- **`the upgrade specification §N`** — the signed-sequences upgrade design document. ⚠ **It is a working document
  and it is NOT in this repository**, and its numbering overlaps this file's (both have a §2 and a §3), which is
  why it is never referred to by number alone.

⇒ ⚠⚠ **No claim in this file depends on reading anything that is not in this repository.** Every requirement of
the upgrade specification that this file relies on is quoted verbatim or restated where it is used, so those
references are attribution and not a route a reader has to follow. The same discipline governs the working
reviews, probe trees, comparison scripts and second-party encoders behind §6: ⛔ **none of them is in this
repository, so none of them is cited by path** — where one established something, this file says what it
established and at what strength. **§6.1 and §6.4 are where that reckoning lives**, and §6.4 is the one to read
before trusting that any number here can be re-derived by running something.

## ⚠ RELOCATED INTO THE REPOSITORY, 2026-08-26 — NO DIGEST MOVED, AND THIS IS NOT A NEW REVISION

⛔ **Every digest, input, matrix and verdict below is revision 4's, unchanged** — which is why the artifact's
`sourceDocument` still pins *revision 4*: the normative content did not move, so the revision series does not
advance. What changed is that this file now lives where the artifact that cites it lives.

**Why it had to move.** The artifact's `sourceDocument` pointed at a path that existed only in a private working
area. ⇒ The reviewer check the artifact itself recommends — *pick any digest and find it in the source document*
— could not be run by anyone holding only the repository, and the artifact's own rule that a moved digest is a
finding was unenforceable without the reference it moved from. ⚠ **This file is the only independent origin of
forty cases' worth of digests**, which is what raises that from a nit.

**What the move changed in the text — and nothing else did:**

1. ⇒ **Every reference was audited.** References to files outside this repository are gone; each is replaced by a
   statement of what that file established, at the strength it was obtained. In-repository references are now
   paths from the repository root.
2. ⇒ **Internal review-artifact identifiers are gone.** §4's table was keyed by a review's own numbering of the
   fifteen divergences it found, which resolves against no document a reader of this repository holds, and the
   citations elsewhere in this file reached into that numbering. The rows are now keyed by their subject — which
   is what the numbers stood for — and every citation of one now names the row rather than a number. ⚠ Stated by
   position rather than as a count of citation sites, deliberately: a hand-kept count of them would be a mirror
   of them, and would go stale on the first edit that adds or removes one.
   ⚠ **The count is unchanged at fifteen and no row was dropped.**
3. ⇒ **§8 lost three items.** They were notes on how this pass was conducted — a checkpointing instruction, a
   contradiction between two working process documents, and a size measurement corrected from an earlier report
   — and each cited a document this repository does not carry. The three that carry technical content are kept.
4. ⇒ **The stale *"not yet the committed artifact"* status is corrected**, here and in §7.3 item 3: the artifact
   and its test exist. ⛔ **What still does not exist is a Sequencer build that fetches them**, so §7.3 item 4 and
   §7.2's owner question are untouched.

## ⚠ REVISION 4, 2026-08-21 — A SIGNATURE CASE EXISTS. NO BYTE MOVED.

⛔ **Every digest in this file is unchanged; both instruments in the new section re-derived
`cert/present-3-logs`' preimage and digest from §6.3.1's stated inputs before signing anything.** The vector pinned
the certificate's bytes and said **nothing about the signature over them** — so the one seam an independent issuer
is most likely to get wrong, `v ∈ {0,1}` versus the `{27,28}` its tooling emits, had no fixture behind it at all.
⇒ **§6.7 adds four `sig/*` cases and the clearly-marked test key they need**, with a measured matrix showing each
case flips under exactly the rule it guards — and, for the recovery-id pair, that a wrong-convention implementation
gets the **opposite** verdict on both, so the convention cannot be got wrong and still pass.

⇒ **The case count is 40.**

## ⚠ REVISION 3, 2026-08-20 — NO BYTE MOVED. A FALSE SENTENCE WAS REMOVED AND THE FIXTURE INPUTS WERE STATED.

⛔ **Every digest in this file is unchanged, and that is the point of the revision rather than an aside** — the
transcription control in §6.3.1 exists to prove it. Three things changed, all of them prompted by a second party
building this construction in TypeScript from this document's prose alone
(**61 assertions matched, 0 disagreements, 13 cases unreachable** — a working pass, not in this repository;
§6.1 and §6.4 carry its standing):

1. ⛔⛔ **`Hashes` is no longer described as being *"in verifier consumption order."*** **MEASURED: the phrase is
   false for 102 of 135 single-carried-leaf shapes**, and it names a verifier that **rejects honest blocks from
   *n* = 4 upward.** §3.6 now states positively where the fold order comes from, records the phrase as superseded,
   and **§6.6 is the new proof case that discriminates the two readings** — the two older proof cases pass under
   either, so the vector could not previously catch it.
2. ⇒ **§6.3.1 states the ten `leaf/*` and four `cert/*` fixtures' INPUTS.** They were a count, a length or a name;
   a second party could not construct them, so they contributed nothing to two-party agreement. ⚠ **§6.3.2 records
   what that cost:** five same-width certificate field transpositions were invisible to every certificate a second
   party could reach, and stating `cert/present-3-logs`'s inputs closes all of them.
3. ⚠ **`leaf/status-1-failed-receipt-still-in-tree` is renamed `leaf/status-1`** — an EVM failure is `status == 0`,
   which §6.5 says explicitly, so the old name asserted both `status = 1` and *this is the failed one*.

⇒ **The case count is 36** (33 in revision 1, 35 after revision 2's two `flatten/*` cases, plus §6.6's proof case).

## ⚠⚠ REVISION 2, 2026-08-20 — THE LEAF LAYOUT CHANGED. `logIndex` IS OUT OF THE LEAF PREIMAGE.

**What changed.** Revision 1 of this file put a 4-byte `logIndex` inside the leaf preimage (§3.2) and registered it
as deviation **D9**, together with a verifier-side `LogIndex == i` rule. ⇒ **Both halves are gone.** Option (d) of
the upgrade specification §2.4 — the index **outside** the preimage — is the ratified decision, and the design's
topology decisions were corrected on **2026-08-20** to state that the second of D9's two MUSTs never stood: a log's position is
**derived by traversal** and certified by folding its audit path against the signed count and root, and the
comparison D9 proposed is one value against itself because the proof carries no index field.

**What that costs this file, and why the change is upward rather than sideways.** A 4-byte insertion moves **every**
digest that routes through a leaf. ⇒ §3.2's layout and its stated leaf size are revised, and so are **24 of the 33**
vector cases in §6.3: the 10 `leaf/*`, the 10 `tree/n1…n1024`, the 2 `cert/present-*`, and both `proof/*` cases,
whose interval hashes are subtree roots over the same leaves. **The remaining 9 — the three keccak controls, the
three tag byte strings, `tree/n0-empty-root`, `cert/void-zero-leaf` and `cert/max-width` — touch no leaf and are
byte-identical in both layouts**; ⛔ **if one of those nine ever appears to have changed, that is an error and not a
regeneration.**

**Why this direction and not the other.** ⚠ It was settled by measurement, not by preference, and the measurement is
not this file's: the cryptographic-conformance peer review of `reactive-tornado`'s implementation independently
recomputed all 24 digests committed there — its own byte assembly, hashed by `cast keccak` (foundry, Rust; 2 075
keccak calls; 32 checks, 0 failures) — and then proved its instrument fires by re-running it with `logIndex`
inserted, matching **23 of 23** of revision 1's values. ⇒ **Both vectors are internally correct for their own
layout. The repository implements the ratified decision; this file was the stale side.**

⚠ **The superseded digests are RETAINED, not deleted** — §6.3 carries them in their own column. A vector whose
history has been erased cannot diagnose an implementation that was built against the layout it replaced, and
revision 1 of this file circulated.

⚠⚠ **WHY THIS IS A SEPARATE DOCUMENT rather than an extension of the delta analysis that preceded it, since I
was asked to say which and why:** that analysis is an **argument** about whether to have these bytes; this one
**is** the bytes. The upgrade specification §15.2 asks for *one artifact with one owner* that another
repository's CI gates on — an artifact whose top half debates its own existence cannot serve that role, and a
Sequencer-side reviewer should not have to read a delta analysis to find a field width.
⇒ That analysis keeps the reasoning and is a working document outside this repository; what it established is
stated here at each point of use, and this file carries the normative content.

## ⛔ What this file is NOT

⚠ **It is not the artifact.** The artifact is `abci/rnk/sequence_encoding_vector.json`, which the upgrade
specification §15.2 requires to live in this repository as a committed fixture plus a test, with the Sequencer's
build gating on it. ⇒ **This file is the specification of that artifact and the driven values it carries**; the
artifact is the machine-readable transcription, and where the two disagree **this file governs.**
⇒ ⚠ **The fixture and its test now exist** — `abci/rnk/sequence_encoding_vector.json` and
`abci/rnk/sequence_encoding_vector_test.go`. ⛔ **What does not exist is a Sequencer build that fetches them**, and
**who owns the artifact is still the BLOCKING open question** — §7.2 and §7.3 below.

## Provenance

| | |
|---|---|
| **Decision authority** | maintainer, relayed 2026-08-19: *"I'd prefer to stick to published standards, so dropping multiproofs seems prudent."* ⇒ the multiproof is **DROPPED**; deduplicated RFC 6962 §2.1.1 inclusion proofs are adopted |
| **Trees read** | this repository at **`a1787c8c29962d8e038d6f6a33af5cfa4465350b`**; and the two sibling repositories, **read-only** — `reactive-sequencer` **`c3916f7`** (branch `master`) and `grpc-broadcaster` **`596fdf254f75dca273f8fdd48255a00a97be9e9a`**. ⚠ Those two are not this repository and are not vendored into it |
| **Hash implementation A** | production go-ethereum `crypto.Keccak256`, via the vendored fork `github.com/Reactive-Network/geth-rnk2-genesis@v0.0.0-20260706123415-ecb3dad88727` |
| **Hash implementation B** | a pure-Python Keccak-256 written for this pass, independent of A |
| **Upstream normative reference** | **RFC 6962** §2.1, §2.1.1 (and §2.1.2, §3.5 for what we do *not* use) |
| **Probe tree** | a working tree, **not in this repository** — §6.4 states what it established and ⛔ why it must not be re-run as a source of a current value |
| **Hash implementation C** (revision 2) | `cast keccak` — foundry 1.5.1, Rust — used for the regeneration and for its transcription check. Neither A nor B |
| **Revision-2 authority** | the ratified option (d): `logIndex` **out** of the leaf preimage, and no verifier-side index equality. Relayed 2026-08-20 as *"(d) stands, its SECOND MUST did not"* |

**Claim labels** inline: MEASURED (I ran it) · VERIFIED (I read it) · INFERRED · RELAYED · SEARCHED.

---

# 1. THE DEVIATION REGISTER

⚠ **Purpose, in the words of the request that commissioned this file: it converts *"we stuck to published standards"* from a claim into a
checkable list.** ⛔ Every row states the departure, whether it is **necessary**, and the risk assessment **at the
strength it was actually obtained** — so the maintainer can overrule any single row cheaply.

⚠ **Reading key for "necessary":** *forced* = no conforming alternative exists · *chosen* = a conforming
alternative exists and was not taken · *n/a* = not a departure, listed to stop a reader looking for one.

| # | departure from RFC 6962 | necessary? | risk | reasoning |
|---|---|---|---|---|
| **D1** | ⚠⚠ **keccak256 substituted for SHA-256** (§2.1 specifies SHA-256: *"The hashing algorithm is SHA-256"*, VERIFIED) | **forced** | **LOW** | ⇒ **Registered as deviation #1, as asked, and the requester's own judgement is adopted rather than re-derived:** substituting keccak in a Merkle tree is standard EVM-ecosystem practice, and **the tree's security argument depends only on the underlying hash's collision resistance, not on which hash it is** — RFC 6962 §2.1's structure is hash-agnostic. Same 256-bit digest, same security target. **Forced** because every consumer of this data is EVM-side: `abci/rnk` hashes with `crypto.Keccak256Hash` throughout (VERIFIED, 19 hash sites), and a deferred layer C would verify in Solidity, where keccak256 is the free primitive and SHA-256 is a precompile call. ⛔ **Overruling this row means changing every hash in the design and paying gas in any future on-chain verifier.** |
| **D2** | ⚠⚠ **ASCII domain tags in place of the `0x00` / `0x01` prefixes** (§2.1) | **chosen** | **LOW** | **The tradeoff, stated as asked.** *Gained:* the version lives in the tag, so a deliberate encoding change **cannot** be rolled out silently — the in-repo precedent's own stated reason (VERIFIED at `abci/rnk/mem_filters.go`: *"bumping a tag changes every digest"*). *Paid:* 13 extra preimage bytes per node, never transmitted; and no RFC test vector applies. ⚠ **Separation is preserved and the argument is one line: all three tags are exactly 14 bytes and differ at byte 7** (`rnk.seqleaf.v1` / `rnk.seqnode.v1` / `rnk.seqcert.v1`, MEASURED as `0x726e6b2e7365716c6561662e7631` etc.), so **no tag is a prefix of another and a leaf preimage can never equal a node preimage.** ⇒ **This also closes a published pitfall the RFC's own scheme has:** OpenZeppelin's *"avoid 64-byte leaf values, because a sorted pair of internal nodes could be reinterpreted as a leaf"* is **structurally impossible** here. ⛔ That reason was recorded nowhere before this file. |
| **D3** | **secp256k1 (r,s,v), low-S, `v ∈ {0,1}`** in place of §3.5's TLS `digitally-signed` signature algorithms | **forced** | **LOW** | secp256k1/ECDSA is as heavily attacked as any signature scheme in use. **Forced** by the design's own `KeyId`→committed-registry model and by `ecrecover` being the only signature primitive available to a future on-chain verifier. |
| **D4** | **`SequenceCert` is not a Signed Tree Head.** §3.5's STH signs `{version, signature_type, timestamp, tree_size, sha256_root_hash}` (VERIFIED); ours adds source-chain provenance and consumer binding | **forced** — it attests a *different object* | **LOW** | ⚠ **One row where we are ALIGNED and it deserves saying: signing `LogCount` IS the RFC's `tree_size`.** The additions (`ChainId`, `BlockHash`, `ParentHash`, `Number`, `Time`, `NetworkId`, `KeyId`) exist because we attest *an external chain's block*, which CT has no analogue for. The **serialisation** departs (keccak over a flat layout, not a TLS struct) — see D5. |
| **D5** | **The leaf and certificate preimage byte layouts are entirely ours** | **n/a — outside RFC scope** | **LOW, once pinned** | ⚠ RFC 6962 §2.1 hashes `0x00 ‖ d(i)` with **`d(i)` an opaque octet string** (VERIFIED); CT's own leaf structure is §3.4 and is CT-specific. ⇒ **Every design in this family must encode something; there is nothing to conform to.** The risk is not the *choice* but the *ambiguity*, and it is discharged by §3's fixed widths (which make injectivity immediate), §4's closing sentences, and §6's driven vector. |
| **D6** | ⚠ **Deduplicated proof serialisation**: the union of the carried leaves' §2.1.1 audit paths, each distinct node sent once | **chosen** | **LOW, and now DRIVEN** | ⇒ **Soundness-neutral by construction, and the argument is short — which is the point**, the standing design constraint for this upgrade being that *the verification argument must stay short enough to be checkable*: each carried leaf is verified **whole, on its own, by RFC 6962 §2.1.1**, against the signed root. The table is a transport optimisation with **zero** effect on what any path verifies. ⚠⚠ **BUT it had a defect I found while pinning it, and it is MEASURED, not inferred — see §5.** |
| **D7** | **No consistency proofs** (§2.1.2 `PROOF`/`SUBPROOF`) | **n/a** | none | Listed only so a reader stops looking: each sequence has an independent tree and we claim **no** append-only property between them. |
| **D8** | **No root tag.** The root is the top interior node | **n/a — this is the RFC's behaviour** | none | ⚠ Registered because the **in-repo precedent has one** (`filtersRootTag`, VERIFIED) and would tempt an implementer to add a third tag. **We follow the RFC here, not the precedent.** |
| **D9** | ⛔⛔ **RETIRED 2026-08-20 — NO LONGER A DEPARTURE.** Revision 1 registered *"`logIndex` inside the leaf preimage, plus a `LogIndex == i` rule"* as a chosen departure; **both halves are withdrawn** and the leaf preimage now binds no index, which is CT's own behaviour | **n/a — the departure was removed** | none | ⚠ **The superseded rationale, kept verbatim because a retracted argument must be replaced rather than deleted:** *"these are the SAME constraint twice, and neither authenticates the index against an independent record, because none exists — the index is derived at serve time and is not at rest (VERIFIED on both Sequencer repos). Cheap belt-and-braces; its whole authority is [the upgrade specification] §15.2's traversal requirement, which is OPEN."* ⇒ **That authority never materialised.** The ratified rule is that a position is **derived by traversal** and certified by folding the leaf's audit path against the signed `LogCount` and `LogsRoot`. ⛔ **DO NOT RE-ADD EITHER HALF.** The equality in particular cannot fail: `SequenceProof` (§3.6) has **no index field**, so the "proven position" a verifier would compare against is derived FROM the carried index — `x == x` wearing the costume of an authenticated position, passing for a lying proposer exactly as for an honest one. ⚠ **The surviving true half:** `SequenceLog.LogIndex` is still RLP'd into the block and still reaches `react()`, so it remains an on-chain observable **outside** the authenticated set, constrained by no verifier-side equality. |

## ⇒ 1.1 The register's verdict

**Nine rows. Two are forced substitutions of standard primitives (D1, D3). Five are not departures at all (D4's
object, D5's scope, D7, D8, and — since revision 2 — the retired D9). Two are chosen (D2, D6), each low-risk with a
stated tradeoff.** ⚠ **Revision 2 removed a departure rather than adding one:** with `logIndex` out of the leaf
preimage the construction is closer to RFC 6962 than revision 1 was, not further from it.

⇒ ⛔ **I found no departure I judge NOT low-risk, so I did not stop.** ⚠ **What I did find is a DEFECT inside a
departure — D6's free-space channel (§5) — and it is fixed rather than documented**, per the standing
preference for repairing a found defect over recording a caveat about it.

⚠⚠ **AND A DEFECT IN THE SPEC ITSELF THAT THE REGISTER EXPOSED, which nobody had caught:** the upgrade specification
§2.4's **prose** and its **code block** specify two different constructions, in adjacent lines. VERIFIED verbatim
in that document at §2.4:

> *"RFC-6962 shape: `leaf = H(0x00 ‖ …)`, `node = H(0x01 ‖ left ‖ right)`"* — **the RFC's prefixes** —

immediately above a code block using **`"rnk.seqleaf.v1"` / `"rnk.seqnode.v1"`**, and a Requirement saying *"MUST
use RFC-6962 leaf/interior domain separation"*, which reads as the prefixes again. ⇒ **The spec does not say which
of D2's two sides it is on.** This file rules: **the tags govern** (D2), and that prose must be corrected to say
*"RFC 6962's tree shape, with domain-separating tags in place of its `0x00`/`0x01` prefixes."*

---

# 2. THE CONTRADICTION, RESOLVED — flat fixed-width GOVERNS; `rlp(…)` is deleted

**The contradiction**, established by the cryptographic-conformance review of this construction: the upgrade
specification §2.7 requires *"every integer … as a **fixed-width** big-endian value"*; its §2.3 defines `preimage = keccak256("rnk.seqcert.v1" ‖ NetworkId ‖ **rlp**(SequenceCert without
Sig))`. RLP integers are **minimal-length** big-endian with no leading zeros and `0` → `0x80`. VERIFIED in the
vendored go-ethereum fork this repository builds against (`github.com/Reactive-Network/geth-rnk2-genesis`, pinned by
the `replace` directive in `go.mod`): `rlp/decode.go`'s `ErrCanonInt`, and `rlp/decode_test.go` pinning
`{input: "00", ptr: new(uint32), error: "rlp: non-canonical integer (leading zero bytes) for uint32"}`.

## ⇒ RULING: the upgrade specification §2.7 governs. `rlp(…)` is removed from the certificate preimage.

### Requirement: hashed preimages are flat, fixed-width, big-endian concatenations
The system MUST compute every hashed preimage in this construction as a flat concatenation of fixed-width
big-endian integer fields and fixed-width byte fields, and MUST NOT use RLP, protobuf, JSON or any
self-describing encoding inside a hashed preimage.

- **Trigger class:** block-bytes.
- **Scenario:** GIVEN the same certificate content WHEN the signer and the verifier each compute the preimage
  THEN they produce identical bytes, and the preimage's length is a function of the topic count and data length
  alone.
- **Because:** four reasons, strongest first.
  1. ⚠⚠ **Fixed widths are what make the LEAF preimage injective, and RLP does not supply them.** With
     minimal-width length fields, `… ‖ nTopics ‖ topics[…] ‖ lenData ‖ data` admits constructible collisions — a
     1-byte and a 2-byte `nTopics` shift everything after them. With every field fixed-width, injectivity is
     immediate by inspection: a **constant-length prefix** followed by two **length-prefixed** variable regions.
     ⇒ **That requirement is not hygiene; it is what makes the leaf hash a function of the log rather than of its
     serialisation.**
  2. **The leaf preimage is already flat** (the upgrade specification §2.4's own code block). Keeping RLP for the certificate leaves two
     opposite encoding disciplines in one construction.
  3. ⚠ **RLP-over-a-Go-struct exports Go's struct-encoding rules as normative to a non-Go signer.** VERIFIED that
     `reactive-sequencer` is **TypeScript on Bun** whose only crypto-adjacent dependency is `@ethereumjs/rlp`;
     under RLP it would have to hand-reproduce Go's treatment of `uint8` 0 → `0x80`, `[32]byte` → a 32-byte
     string, and field order fixed by Go declaration order.
  4. ⚠ **A flat layout cannot be changed by accident.** Under `rlp(SequenceCert)` a Go-side field reorder or type
     change **silently changes every preimage**; under an explicit layout it cannot. ⇒ **What looks like the cost
     of option A is actually its main benefit.**
- **Retired when:** never, while two repositories compute one hash.
- **Depth:** SPECIFIED, and **driven** (§6).

⚠ **Consequence for the upgrade specification §2.3, stated so it is not missed:** `NetworkId` appeared **twice** under the old formula (once
raw, once inside the struct). In the pinned layout it appears **once**, hoisted to immediately after the tag so the
*"domain tag then network binding"* prefix shape it intended is preserved. ⇒ **This resolves §4's
`NetworkId`-twice divergence.**

---

# 3. THE PINNED ENCODING — normative

## 3.1 Constants

| name | value | bytes |
|---|---|---|
| `leafTag` | `"rnk.seqleaf.v1"` | `0x726e6b2e7365716c6561662e7631` (14) |
| `nodeTag` | `"rnk.seqnode.v1"` | `0x726e6b2e7365716e6f64652e7631` (14) |
| `certTag` | `"rnk.seqcert.v1"` | `0x726e6b2e736571636572742e7631` (14) |

⚠ **A tag is its raw ASCII bytes — unprefixed, unterminated, no length field.** (Matches the in-repo precedent,
VERIFIED: `append(buf, filtersLeafTag...)` over a bare Go `string` constant.) ⇒ Closes §4's tag-byte-encoding divergence.

| name | value |
|---|---|
| `kindVoid` | `0x00` |
| `kindPresent` | `0x01` |

⚠ **`Kind`'s values were stated NOWHERE before this file** — the first of §4's fifteen divergences, and the one that would
have diverged every certificate from block 1. ⛔ **The assignment is arbitrary and is pinned, not derived. Do not
give it a fresh rationale.** The only property worth noting is that the zero value is the more restrictive one
(a `void` certificate forbids a payload row), so a defaulted field fails closed.

## 3.2 The leaf preimage — 90 + 32·nTopics + lenData bytes

⚠ **REVISED IN REVISION 2 (2026-08-20): `logIndex` is NOT a field here.** Revision 1's layout carried it as 4
big-endian bytes between `seqNumber` and `status`, giving a leaf size of `94 + 32·nTopics + lenData`. See the
revision banner at the top of this file, and D9.

```
leafTag                14 bytes  raw ASCII
seqNumber               8 bytes  big-endian uint64
status                  8 bytes  big-endian uint64
txHash                 32 bytes
address                20 bytes
nTopics                 4 bytes  big-endian uint32
topics[0..nTopics-1]   32 bytes each
lenData                 4 bytes  big-endian uint32
data                   lenData bytes
```

**Field provenance, VERIFIED at `abci/rnk/types.go` `a1787c8c2`:** `seqNumber` ← `Sequence.SeqNumber` `uint64`;
`status` ← `SequenceReceipt.Status` **`uint64`**; `txHash` ← `SequenceReceipt.TxHash` `common.Hash`; `address` ←
`SequenceLog.Address` `common.Address`; topics ← `SequenceLog.Topics` `[]common.Hash`; `data` ←
`SequenceLog.Data` `[]byte`.

### ⛔ WHAT AUTHENTICATES A LOG'S POSITION, since no field in the leaf does

A log's position is authenticated by **the audit path it verifies under, together with the `LogCount` the
certificate signs** — and by nothing else. ⇒ Two consequences, and neither may be undone:

- **`LogCount` is load-bearing, not decorative.** Without a certified count an honest audit path verifies at a
  lied-about position: RFC 6962 §2.1.1's index/total reduction produces the same left/right side sequence for many
  `(index, total)` pairs, so a free `total` lets a proposer move a log. This is why `LogCount` is inside the signed
  certificate preimage (§3.5) and not merely alongside it.
- ⛔ **A verifier MUST NOT compare the carried `LogIndex` against "the proven position".** It is the first rule most
  readers reach for and it is the one rule guaranteed to pass — see D9 for the mechanism. What it must do instead is
  fold the leaf's §3.6 audit path, parameterised by the carried index and the signed count, up to the signed
  `LogsRoot`, and reject the block if the fold does not reach it.

⚠ **A property of option (d) that looks like a defect and is not:** two logs in one sequence with the same address,
topics and data now produce **byte-identical leaves**. That is harmless in RFC 6962 — a proposer must still supply a
valid path at whichever position it claims, and both positions genuinely contain that log. ⛔ Do not "fix" it by
putting the index back.

### Requirement: the leaf preimage binds no log index
The system MUST NOT include a log's index, or any value derived from it, in the leaf preimage, and MUST NOT gate
proof acceptance on an equality between a carried `LogIndex` and a position derived from that same carried index.

- **Trigger class:** block-bytes for the first clause (it changes every root and every signed digest); the second
  clause is not a check at all, which is the point.
- **Because:** ⇒ **the ratified option (d)**, plus the mechanism in D9: the proposed equality has one operand, so it
  cannot fail, and a check that cannot fail reads as coverage in review and on a dashboard while constraining
  nothing.
- **Retired when:** never, while `SequenceProof` carries no index field.
- **Depth:** SPECIFIED, and the first clause is pinned by every `leaf/*` and `tree/*` value in §6.3.

⚠ **The three widths the upgrade specification §2.7 could not resolve, and why:**

- **`status` = 8 bytes.** Its declared type is `uint64` on **both** Go sides (`abci/rnk`'s `SequenceReceipt` and
  `grpc-broadcaster`'s `TinyReceipt`, both VERIFIED). ⛔ **Do not narrow it to one byte** because the value is 0/1:
  the width follows the declared type, not the observed range, so a future non-boolean status cannot silently
  change the encoding.
- **`nTopics` = 4 bytes (uint32).** ⚠ It has **no declared type anywhere** — it is `len(log.Topics)`. Chosen to
  match `LogCount`'s `uint32`. ⛔ **Deliberately NOT `uint8`**, even though the EVM emits at most 4 topics:
  `Sequence.FromProto` copies `logProto.Topics` with **no bound** (VERIFIED), so a `uint8` width would wrap at 256
  and make two different logs collide. **The vector pins a 5-topic case for exactly this reason.**
- **`lenData` = 4 bytes (uint32).** Also no declared type; `uint32` bounds `data` at 4 GiB, far above any reachable
  size.

## 3.3 The interior node — 78 bytes

```
nodeTag                14 bytes  raw ASCII
left                   32 bytes
right                  32 bytes
```

## 3.4 The tree — RFC 6962 §2.1, adopted including BOTH base cases

```
MTH({})      = keccak256("")                                  <- RFC 6962 s2.1
MTH({d0})    = leaf(d0)                                       <- RFC 6962 s2.1
MTH(D[n])    = node( MTH(D[0:k]), MTH(D[k:n]) ),  n > 1
               k = the largest power of two STRICTLY below n   <- RFC 6962 s2.1
```

⚠ **No padding convention. `n` need not be a power of two** — VERIFIED verbatim in §2.1: *"Note that we do not
require the length of the input list to be a power of two."*

### ⇒ RULING on the empty tree: **adopt RFC 6962 §2.1's own rule.**

`MTH({}) = keccak256("") = 0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470` (MEASURED, and
independently by `cast keccak 0x`).

- ⇒ **Under the maintainer's principle the RFC's value is the default and it needs no argument of its own.** The upgrade specification
  §2.7's requirement is satisfied as written: it is a defined constant and it is **not** the zero hash, so *"no root"* and
  *"the root of nothing"* stay distinguishable.
- ⛔ **REJECTED, and recorded here as §3.4's comment requires: `keccak256("rnk.seqroot.empty.v1")` =
  `0xca30fc15617bfeaecb01ac0528ad12c0546b676fcae06905955f6ad5c01e7600`** (MEASURED). It is defensible — domain-
  separated and version-carrying, matching D2's discipline — and it was **not** taken because it is a gratuitous
  departure on the single case that occurs most often.
- ⚠ **The one honest cost of adopting the RFC's value, named so nobody rediscovers it:
  `keccak256("")` is Ethereum's `EMPTY_CODE_HASH`** — a constant that genuinely circulates in EVM state. ⇒ **Not an
  attack surface** (an actor who can set `LogsRoot` can set it to anything; the field is inside the signed
  preimage), and **not an accident surface** (a defaulted field is zero, not `keccak256("")`). Registered as a
  known coincidence, not a risk.
- ⚠⚠ **AND WHY THE IN-REPO PRECEDENT CANNOT BE COPIED HERE:** `contentDigest`'s empty value
  `0xb883327dcbe7961aa858d9fb496eacf9f5409d63cdb8d330bb732be0b4a02451` is **derived, not special-cased** — its
  64-bucket fold is total for an empty index. **RFC 6962's recursion is NOT total for n = 0**, which is exactly why
  the RFC states the case explicitly and why we must too. ⛔ Only the non-zero-ness lesson transfers.

### ⇒ RULING on n = 1: **adopt RFC 6962 §2.1's own rule — the root of a one-leaf tree IS the leaf hash.**

⚠⚠ **The upgrade specification §2.7 defines n = 0 and FORGOT n = 1** (§4's *n* = 1 row), and this is not a cosmetic gap:
**MEASURED-by-construction, §2.1's split rule applied to a one-element list yields `k = 1` and an EMPTY right
half**, so the recursion is ill-defined at n = 1 without the base case. ⛔ **And the tempting wrong answer —
`node(leaf, leaf)` — is `CVE-2012-2459`'s own duplicate-last-leaf shape**, which the upgrade specification §2.4's `Because:`
warns against in the other direction. **No interior node is applied at n = 1.**

### Requirement: the logs tree covers every log of every receipt
The system MUST build the logs tree over **every log of every receipt of the sequence, in stored order, including
the logs of receipts whose `status` indicates failure**, and `LogCount` MUST equal that total.

- **Trigger class:** block-bytes.
- **Because:** ⚠⚠ **this is the only answer consistent with the served index, and it is VERIFIED rather than
  chosen:** `grpc-broadcaster`'s `sequenceMsgToEvent` increments `logIndex` across `block.Receipts` **with no
  status check**, so the served `log_index` counts failed receipts' logs. ⛔ **The tempting wrong reading is on OUR
  side:** `processEventsWithNormalization` drops `Status == types.ReceiptStatusFailed` **before doing anything
  else**, which is the first thing an `abci/rnk` implementer reads. Excluding them changes *n*, every leaf index,
  and the root. ⇒ **§4's *failed receipts* and *what `LogCount` counts* rows.**
- **Retired when:** never, while the index is a dense count over stored order.
- **Depth:** SPECIFIED, and the vector pins a failed-receipt leaf.

## 3.5 The certificate preimage — 159 bytes, always

```
certTag                14 bytes  raw ASCII
NetworkId               8 bytes  big-endian uint64
SeqNumber               8 bytes  big-endian uint64
Kind                    1 byte
KeyId                   4 bytes  big-endian uint32
ChainId                 8 bytes  big-endian uint64
BlockHash              32 bytes
ParentHash             32 bytes
Number                  8 bytes  big-endian uint64
Time                    8 bytes  big-endian uint64
LogCount                4 bytes  big-endian uint32
LogsRoot               32 bytes
```

`certDigest = keccak256(preimage)`; the signature is secp256k1 over `certDigest`, 65 bytes, low-S, `v ∈ {0,1}`.
⚠ **`v` is the recovery id 0 or 1, NOT the `{27,28}` most Ethereum tooling emits** — the two conventions disagree on every certificate, and §6.7's `sig/*` cases are what stop an implementation picking the wrong one silently.

⚠ **The length is CONSTANT at 159 bytes** (MEASURED across the void, present and max-width vectors) — which is
itself a cheap implementation check: a preimage of any other length is a bug.

### Requirement: a void certificate's block fields are zero and remain in the preimage
For `Kind == kindVoid` the system MUST set `ChainId`, `BlockHash`, `ParentHash`, `Number` and `Time` to their zero
values, MUST set `LogCount` to 0 and `LogsRoot` to the empty-tree constant, and MUST include all of them in the
preimage at full width.

- **Because:** VERIFIED that this is what the node holds — `Sequence.FromProto` returns early when
  `sequence.Block == nil`, leaving every block field at its zero value. ⇒ Truncating or omitting them would make
  the preimage variable-length and would diverge from what the verifier can reconstruct. **§4's void-block-fields row**,
  and it hits **every** void certificate.
- **Depth:** SPECIFIED, and pinned by the `cert/void-zero-leaf` vector.

## 3.6 The proof — deduplicated RFC 6962 §2.1.1 audit paths

**Node identity is the leaf interval `[lo, hi)`.** ⛔ **NOT `(level, index)`:** because the split is at the largest
power of two strictly below *n*, the tree is **not level-uniform** for non-power-of-two *n*, so a level/index scheme
is ill-defined — and it is the first thing most implementers reach for (§4's node-identity row).

```
SequenceProof { SeqNumber uint64; Hashes []common.Hash }
```

**`Hashes` is the union of the carried leaves' RFC 6962 §2.1.1 audit paths, each distinct node appearing exactly
once, in ascending canonical order of its leaf interval — `lo` ascending, then `hi` ascending.**

⇒ ⚠⚠ **WHERE THE FOLD ORDER COMES FROM, stated positively, because there is exactly one right answer and the
wrong one rejects honest blocks.** ⛔ **The order the table is transmitted in is NOT the order a verifier consumes it
in.** A verifier regenerates the interval list itself — `neededIntervals(carried, LogCount)`, sorted `lo` ascending
then `hi` ascending — and **indexes into `Hashes` positionally by that list**. It then folds each carried leaf in
**RFC 6962 §2.1.1's own** order, looking each sibling up **by interval**, and decides that sibling's side by comparing
intervals: a sibling whose `lo` is below the accumulator's current `lo` is the **left** child, otherwise the
**right**. ⇒ **Nothing on the wire, and no property of the table's order, tells the verifier the fold order** — it
derives both orders from `LogCount` and the carried indices and converts between them locally.

⛔ **SUPERSEDED, and recorded rather than deleted so that an implementation built against it can be diagnosed from
its behaviour instead of guessed at.** This field was described as being *"in verifier consumption order"* — here in
this section's `Because:`, and in the upgrade specification §2.6 both in the `SequenceProof` struct comment and in
the prose below it. ⚠⚠ **The phrase is FALSE, and it is not a harmless imprecision: it names an implementation that
REJECTS HONEST BLOCKS from *n* = 4 upward.** **MEASURED** over every single-carried-leaf shape for *n* = 2…16:
**102 of 135 fold orders are NOT a subsequence of the canonical order.** Smallest counterexample — *n* = 4, carried
leaf 2: canonical `[0,2) [3,4)`, fold `[3,4) [0,2)`. ⇒ The cause is structural and permanent: a leaf in the tree's
**right** half takes `[0,k)` as its **last** sibling, and `[0,k)` sorts **first**. ⚠ The phrase is a leftover from the
dropped multiproof, where a single combined walk made "consumption order" meaningful; under per-leaf deduplicated
paths it describes nothing.
⛔⛔ **And the vector could not catch it.** MEASURED: **both** `proof/n5-carried-1-and-4` and
`proof/n8-carried-0-and-1-shared-nodes` verify under the wrong reading as well as the right one — so an implementer
who followed the phrase passed the whole vector and then rejected honest blocks in production. ⇒ **§6.6 is the case
that separates the two readings**, and it exists for no other reason.

### Requirement: the proof's contents and order are derived, never declared
The system MUST derive the needed interval set and its order from `LogCount` and the carried leaf indices alone,
and MUST NOT transmit interval tags, levels or ordering hints.

- **Because:** `LogCount` is inside the signed preimage, and the carried leaf indices come from the decoded record
  itself, so the interval set and any total order over it are a **total function of the signed count and the
  block's own bytes** — nothing about the addressing is declared on the wire. ⇒ **Zero wire bytes for addressing.**
  **MEASURED:** both implementations compute the same interval set independently, and the `dedupTable` keys equal
  `neededIntervals(carried, n)` in every driven case.
  ⚠ **REVISED IN REVISION 2.** Revision 1 justified this with *"each carried log's `LogIndex` is pinned to its
  proven leaf index"* — that pinning was D9's second MUST and **it is withdrawn**; it was never an independent
  constraint (§3.2, D9). The derivation argument survives without it, because what the interval set is a function of
  is the **signed count** and the indices the block already carries; it never needed those indices to have been
  independently authenticated. ⇒ **The conclusion stands on a repaired premise, not on the retracted one.**
- **Depth:** SPECIFIED, and driven.

### Requirement: verification is RFC 6962 §2.1.1 run once per carried leaf
The system MUST verify each carried leaf independently by reconstructing that leaf's full audit path from the
shared table by interval and folding it to the signed `LogsRoot`, and MUST reject the block if any leaf fails.

- **Because:** ⇒ **this IS the whole verification argument, and its shortness is the reason the multiproof was
  dropped** — the standing design constraint being that *the verification argument must stay short enough to be
  checkable*.
  Deduplication is a transport concern with no effect on what any path verifies.
- **Depth:** SPECIFIED, and driven — both implementations verify every carried leaf in every proof vector.

---

# 4. THE CLOSING SENTENCES — the ambiguities, discharged

⇒ The cryptographic-conformance review of this construction listed **15** places where two honest
implementations would diverge. **The multiproof-order one is dissolved by the maintainer's decision, not closed by
a sentence.** The rest:

⚠ **The rows are keyed by their subject.** That review numbered them, and the numbers are dropped rather than
reproduced: they resolve against a working document no reader of this repository holds, and the subject is what
each number stood for. **Fifteen rows, none dropped.**

| divergence | closed by |
|---|---|
| `Kind` values | §3.1 — `kindVoid = 0x00`, `kindPresent = 0x01` |
| endianness | §2 + §3 — **fixed-width big-endian throughout** |
| `nTopics` width | §3.2 — **4 bytes, uint32**, and why not uint8 |
| `lenData` width | §3.2 — **4 bytes, uint32** |
| `status` width | §3.2 — **8 bytes**, the declared type on both Go sides |
| failed receipts | §3.4's Requirement — **every log of every receipt** |
| what `LogCount` counts | same Requirement |
| n = 1 | §3.4 — **the RFC's rule; the root is the leaf hash** |
| root tag | §3.4 / **D8** — **no root tag; the RFC, not the in-repo precedent** |
| tag byte encoding | §3.1 — **raw ASCII, unprefixed, unterminated** |
| `NetworkId` twice | §2 — **once, hoisted after the tag** |
| void block fields | §3.5's Requirement — **zero, and in the preimage at full width** |
| empty-tree root | §3.4 — **the RFC's `keccak256("")`**, rejected alternative recorded |
| multiproof order | ⇒ **DISSOLVED** — the multiproof is dropped (maintainer, 2026-08-19) |
| node identity | §3.6 — **the leaf interval, not (level, index)** |

## ⇒ 4.1 The one that needed more than a sentence, and what it needed

**D6's serialisation.** ⚠ It is not that its *definition* was long — §3.6 is three lines. **It is that pinning it
surfaced a defect that no sentence would have found, and closing that needed a new requirement plus a driven
control.** That is §5.

---

# 5. ⛔⛔ A FREE-SPACE CHANNEL IN THE PROOF SERIALISATION — FOUND WHILE PINNING, AND MEASURED

⚠⚠ **This is a finding, not a restatement, and it is DRIVEN rather than inferred.**

**The defect.** Verification consults only the intervals on each carried leaf's own path. Those intervals are
derived, so **an EXTRA hash appended to `Hashes` is never consulted by any leaf** — verification still succeeds.
⇒ **Two byte-different blocks both verify.** That is precisely the *"consensus-relevant free-space channel"* the
upgrade specification §2.3 forbids for signatures, **in a transaction whose bytes are inside the block hash and the
AppHash's inputs** (the same document, §13.2).

**MEASURED, both directions, in implementation A:**

- With the count check **removed**, appending one 32-byte zero hash to an honest `n = 5` proof is **ACCEPTED** —
  the probe's guard fired: `panic: n5: EXTRA hash accepted — free-space channel open`.
- With the count check **present**, the same tampered table is **REJECTED**, as are a dropped hash and a corrupted
  hash.

⇒ ⚠ **That is the acceptance-criteria-must-fail-first rule applied to my own control: the tamper check was shown to
fire before being trusted.** Both implementations carry it; the check was then restored and the full comparison
re-run green.

## ⇒ The requirement that closes it

### Requirement: the supplied hash count is exactly the derived count
The system MUST compute the needed interval set from `LogCount` and the carried leaf indices, MUST require
`len(Hashes)` to equal that set's cardinality **before** performing any hashing, and MUST reject the block on any
mismatch.

- **Trigger class:** block-bytes.
- **Scenario:** GIVEN an otherwise-valid proof WHEN a proposer appends, removes or reorders a supplied hash THEN
  the block is rejected with `check=proof_shape`.
- **Because:** ⇒ **MEASURED above.** Without it the proof carries unconstrained free space; with it the whole table
  is positionally determined by authenticated data, so there is no free space at all. ⚠ It is also **the cheapest
  check in the construction** — an integer comparison ahead of every keccak, which satisfies the
  upgrade specification §7.4's *"caps are checked before any cryptography."*
- **Retired when:** never.
- **Depth:** SPECIFIED, and **driven in both implementations.**

⚠⚠ **NOTE FOR THE MAINTAINER, because this requirement is MINE and not in any input document:** it is a length comparison, not a cryptographic construction, so the standing rule against rolling our own cryptography is not engaged. ⛔ But it **is** a new consensus check and
therefore needs the classification discipline: **trigger class block-bytes ⇒ Class 1 ⇒ a REJECT is unanimous and
safe.** ⚠ **And it should get no `FinalizeBlock` half** — like the arity and continuity rules it cannot fire on an honest
node, so the prevote-time REJECT is the whole of its value, while a `FinalizeBlock` error is fatal post-commit on
the blocksync path. That asymmetry is the repository's own, recorded in the root `CLAUDE.md`'s Invariants section
and in `abci/rnk/docs/adr/adr-002-sequencer-outage-liveness.md`; the upgrade specification §8.1 states the same.

---

# 6. THE VECTOR — 33 CASES IN REVISION 1, 35 AFTER REVISION 2, 36 IN REVISION 3, **40** SINCE REVISION 4

⚠⚠ **READ §6.1 BEFORE TRUSTING A NUMBER IN §6.3.** The cases have **three different provenances** — revision 1's
two-implementation drive, revision 2's regeneration, and revision 3's §6.6 — and conflating them would overstate
what the vector establishes. ⚠ **And read §6.3.1 before trusting a fixture's INPUTS**, which for fourteen cases
existed nowhere until revision 3.

## 6.1 How it was driven, and what the controls were

### Revision 1's drive — the ORIGINAL, and it now describes the SUPERSEDED layout

| | |
|---|---|
| **Implementation A** | Go, hashing with **production go-ethereum** `crypto.Keccak256` (vendored fork `geth-rnk2-genesis@v0.0.0-20260706123415-ecb3dad88727`) |
| **Implementation B** | a **pure-Python Keccak-256** written for this pass |
| **Result** | **MEASURED: 33/33 cases present in both; 57 field comparisons; every one AGREED.** Exit 0 |

⛔ **That drive was over the `logIndex`-IN leaf preimage.** It remains a valid statement about revision 1's layout —
which is why revision 1's digests are retained in §6.3's second column — and it says **nothing** about the ratified
layout's values.

### Revision 2's regeneration — what each class of value now rests on, at the strength it was obtained

| class | count | provenance |
|---|---|---|
| **unchanged by the layout change** — the three keccak controls, the three tag byte strings, `tree/n0-empty-root`, `cert/void-zero-leaf`, `cert/max-width` | 9 | ⇒ **Revision 1's two-implementation drive still applies verbatim**, because none of them routes through a leaf. ⛔ **Their values MUST be identical in both columns; a difference is an error, not a regeneration.** |
| **every `leaf/*`, `tree/n1..n1024` and `cert/present-*` value** | 22 | ⇒ These are the **24 digests committed in this repository** — today `abci/rnk/sequence_logs_tree_test.go` (implementation A, production go-ethereum keccak, in a committed test) — independently recomputed **twice** by byte assemblies written from the field order and hashed with `cast keccak` (implementation C): once by the cryptographic-conformance peer review of that work — 2 075 keccak calls, **32 checks / 0 failures** — and again while regenerating this file, as a transcription guard — **26 checks / 0 failures**. |
| **the four interval hashes inside the two `proof/*` cases**, and §6.6's three | 7 (inside 3 cases) | ⚠ **WEAKER, and still labelled as such — but LESS weak since revision 3.** There is still no proof code in `reactive-tornado`, so these have **no implementation-A counterpart**. ⇒ **What changed: all four of the original interval hashes were reproduced by a second party** — a TypeScript implementation written from this document's prose, by a different byte assembly, hashed by two libraries that are neither A, B nor C (§6.4). ⛔ **Superseded, kept visible:** this row read *"they rest on implementation C alone — one byte assembly, one hash tool … two-implementation agreement is **not** claimed for them."* **That claim is withdrawn for the four; two-implementation agreement IS now claimed.** §6.6's three carry the same standing (two instruments, no A), and two of them coincide with `tree/*` values that do have an A counterpart. |

⚠ **The positive control on the regeneration, and it is the one that matters.** The peer review re-ran its own
instrument with `logIndex` re-inserted and matched **23 of 23** of revision 1's values. ⇒ **A 4-byte layout change
moves every leaf-dependent digest and the instrument produced the OTHER correct answer rather than the same one.**
It fires; it is not a green light that would be green either way. And the discriminating detail that makes the
split legible: **exactly the values that route through a leaf differ between the two columns, and exactly the
values that do not, do not.** That is the signature of a leaf-layout change and of nothing else.

**Controls, all four kinds:**

1. ⇒ **Absolute (anchors the hash):** three `cast keccak` values are hard-coded in the comparator and matched by
   **both** implementations — `keccak256("")`, `keccak256("abc")`, `keccak256(0x00)`. ⚠ **A drift in both
   implementations at once is still caught by these.**
2. ⇒ **Cross-implementation (anchors the encoding):** every field of every case, byte for byte.
3. ⇒ **Negative control on the comparator itself.** MEASURED: flipping **one function** in A — `be64` from
   big-endian to little-endian — reddens the comparison across **every leaf, tree, proof and certificate case**.
   ⚠⚠ **And the instructive part: the three absolute controls did NOT redden**, because they do not route through
   `be64`. ⇒ **The two instruments catch different failure classes, and neither is sufficient alone** — which is
   the upgrade specification §16.4's whole thesis, observed on our own bench. The perturbation was then reverted and the restore verified by
   re-running green.
4. ⇒ **Negative control on the free-space check** (§5), fired and then closed.

⚠⚠ **THE LIMIT OF THIS DRIVE — NARROWED IN REVISION 3, and the narrowing is measured.** As written, the **hash**
was genuinely independent (production geth vs a from-scratch Python Keccak) while the **construction** was one author
writing the same design twice. ⇒ **That is no longer the whole story: a second implementation, written in TypeScript
from THIS DOCUMENT'S PROSE by a party that read no Go, matched 61 assertions with 0 disagreements and made no
adjustment to reach them** (§6.4). **The specification is
sufficient for the ENCODING; that is established from outside.**
⛔ **What still is NOT closed, and the distinction is the point:** that pass is a second implementation of the same
spec by the same organisation. It closes *"is the prose sufficient"*; it does not close *"does the issuer that will
actually sign agree"*, which needs the Sequencer side to build against these numbers. **That remains outstanding and
is the whole point of the committed artifact.**
⚠ **And it was insufficient for the FIXTURE**, which is the finding that produced §6.3.1: 13 of the 35 cases could
not be attempted at all, because their inputs were a count, a length or a name.

## 6.2 The case list — every case the request asked for, and why each is here

| case | pins |
|---|---|
| `control/keccak-empty` · `control/keccak-abc` · `control/keccak-single-zero-byte` | the hash itself, against `cast` |
| `tag/leaf` · `tag/node` · `tag/cert` | the three tags' exact bytes, so a second implementation can check its own literals |
| `tree/n0-empty-root` | ⇒ **n = 0**, the case every `void` certificate hits |
| `tree/n1-root` (+ `equals_leaf0`) | ⇒ **n = 1**, and that the root **equals leaf 0** |
| `tree/n2..n9-root` | every small *n*, **including the non-powers of two** 3, 5, 6, 7, 9 |
| `tree/n1024-root` | a large power of two, and the operating point |
| `leaf/all-zero-no-topics-no-data` | ⇒ **zero integers, zero topics, empty `data`** together |
| `leaf/leading-zero-ints-empty-data` | ⇒ **the leading-zero class the TS/Go seam has demonstrably drifted on** |
| `leaf/status-0` · `leaf/status-1` | ⇒ that **`status` is bound** — one log, encoded twice, at each of the two observed status values. ⛔ **`leaf/status-1` was named `leaf/status-1-failed-receipt-still-in-tree` and the old name was self-contradictory:** in the EVM a *failed* receipt has `status == 0` (`ReceiptStatusFailed`), and §6.5 says so explicitly, so the old name asserted both `status = 1` and *this is the failed one*. ⇒ The failed-receipt-is-in-the-tree property is pinned by `flatten/multi-receipt-mixed-status` (§6.5) and by §3.4's Requirement, not by this pair. |
| `flatten/multi-receipt-mixed-status` · `flatten/wire-width-normalisation` | ⇒ **ADDED IN REVISION 2 — see §6.5.** The two cases that close revision 1's largest hole: `Sequence` → ordered leaves, and the wire-width normalisation that conversion applies |
| ⚠ **THE HOLE REVISION 1 LEFT, recorded because the fix is what §6.5 is** | ⇒ **nothing in revision 1 pinned `Sequence` → ordered leaves.** Every `leaf/*` case above states a leaf's fields directly; no case starts from a multi-receipt block and asks for its root. That JOIN — which leaves, in which order, each attributed which owning receipt's `status` and `txHash` — is what an issuer must actually agree with us on, and MEASURED on this repository, at the tree state that first committed the certificate store, three corruptions of it (every `txHash` zeroed, `status` forced to a constant, receipts flattened in reverse) left its whole suite green. ⇒ **Two cases the committed artifact MUST add: one root over an explicit multi-receipt sequence** (mixed statuses, unequal log counts per receipt, one receipt with no logs, distinct `txHash` per receipt — a single-receipt fixture cannot detect a reversed order), **and one root over deliberately mis-width inputs** (a 31-byte and a 33-byte topic, a 19-byte and a 21-byte address, a zero-length topic), pinning the `common.BytesToHash`/`BytesToAddress` left-pad-and-truncate rule that §7.2 flags. ⇒ **Both are now §6.5, and both are committed as tests here** (`abci/rnk/sequence_logs_tree_test.go`). |
| `leaf/topics-0` · `-1` · `-4` · `-5` | ⇒ **min, one, the EVM maximum, and BEYOND it** — the case that would break a `uint8` `nTopics` |
| `leaf/max-width-ints` | every integer at its type maximum |
| `leaf/data-512B-multiblock` | ⇒ **`data` crossing keccak's 136-byte rate boundary** — multi-block absorption |
| `proof/n5-carried-1-and-4` | ⇒ **the upgrade specification §2.7's named case: a sparse kept-set over a non-power-of-two *n*** |
| `proof/n8-carried-0-and-1-shared-nodes` | ⇒ **that deduplication actually deduplicates** — MEASURED 6 independent path hashes → **4** |
| `proof/n5-carried-2-fold-order-differs-from-table-order` | ⇒ **ADDED AFTER THE SECOND-PARTY PASS — see §6.6.** That the transmitted order is **not** the fold order. ⛔ It is the only proof case that discriminates: MEASURED, both cases above verify under the false *"in verifier consumption order"* reading as well as the right one. |
| `cert/void-zero-leaf` | ⇒ **a void certificate**: zero block fields, `LogCount = 0`, `LogsRoot` = the empty constant |
| `cert/present-3-logs` | a normal certificate over a 3-leaf tree |
| `cert/present-3-logs-kind-flipped-to-void` | ⇒ that **`Kind`'s numeric value is inside the preimage** |
| `cert/max-width` | every certificate field at its maximum |
| `sig/present-3-logs-valid` · `sig/present-3-logs-recovery-id-in-the-27-28-convention` · `sig/present-3-logs-recovery-id-flipped` · `sig/present-3-logs-high-s` | ⇒ **ADDED IN REVISION 4 — see §6.7.** The first signature cases in the vector, over the `cert/present-3-logs` digest, signed by the clearly-marked test key §6.7 states. ⛔ **The recovery-id pair is the point**: an implementation on the `{27,28}` convention gets the OPPOSITE verdict on both, so the convention cannot be got wrong and still pass. The other two catch the low-S rule and a verifier that ignores the carried recovery id. |

## 6.3 The pinned values

⚠ **The machine-readable form of this vector is `abci/rnk/sequence_encoding_vector.json`**, which carries every
case as data, including the preimages, interval lists and proof hashes. ⚠ **It is a transcription of the tables
below and not a second authority — this file governs**, and the artifact says so itself. ⛔ **Revision 1's probe
tree also emitted two machine-readable vectors; they describe the SUPERSEDED layout, nothing has regenerated them,
and they are not in this repository** (§6.4).

⚠⚠ **HOW TO READ THE TWO COLUMNS.** The left value is **normative** — the ratified layout, `logIndex` out. The right
column is revision 1's value for the same case, **retained and NOT normative**, so that an implementation built
against revision 1 can be diagnosed from its digests rather than guessed at. `—` means the case touches no leaf and
therefore has **one** value in both layouts; ⛔ **a `—` row whose value ever appears to have changed is an error.**

| case | value — RATIFIED (`logIndex` OUT) | superseded (revision 1, `logIndex` IN) — ⛔ NOT normative |
|---|---|---|
| `control/keccak-empty` | `0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470` | — |
| `control/keccak-abc` | `0x4e03657aea45a94fc7d47ba826c8d667c0d1e6e33a64a036ec44f58fa12d6c45` | — |
| `control/keccak-single-zero-byte` | `0xbc36789e7a1e281436464229828f817d6612f7b477d66591ff96a9e064bcc98a` | — |
| `tag/leaf` | `0x726e6b2e7365716c6561662e7631` | — |
| `tag/node` | `0x726e6b2e7365716e6f64652e7631` | — |
| `tag/cert` | `0x726e6b2e736571636572742e7631` | — |
| **`tree/n0-empty-root`** | **`0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470`** | — |
| `leaf/all-zero-no-topics-no-data` | `0x75cd01e8acef921deb743e60840f7c6bea1f5f2fef3761ced72602140bbe51c9` | `0x26f91452aeee7b4b428bc893e12900c58ef43935df178bfd32836e21aa739c79` |
| `leaf/leading-zero-ints-empty-data` | `0x02da1614e4b015908366b4dd795ec28b8d6341b95b224805f9b543db13de9923` | `0x23a8f900702311041cc884a8c98dc77ba2b1d2df5936337d2b81e9bdc45b2dc4` |
| `leaf/status-0` | `0x68ffaa8f7ba4ded43b7d45c1806185df23b4f3a4caf7d6f8f97a1169457f04a8` | `0xf63624d2da20fdd9004396aba525d6bea1313499aed0f9cc58e318c73790742f` |
| `leaf/status-1` (renamed; was `leaf/status-1-failed-receipt-still-in-tree`) | `0xc2cbe1e0fda342f9d89460332dcd9aca4ebbbd9a564b52cbb4d2332f673b251f` | `0x4dea8396192517cdda39eb3ca82391841bb13c44acd5b631cbf5292e9b53d396` |
| `leaf/topics-0` | `0x2f3e02668dea2028dcb35f402bd13fcb8a35d78a173a75323c00c6720c0750ec` | `0x080d2d60db04e09f9d54d3143d144658b05cb91f1bd1981ea8300cbb76c0c5cb` |
| `leaf/topics-1` | `0x3aaea2b5147299b1471ac1cdd8df1674479cfe5d390c5f5b4edb6dce73ceb927` | `0x8a0de78df2fd4a841c4b6b0568e51d38751761d462332e5296a90d24c6f68278` |
| `leaf/topics-4` | `0x6d19022366e13bb28324973d9461618d5a79f67496f699da9b0dfa36b11fa99e` | `0x9cb1ee1f4fad9e5b2e5d6c49803cc32bcdb1795e5daf29c4f9fea863b841d134` |
| `leaf/topics-5` | `0x9d7b1cc84a6e35a155e121b8689ff09582f250a5b519a6180eddd55677d39295` | `0xca94e02059569e6784fc2e70be3c3790859638ba602fefa84b0b48a501f4f983` |
| `leaf/max-width-ints` | `0x81632063816914cbd1a19d0f458ba20875ad07679e36376fac914e06de8822c1` | `0x767e45170b659506336c901aed4120c7c362bbc93fa6f8001dbe576e089ec124` |
| `leaf/data-512B-multiblock` | `0x83ec2817ff134993e48dd4c9dba10a546fef85cc43ce1574bb44ee251db164a8` | `0x4828c1bcf64cf8613ab52f5bd3df5947f0e8b257962cea95d2f7fbd0266ff89b` |
| **`tree/n1-root`** (= leaf 0) | **`0x384c59089c8b8f62c2cfc3371759f4b310f280ad9c7c104958f0ed814a07280c`** | `0x4562c33ab65ca1667acb0f2b27c0c4cdcf0830798e8045ee7a3904c11e9cebe1` |
| `tree/n2-root` | `0x70234db48f8bf93dd3ce3697907e8a55b7c2db1d0e32e962801d984bf679f2ea` | `0xfa00917fa389c93a4b881897f9e9aee326b8123a74a24e62c26dabfd08adf6b8` |
| `tree/n3-root` | `0x37e938814ba430e5cfd9f95b8347ccf131ed70ccf5b1508da536269dce08b86b` | `0x35402f79c8b8167bbacb7ef01f6b9990ace19453e76641f593a1f9b925b5c0e8` |
| `tree/n4-root` | `0x78ea4bd1d9613132b8a9575d1ef81b4f9619f7ba6f3b9000e855d86cff5ec50a` | `0x510d2ba38b95433a0cebe2cebacbff63d5c35f7d9d1d5ea324dfc73bea2123e0` |
| `tree/n5-root` | `0x23ed8d42b4a8579bd3a25a83d7622f771c40288ea6ae38fa4329e450ccd3e388` | `0xe6c0994a300d92bbe44847b3d7471c65f3ebc31b2ab23174e3aede064017e79f` |
| `tree/n6-root` | `0xb96f1b79377e730929c45e8b18ca8a27dab0f631de5353fba549511f854e405f` | `0xd37404a131f55ad4985777c3580cbfaef3c1edc3161d14a0de65c27c133ab6c0` |
| `tree/n7-root` | `0xd9dd638e60699de2a7cbc7c19aa99647fff7aa6fa32d340abd20f776f5baf10b` | `0xdac39013c7363c42cc908c7c7dd65f12df7783b839a446ae450062075b527a6c` |
| `tree/n8-root` | `0x97e20e75e216ea00ac7042e58581809f25089063269232ca712172ca07274800` | `0x4a55ba4a8c800e45c8dd832f86e7262325bcd6a1fd449d255695ccad5965c853` |
| `tree/n9-root` | `0x4fe060c411d303a0140f3af069206cc43f8f1dec0d8945963db9a93c2d477e31` | `0x351e151e998a5990400800c49ff8b85dbbb172a26aa02de2a40e6f42efec7991` |
| `tree/n1024-root` | `0x1f6d32df0e7bc2866f7ed9cb5075bdb51671d60088d777f7925ceb18342a9be5` | `0x919d5cf076ac5f919796311e95e15ce9bcaec5d87feb48a15e56a9b0867a9d1c` |
| `cert/void-zero-leaf` | `0x29cdbf043332f5457dc292bbe58e9e2d47f4ce8c425b624e9b088900e1704baa` | — |
| `cert/present-3-logs` | `0xd14177b38a313090746b0a11245510712b85ec7c47e863a66db4e84bc4d1ea39` | `0x2f98a9874e1b4bc3cb2e148d57867109ca786466105c69e812809f2ff7343d79` |
| `cert/present-3-logs-kind-flipped-to-void` | `0x7e182a8c1a741329094fb219753f603dbefb0cf231aa44982f4d3f4a7943e6b3` | `0xec464a665dda21d6e5096650dd4b60bfa9188b457774c467ce9eea42f85a84a1` |
| `cert/max-width` | `0xcaf119688d33717aeddd01aa4a434c1f4c7b724b6c5d8d49a5ccf994289f2986` | — |

⚠ **The `—` rows are the cross-check, not a convenience.** Nine of the 33 cases depend on no leaf; all nine came out
identical in both layouts. **Everything that routes through a leaf differs; nothing that does not, does.**

**The two proof cases in full.**

⚠ **Both proof cases were regenerated for the ratified layout, and they carry §6.1's weaker label** — no
implementation-A counterpart exists, because `reactive-tornado` has no proof code yet.

`proof/n5-carried-1-and-4` — `LogCount = 5`, carried `{1, 4}`, root
`0x23ed8d42b4a8579bd3a25a83d7622f771c40288ea6ae38fa4329e450ccd3e388` (= `tree/n5-root`, ✓ internally consistent),
`expected_hash_count = 4`:

| interval | hash — RATIFIED | superseded (revision 1) — ⛔ NOT normative |
|---|---|---|
| `[0,1)` | `0x384c59089c8b8f62c2cfc3371759f4b310f280ad9c7c104958f0ed814a07280c` | `0x4562c33ab65ca1667acb0f2b27c0c4cdcf0830798e8045ee7a3904c11e9cebe1` |
| `[0,4)` | `0x78ea4bd1d9613132b8a9575d1ef81b4f9619f7ba6f3b9000e855d86cff5ec50a` | `0x510d2ba38b95433a0cebe2cebacbff63d5c35f7d9d1d5ea324dfc73bea2123e0` |
| `[2,4)` | `0x6f17319bb92ae728326c4e8237525348b9fa1f7b0f4a7cde1febb98194000db6` | `0xa08718a64f9d57ef8e3139cf7c70ee8fa083b4e33d0811dd56eb440ed94b9c3e` |
| `[4,5)` | `0x90debd54d3ebd4a2fbe247b930f81b7c5a773d4871ebf9bf2188ce4e6836df2d` | `0x74d3741010110a64e3f4ba51f6ce75c7ff6d3dc06f40f2624fc81d3f9a7ff314` |

⚠⚠ **This case makes the dropped multiproof's saving concretely visible, and it is worth one sentence:** `[0,4)`
is **derivable** by the verifier from `[0,1)`, `[2,4)` and carried leaf 1, so a minimal multiproof would omit it.
⇒ **That one redundant hash IS the 3.05 KB-per-carried-sequence price the maintainer accepted**, in miniature.
⛔ Do not "optimise" it away — removing it reintroduces the combined walk and with it CVE-2023-34459's class.

`proof/n8-carried-0-and-1-shared-nodes` — `LogCount = 8`, carried `{0, 1}`, root
`0x97e20e75e216ea00ac7042e58581809f25089063269232ca712172ca07274800` (= `tree/n8-root` ✓),
**independent path hashes 6 → deduplicated 4** (MEASURED, and unaffected by the layout change: deduplication is a
property of the interval set, not of the leaf bytes), `expected_hash_count = 4`:

| interval | hash — RATIFIED | superseded (revision 1) — ⛔ NOT normative |
|---|---|---|
| `[0,1)` | `0x384c59089c8b8f62c2cfc3371759f4b310f280ad9c7c104958f0ed814a07280c` | `0x4562c33ab65ca1667acb0f2b27c0c4cdcf0830798e8045ee7a3904c11e9cebe1` |
| `[1,2)` | `0x0a078127169f37f51eebef2b2f25b0a6f9af6045bb11e120205bf375508fff1e` | `0x4f12b8b0d6b6d3d2f1b6dc1facea160ebe4a58b35aed4a2f5b987d92041be98b` |
| `[2,4)` | `0x6f17319bb92ae728326c4e8237525348b9fa1f7b0f4a7cde1febb98194000db6` | `0xa08718a64f9d57ef8e3139cf7c70ee8fa083b4e33d0811dd56eb440ed94b9c3e` |
| `[4,8)` | `0x4c663bf5e4812b7babc6798c8c85d6f2aede7fb84b573993c27069eacdb8036d` | `0xfdf1d94daec9b0c05fdcded7d66036ea0725a5bedec664c6b9ec517c612c2f84` |

⚠ **The vector's leaf inputs are generated, not hand-written.** The generator is the rule stated here, and it is
the rule `abci/rnk/sequence_encoding_vector.json` carries as parameters plus explicit leaves — leaf *i* of a
sequence has
`status = 1`, `txHash = (0x10+i)×32`, `address = 0x20×20`, two topics
`(0x30+i)×32` and `(0x31+i)×32`, and `data = (i mod 256)` repeated `i mod 7` times, with `seq = 42` (or 101 for the
`cert/present-3-logs` tree). ⚠ **Revision 1's description of this generator also said `logIndex = i`; the record
still carries an index, it is simply no longer hashed.** ⛔ **The committed artifact must carry these inputs
explicitly, not the generator** — a fixture whose inputs are code is a fixture two implementations cannot
independently reproduce. ⚠ **And this is not hypothetical arithmetic:** reproducing `tree/n1024-root` requires
replicating Go's `byte(0x10+i)` and `topicByte+byte(i)` **wrapping mod 256** for *i* up to 1023, which a
TypeScript implementer handed this file would have to infer from Go's non-constant-conversion rules.
⇒ ⚠ **MEASURED IN REVISION 3: this paragraph turned out to be sufficient** — a second party working from it alone
reproduced `tree/n1024-root`, so the warning did its job. ⛔ **The rule it states is nevertheless not satisfied by
prose about code, and the ten `leaf/*` and four `cert/*` cases were the ones it failed: their inputs follow from no
rule at all, and §6.3.1 now states them.** The generator stays only for `tree/*` and `proof/*`, where the inputs
genuinely ARE a rule and writing 1024 leaves out as hex would trade a working description for bulk.

### 6.3.1 ⇒ THE FIXTURE INPUTS — the ten `leaf/*` and four `cert/*` cases, stated

⚠⚠ **WHY THIS SECTION EXISTS, and it is not tidiness.** A second party built this construction in TypeScript from
this document's prose alone and **matched 61 assertions with 0 disagreements — and could not attempt 13 of the 35
cases at all**, because the cases above state a *count*, a *length* or a *name* where an implementer needs *bytes*.
⇒ **A fixture whose inputs are unstated contributes nothing to two-party agreement**, whatever its digest.
⛔ **And that is measured, not argued:** the second party's search then brute-forced 26.3 M trial digests and
recovered three of the thirteen; the other ten resisted, and `leaf/topics-0` — which has *no* topics, so the search
covered **every** unknown field it has — resisted a sweep over every uniform and incrementing fill. ⇒ **The bytes
are simply arbitrary and there is nothing in this document to infer them from. A second party can only be told.**

⚠ **Notation, and it is §6.5's, already consumed correctly by a second party (MEASURED):** `0xbb`×32 is the 32-byte
value whose every byte is `0xbb`. Nothing below is elided. **The same values with every byte written out are in
`abci/rnk/sequence_encoding_vector.json`**, which is the language-neutral shape the upgrade specification §3.4
asks for; ⚠ that artifact is a **transcription of these values, not a second authority** — this table governs.
⚠ A working transcription file preceded it and is superseded by it.

⛔ **THE CONTROL, and it is what makes transcription safe.** Every input below was fed to an encoder that never saw
the node's Go — the second party's own TypeScript encoder, hashing through two cross-checked keccak libraries — **and to
a third, an independent byte assembly hashed by `cast keccak`.** Each reproduced the digest **already committed** in
§6.3's left-hand column. **MEASURED: 15/15 and 18/18, no digest moved, nothing above was edited.** ⚠ And the control
was shown to FAIL first: perturbing one transcribed `seqNumber` and one `Kind` reddened exactly those two rows.

**The ten `leaf/*` cases.** Every case's `preimage length` is `90 + 32·nTopics + lenData` and is given so a
mistyped row is caught by arithmetic before it is caught by a hash.

| case | `seqNumber` | `status` | `txHash` | `address` | `topics` | `data` | preimage len |
|---|---|---|---|---|---|---|---|
| `leaf/all-zero-no-topics-no-data` | 0 | 0 | `0x00`×32 | `0x00`×20 | *(none)* | *(empty)* | 90 |
| `leaf/leading-zero-ints-empty-data` | 1 | 0 | `0x11`×32 | `0x22`×20 | `0x33`×32 | *(empty)* | 122 |
| `leaf/status-0` | 7 | 0 | `0xaa`×32 | `0xbb`×20 | `0x40`×32, `0x41`×32 | `0xdead` | 156 |
| `leaf/status-1` | 7 | **1** | `0xaa`×32 | `0xbb`×20 | `0x40`×32, `0x41`×32 | `0xdead` | 156 |
| `leaf/topics-0` | 9 | 1 | `0xc1`×32 | `0xc2`×20 | *(none)* | `0x01` | 91 |
| `leaf/topics-1` | 9 | 1 | `0xc1`×32 | `0xc2`×20 | `0x50`×32 | `0x01` | 123 |
| `leaf/topics-4` | 9 | 1 | `0xc1`×32 | `0xc2`×20 | `0x50`×32, `0x51`×32, `0x52`×32, `0x53`×32 | `0x01` | 219 |
| `leaf/topics-5` | 9 | 1 | `0xc1`×32 | `0xc2`×20 | `0x50`×32, `0x51`×32, `0x52`×32, `0x53`×32, `0x54`×32 | `0x01` | 251 |
| `leaf/max-width-ints` | `18446744073709551615` = 2⁶⁴−1 | `18446744073709551615` = 2⁶⁴−1 | `0xff`×32 | `0xff`×20 | `0xff`×32 — ⚠ **ONE topic, not four** | `0xff` — ⚠ **one byte** | 123 |
| `leaf/data-512B-multiblock` | 11 | 1 | `0x01`×32 | `0x02`×20 | `0x60`×32 | ⇒ the 256 byte values `0x00 0x01 … 0xff` in ascending order, **twice** — 512 bytes | 634 |

⚠ **`leaf/status-0` and `leaf/status-1` are the SAME log**, and the table now shows that rather than implying it:
the pair's whole content is that `status` is bound, so every other field must be equal between them.
⚠ **`leaf/max-width-ints` is the one case whose two qualifiers matter more than its fills.** *"Every integer at its
type maximum"* determines the two `uint64`s; it says nothing about the topic count or the data length, and the
fixture holds **one** topic and **one** data byte. A reader who assumed four topics — the EVM maximum, and what
§6.3's generator uses — gets a different digest.

**The four `cert/*` cases.** ⚠ `Kind` is written as its byte, not as a name, because that is where the one measured
two-party divergence happened. ⚠ **Integers are written in full decimal, not as `2⁶⁴−1`**, so that no reader and no
parser has to evaluate an expression: `18446744073709551615` is 2⁶⁴−1 and `4294967295` is 2³²−1.

| case | `NetworkId` | `SeqNumber` | `Kind` | `KeyId` | `ChainId` | `BlockHash` | `ParentHash` | `Number` | `Time` | `LogCount` | `LogsRoot` |
|---|---|---|---|---|---|---|---|---|---|---|---|
| `cert/void-zero-leaf` | 1597 | 100 | `0x00` | 0 | 0 | `0x00`×32 | `0x00`×32 | 0 | 0 | 0 | `tree/n0-empty-root` |
| `cert/present-3-logs` | 1597 | 101 | `0x01` | 7 | 1 | `0xab`×32 | `0xcd`×32 | 21000000 | 1755000000 | 3 | `0x8c6e26c25502a62aa23c5ae614f1c237da67c382b9844b539275ea3da07011cf` |
| `cert/present-3-logs-kind-flipped-to-void` | 1597 | 101 | **`0x00`** | 7 | 1 | `0xab`×32 | `0xcd`×32 | 21000000 | 1755000000 | 3 | *(the same root)* |
| `cert/max-width` | `18446744073709551615` | `18446744073709551615` | ⚠⚠ **`0x01`, NOT `0xff`** | `4294967295` | `18446744073709551615` | `0xff`×32 | `0xff`×32 | `18446744073709551615` | `18446744073709551615` | `4294967295` | `0xff`×32 |

⛔⛔ **`cert/max-width`'s `Kind = 0x01` is the strongest single argument for this whole section, so it gets its own
note.** The case is glossed *"every certificate field at its maximum."* `Kind` is a `uint8`, so its **type** maximum
is `0xff`; its maximum **defined** value is `kindPresent = 0x01`. The fixture holds `0x01`. ⇒ **The second party read
the phrase literally, chose `0xff`, flagged it as the one judgement where it expected a real implementer to land on
the other side — and was wrong, in exactly the direction it flagged.** ⚠⚠ **That is a genuine two-party divergence
on the first attempt, caused by nothing but an unstated input**, on a case that ought to be among the easiest in the
vector. No reading of *"every field at its maximum"* recovers `0x01`; only writing it down does.

⚠ **`cert/present-3-logs`'s `LogsRoot` is §6.3's generator at *n* = 3, `seq = 101`**, and it is stated above as a
value so the certificate is checkable without first reproducing a tree. Its three leaf hashes, for the same reason:

| leaf | hash |
|---|---|
| 0 | `0x3db5b616d7db1247cd17a8a48674363d6e3b8a6e6749083a17fb06a8423fada1` |
| 1 | `0x37473f7933f7dcde99f19ed138cec6c4996df33fd052b4165262739e1b6a5bc7` |
| 2 | `0xa2cb7af72b7fa10761a89f9a4948feb871f7307421a32fae5098b256b3aa5715` |

### 6.3.2 ⇒ ⛔ `cert/present-3-logs`' SAME-WIDTH FIELDS ARE PAIRWISE DISTINCT, and that is load-bearing

⚠⚠ **A permuted encoder passes a certificate fixture whose same-width fields hold EQUAL values**, because swapping
their contents leaves the 159-byte preimage byte-identical. `cert/void-zero-leaf` has all five `uint64`s at 0 and
`cert/max-width` has them all at 2⁶⁴−1, so **neither can see a `Number`/`Time` transposition, a
`BlockHash`/`ParentHash` transposition, or a `KeyId`/`LogCount` transposition** — MEASURED: **5 of 10 same-width
swaps are invisible to those two fixtures**, which is what a second party holding only §6.3's names and digests was
left with, because those two are the only certificates it could reach at all.

⇒ ⚠ **`cert/present-3-logs` closes every one of them, and stating its inputs is the whole of the fix.** Its five
`uint64`s are 1597 / 101 / 1 / 21000000 / 1755000000, its two `uint32`s are 7 and 3, and its three 32-byte fields
are `0xab`×32, `0xcd`×32 and the generator root — **pairwise distinct in every width class.** **MEASURED: all 14
same-width transpositions move the digest; 0 of 14 are invisible.**

| transposition | `cert/void` + `cert/max-width` alone | `cert/present-3-logs` |
|---|---|---|
| `NetworkId` ↔ `SeqNumber` | caught | digest moves ✓ |
| `NetworkId` ↔ `ChainId` | caught | digest moves ✓ |
| `NetworkId` ↔ `Number` | *(not enumerated)* | digest moves ✓ |
| `NetworkId` ↔ `Time` | *(not enumerated)* | digest moves ✓ |
| `SeqNumber` ↔ `ChainId` | *(not enumerated)* | digest moves ✓ |
| `SeqNumber` ↔ `Number` | caught | digest moves ✓ |
| `SeqNumber` ↔ `Time` | *(not enumerated)* | digest moves ✓ |
| `ChainId` ↔ `Number` | ⛔ **INVISIBLE** | digest moves ✓ |
| `ChainId` ↔ `Time` | ⛔ **INVISIBLE** | digest moves ✓ |
| `Number` ↔ `Time` | ⛔ **INVISIBLE** | digest moves ✓ |
| `BlockHash` ↔ `ParentHash` | ⛔ **INVISIBLE** | digest moves ✓ |
| `BlockHash` ↔ `LogsRoot` | caught | digest moves ✓ |
| `ParentHash` ↔ `LogsRoot` | caught | digest moves ✓ |
| `KeyId` ↔ `LogCount` | ⛔ **INVISIBLE** | digest moves ✓ |

⛔ **So do not "simplify" this fixture's values, and do not add a second pairwise-distinct certificate case.** The
first would silently reopen the five positions — including the `Number`/`Time` and `BlockHash`/`ParentHash`
orderings, the two the specification took the trouble to argue for (the upgrade specification §2.3's *"header
fields the derivation never reads are bound anyway"*). The second would imply this case lacks the power it has. ⚠ **This
property is a property of the VALUES, so it is invisible in the digest and has to be written down** — it is exactly
the shape §6.5's `flatten/*` fixture asserts about itself for the same reason.

⚠ **One residual, stated so it is not mistaken for closed:** `cert/present-3-logs`'s digest also depends on the leaf
encoding, through its `LogsRoot`. So a *simultaneous* leaf error and certificate-layout error is not isolated by
this case alone — it is isolated by the ten `leaf/*` cases above, which move under a leaf error and not under a
field transposition. ⇒ **Diagnosis is available; it is just not available from one row.**

## 6.4 The instruments behind these numbers — and ⛔ not one of them is in this repository

⚠⚠ **This section is the honest limit of this file's provenance, and it is stated first because a reader who
assumes otherwise will look for a script to re-run and find none.** The comparators, revision 1's two
implementations, revision 2's regeneration scripts and the second party's TypeScript encoder were all working
artifacts in a private area. ⛔ **None is committed here, so none is cited by path**, and re-deriving these digests
is not something this repository can do. What each established is recorded below — and in §6.1, which splits it by
class of value rather than by instrument.

| instrument | what it was | what it established |
|---|---|---|
| **A** | Go, hashing with the production go-ethereum `crypto.Keccak256` of the vendored fork | revision 1's whole column, and — as a committed test in this repository — the 22 regenerated values (§6.1) |
| **B** | a pure-Python Keccak-256 written for revision 1's pass, independent of A | the same column, by a second hash implementation |
| **the comparator** | a script diffing A against B field by field, with three `cast keccak` values hard-coded as absolute anchors | **33/33 cases, 57 field comparisons, all AGREED**, plus the four controls listed in §6.1 — including the `be64` perturbation that reddened every leaf-routed case and **not** the three anchors |
| **C** | an independent byte assembly hashed by `cast keccak` (foundry 1.5.1, Rust); it implements no hash of its own, which is the point of the route | revision 2's regeneration and its transcription guard, **26 checks / 0 failures**; §6.5's two `flatten/*` cases, produced **before** the Go test that then passed first time |
| **the review's instrument** | the cryptographic-conformance review's own byte assembly, also over `cast keccak` | **2 075 keccak calls, 32 checks / 0 failures** — and the positive control that re-inserted `logIndex` and matched **23 of 23** of revision 1's values, which is what shows the instrument fires |
| **the second party** | a TypeScript encoder written from this file's prose by a party that read no Go, over two cross-checked keccak libraries | **61 assertions, 0 disagreements, 13 cases unreachable** — the finding that produced §6.3.1; the four original proof-interval hashes; and §6.7's signature matrix |

⛔⛔ **REVISION 1's PROBE TREE MUST NOT BE TREATED AS A SOURCE OF A CURRENT VALUE, and it no longer can be.** Its
two implementations hash the `logIndex`-IN leaf, so it reproduces the **superseded** right-hand column of §6.3. ⇒ It
is the audit trail for that column and for §5's free-space control, and for nothing else. ⚠ That is why §7.3 item 7
says regenerate it or retire it: a probe tree that reproduces the wrong column is a trap for the next reader, and
it is now a trap a reader of this repository cannot open at all.

⇒ ⚠ **What this repository DOES carry, and it is the check that matters going forward.**
`abci/rnk/sequence_encoding_vector_test.go` runs this package's production functions against every case of
`abci/rnk/sequence_encoding_vector.json`, and `abci/rnk/sequence_logs_tree_test.go` pins the same roots as Go
literals with a test that the two agree. ⇒ That is a standing, re-runnable comparison between the node's
implementation and this file's transcribed values — ⛔ **it is not a re-derivation of the values themselves.**
Which is exactly why this file has to be here: without it the transcription has no reference, and "a digest that
appears to have moved is a finding" has nothing to be a finding against.

## 6.5 THE TWO CASES ADDED IN REVISION 2 — `Sequence` → ordered leaves, and wire-width normalisation

⚠⚠ **WHY THESE TWO AND NOT MORE.** Every case in §6.3 states a leaf's fields directly, so between them they pin the
leaf **encoding** and the tree **shape** and nothing else. The function an issuer must actually agree with us on is
the **join**: given a block's receipts, which leaves, in which order, each attributed which owning receipt's
`status` and `txHash`. Revision 1 pinned both halves and left the join unpinned — and that is not a theoretical gap.
**MEASURED on this repository, at the tree state that first committed the certificate store:** three separate corruptions of the join
(every leaf's `txHash` replaced by the zero hash, every leaf's `status` replaced by a constant, the receipts
flattened in reverse order) each left that repository's **entire** test suite green, exit 0. ⇒ Below, the join is a
pinned digest.

⛔ **Inputs are given as explicit hex, not as a generator, per §6.3's own rule.** They are reproducible with no
knowledge of Go.

### `flatten/multi-receipt-mixed-status`

`seqNumber = 7331`. Four receipts, in this order. ⚠ **Each part of the shape is load-bearing and none may be
simplified:** four DISTINCT `txHash`es (a single-receipt fixture cannot detect a reversed order, and equal hashes
would hide a mis-attributed receipt); log counts 2, 1, 0, 2 (a flattener assuming one log per receipt would match a
uniform fixture); one FAILED receipt among passing ones (its log is in the tree and carries `status = 0`); one
receipt carrying NO logs (it must contribute no leaf and must not shift the leaves after it).

| # | status | txHash |
|---|---|---|
| 0 | `1` | `0x00112233445566778899aabbccddeeff00112233445566778899aabbccddeeff` |
| 1 | `0` | `0xffeeddccbbaa99887766554433221100ffeeddccbbaa99887766554433221100` |
| 2 | `1` | `0x0f1e2d3c4b5a69788796a5b4c3d2e1f00f1e2d3c4b5a69788796a5b4c3d2e1f0` |
| 3 | `1` | `0x000000000000000000000000000000000000000000000000000000000000dead` |

| receipt | log | address | topics | data |
|---|---|---|---|---|
| 0 | 0 | `0x0102030405060708090a0b0c0d0e0f1011121314` | `0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef`, `0x000000000000000000000000000000000000000000000000000000000000002a` | *(empty)* |
| 0 | 1 | `0xfeedfacecafebeef0000000000000000deadbeef` | *(none)* | `0x2a` |
| 1 | 2 | `0x00000000000000000000000000000000000000ff` | `0x8be0079c531659141344cd1fd0a4f28419497f9722a3daafe3b4186f6b6457e0` | the 64 bytes `0x00 0x01 … 0x3f` |
| 2 | — | *(the receipt carries no logs)* | | |
| 3 | 3 | `0x0102030405060708090a0b0c0d0e0f1011121314` | `0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef`, `0x000000000000000000000000000000000000000000000000000000000000002a`, `0x8be0079c531659141344cd1fd0a4f28419497f9722a3daafe3b4186f6b6457e0`, `0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff` | *(empty)* |
| 3 | 4 | `0xfeedfacecafebeef0000000000000000deadbeef` | `0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff` | `0x00` |

**Expected — `LogCount = 5`:**

| value | |
|---|---|
| leaf 0 | `0x351a95c9aa36f1ed6b64f8bce655f9d5446cc6b6dd62a24c328df13086ca1f6c` |
| leaf 1 | `0x1dffafea4a381a7ea30d50cb8405ce43e735662d808fe03ca11601398d317133` |
| leaf 2 | `0xf41b24fe6e162189f80472056af44c49328adb6616f0a7cc46ad544d5db7b9cd` |
| leaf 3 | `0x3a636033b4e7dc24953282c95f91d739d5741f42693b051dcf3e48a58d0eefab` |
| leaf 4 | `0x21b32bcdf8993115176f9afa68e2a2246ad301b9f0df89bc2c1838650ae6f0bd` |
| **`LogsRoot`** | **`0x6c73c82fd52ab32802868b078be537b90b1f0fc8d4b861a61e5bda80004532fc`** |

⚠ **The three wrong answers, given so an implementer can tell WHICH way it diverged rather than only that it did.**
All three are values a plausible implementation produces; none of them is this case's root:

| a flattener that… | produces |
|---|---|
| zeroes every leaf's `txHash` | `0x3132c9325157aa2bba99716c5195f9c28c3d5e548b25dd2042578b9c91e95391` |
| forces `status` to `1` on every leaf | `0x735fe2c75b63ed7fbf7336f0a327ab80b702cc6191a0bc8d31a7911ff2f21564` |
| iterates the receipts in reverse | `0x4036595dae7c0f64fd3363dac8d12d6795e2fbb77deb8b54336d8bf5d48b416c` |

### `flatten/wire-width-normalisation`

⛔⛔ **THIS IS THE CASE MOST LIKELY TO DIVERGE BETWEEN A GO NODE AND A TYPESCRIPT ISSUER, and revision 1 had nothing
covering it.** The certificate is computed over the node's **retained internal form**, never over the wire bytes:
every bytes-typed wire field is unbounded (proto declares no width) and `Sequence.FromProto` funnels each through
`common.BytesToHash` / `common.BytesToAddress`, which **LEFT-PAD** a short value and keep only the **LAST** 32 (or
20) bytes of an over-long one. ⇒ That rule is part of the hashed preimage's definition and an issuer must reproduce
it exactly. ⚠ **It is LOSSY in the over-long direction**: two different wire values whose last 32 bytes agree become
one internal value and hash identically. An issuer that *rejects* an over-long value, or that keeps its leading
bytes, disagrees with every node on that input — and the disagreement surfaces only as a permanently uncertified
sequence number.

⚠ `data` is deliberately **absent** from this case: it is the one bytes field `FromProto` copies verbatim, so it has
no normalisation to pin. Its width is carried faithfully by `lenData`, which §6.3's leaf cases already cover at 0, 1,
2 and 512 bytes.

`seqNumber = 9001`, `chainId = 1`. Two receipts, one log each.

| field | RAW wire value | width | NORMALISED to |
|---|---|---|---|
| receipt 0 `txHash` | `0x112233445566778899aabbccddeeff00112233445566778899aabbccddeeff` | 31 | `0x00112233445566778899aabbccddeeff00112233445566778899aabbccddeeff` |
| receipt 0 log 0 `address` | `0x0102030405060708090a0b0c0d0e0f10111213` | 19 | `0x000102030405060708090a0b0c0d0e0f10111213` |
| receipt 0 log 0 topic 0 | `0x0102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f` | 31 | `0x000102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f` |
| receipt 0 log 0 topic 1 | `0xaabb0102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f` | 33 | `0xbb0102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f` — ⛔ the leading `0xaa` is DISCARDED |
| receipt 0 log 0 topic 2 | *(zero-length)* | 0 | `0x0000…0000` (the zero hash) |
| receipt 0 log 0 `data` | `0x01` | 1 | `0x01` — copied verbatim, not normalised |
| receipt 1 `txHash` | `0xff0102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f20` | 33 | `0x0102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f20` |
| receipt 1 log 0 `address` | `0xaa0102030405060708090a0b0c0d0e0f1011121314` | 21 | `0x0102030405060708090a0b0c0d0e0f1011121314` |
| receipt 1 log 0 topic 0 | `0x11`×32 ‖ `0x22`×32 | 64 | `0x2222222222222222222222222222222222222222222222222222222222222222` — ⛔ the **first 32 bytes are discarded entirely** |
| receipt 1 log 0 `data` | *(empty)* | 0 | *(empty)* |

Both receipts have `status = 1`.

**Expected — `LogCount = 2`:**

| value | |
|---|---|
| leaf 0 | `0xc470390dfb1d69cc34d89943ab7f9c1b79a80856489272570d1ff28c02ade32c` |
| leaf 1 | `0xc3e68996f535d7a3027fdc22063586abac1700512ddf024406592458e8a7c0a1` |
| **`LogsRoot`** | **`0x8993370d4bd1cfc89b86d683ed0df0dcc4377ad54b97d54ba478cbf8d36cac6a`** |

### Provenance of these two cases

**Implementation A**, production go-ethereum keccak, in a committed test in this repository
(`abci/rnk/sequence_logs_tree_test.go`); **implementation C**, an independent byte assembly hashed by `cast keccak`,
which is where the expected values above came from — they were produced **before** the Go test was written and it
passed on its first run. ⇒ Same standing as §6.3's 22 regenerated values. ⚠ **Still not two PARTIES**, for §6.1's
stated reason.

## 6.6 THE PROOF CASE ADDED AFTER THE SECOND-PARTY PASS — the transmitted order is NOT the fold order

⚠⚠ **WHY THIS CASE AND NOT ANOTHER, and it is the sharpest fixture-design fact in this file.** §3.6's two existing
proof cases both **verify under the false *"in verifier consumption order"* reading as well as the right one**
(MEASURED). ⇒ **An implementer who followed that phrase passed the entire vector and then rejected honest blocks in
production from *n* = 4 upward.** ⛔ This is a different defect class from §6.3.1's: there a case exists and cannot be
*reached*; here two cases exist, are reached, **pass**, and do not discriminate — and what they fail to discriminate
is a **liveness** failure, honest blocks rejected, not a drift. This case is the smallest one that separates the two
readings, and it costs three hashes of which two are already pinned elsewhere in this file.

`proof/n5-carried-2-fold-order-differs-from-table-order` — `LogCount = 5`, carried `{2}`, leaves are §6.3's
generator at `seq = 42`, root `0x23ed8d42b4a8579bd3a25a83d7622f771c40288ea6ae38fa4329e450ccd3e388`
(= `tree/n5-root`, ✓ internally consistent), `expected_hash_count = 3`.

| | |
|---|---|
| canonical table order — **what the wire carries** | `[0,2)` `[3,4)` `[4,5)` |
| RFC 6962 §2.1.1 fold order for leaf 2 — **what a verifier consumes** | `[3,4)` `[0,2)` `[4,5)` |
| the fold's left/right sequence for leaf 2 | **right, left, right** |

⇒ **The first two positions are transposed, and that is the whole case.** Leaf 2 sits in the **right** half of the
`[0,4)` subtree, so its **last** sibling below the root is `[0,2)` — and `[0,2)` sorts **first**.

| interval | hash |
|---|---|
| `[0,2)` | `0x70234db48f8bf93dd3ce3697907e8a55b7c2db1d0e32e962801d984bf679f2ea` — = `tree/n2-root`, ✓ |
| `[3,4)` | `0xae62879ceb06125802985837ec3755f4c9b8f292be73e448642e25094b809aef` |
| `[4,5)` | `0x90debd54d3ebd4a2fbe247b930f81b7c5a773d4871ebf9bf2188ce4e6836df2d` — = the same interval in `proof/n5-carried-1-and-4`, ✓ |
| carried leaf 2's own hash | `0x53f51ec1f6c17d8f1377ce1c9ee64fdfaa659fbbfcb9d6d5320f16771f32150b` |

**Expected: the fold reaches `tree/n5-root`.**

⚠ **The wrong answer, given so an implementer can tell WHICH way it diverged rather than only that it did** — this
is the value produced by a verifier that takes `Hashes[j]` as the *j*-th sibling of its fold instead of regenerating
the interval list. ⚠ Note that the *side* sequence is not what is misread: right/left/right is forced by RFC 6962's
own index/total reduction and any implementation gets it. **Only the VALUE at each step moves.**

| a verifier that… | folds to |
|---|---|
| reads the transmitted order as its own consumption order | `0xdc663e18feeb29282ab6859edfc9c98a4e68e7e273907aef8325129c3bdd0c84` |

⛔ **That is not the root, so such a verifier REJECTS this block** — which is precisely what it would do to honest
blocks on a live chain. ⇒ **It is the discrimination, stated as a value: the two readings differ here, and they agree
on both older proof cases.** ⚠ **VERIFIED that it discriminates by computing it both ways under two instruments**,
rather than by asserting that it must.

### Provenance of this case

⚠ **It carries §6.1's weaker label, and one degree weaker still than the other two proof cases.** Its three interval
hashes come from **two** instruments — the second party's TypeScript encoder (two cross-checked keccak libraries) and
an independent byte assembly hashed by `cast keccak` — and two of the three coincide with values §6.3 already pins
(`tree/n2-root` and `proof/n5-carried-1-and-4`'s `[4,5)`), so only `[3,4)` and the wrong-answer root are new.
⛔ **There is still no implementation-A counterpart**, because `reactive-tornado` has no proof code; that is
unchanged by this case and is §7.3 item 5's business.

---

## 6.7 THE SIGNATURE CASES — `v ∈ {0,1}` versus `{27,28}`, with a clearly-marked test key

⚠⚠ **WHY THIS SECTION EXISTS, and it is the last gap of its own kind.** Every case above pins a preimage, a
digest or a root. ⛔ **Not one of them pinned a SIGNATURE** — so the artifact a second, independent issuer checks
itself against said nothing at all about the one field that decides whether its certificates are believed.
⇒ **The named hazard is the recovery id.** D3 and §3.5 require `v ∈ {0,1}`; the Ethereum tooling an issuer is most
likely to reach for emits `{27,28}` (`cast wallet sign` does, MEASURED below, as does the `eth_sign` /
`personal_sign` JSON-RPC family). **An issuer on one convention and a verifier on the other disagree on EVERY certificate, and neither side's
own tests can see it** — each is self-consistent. ⚠ The node side does check and is tested; this was a **vector**
gap, which is the gap that matters, because the vector is what the party that does not read our Go builds against.

### ⛔⛔ THE TEST KEY — TEST MATERIAL, AND THE MARKING IS PART OF THE FIXTURE

| | |
|---|---|
| the key's 32 bytes, as ASCII | `rnk.vector.test.key.never.deploy` |
| the same 32 bytes, as hex | `0x726e6b2e766563746f722e746573742e6b65792e6e657665722e6465706c6f79` |
| the issuer address it derives | `0xfff0C37702e1Ac61A477Bb38feEC4ccE30914b3e` |

⛔⛔ **WHAT IT IS, WHAT IT IS FOR, AND WHERE IT MUST NEVER GO.** It is a secp256k1 private key whose 32 bytes are
the ASCII sentence above, chosen for exactly that reason: **dump the key in any tool and it states its own status.**
Its only purpose is to make the four cases below reproducible by anyone, in any language, without a shared secret.
⛔ **It MUST NEVER appear in a genesis file, a node or Sequencer configuration, a keystore, a deployment script, or
any issuer registry on any network — mainnet, testnet or devnet.** It is published, so it protects nothing; a
certificate that verifies under it is a certificate anyone can forge. ⚠ **It is not a credential that was moved
here for safe-keeping and it is not a rotated key** — no address derived from it has ever held state or been
registered as an issuer, and this document is its only home.

⚠ **Why the key is a sentence rather than 32 random-looking bytes, stated because the repository's existing test
keys are the other kind.** A 64-hex literal is indistinguishable from a wallet export, so its status lives only in
the comment beside it and is lost the moment the value is copied. This one carries its status **in the value**, and
`0x726e6b2e…` — `"rnk."` — is the same four bytes every domain tag in §3.1 opens with, so it reads as construction
material at a glance. ⛔ **Do not "tidy" it into a random key, and do not add a second key**: one issuer is all four
cases need, and a second would make the fixture's registry ambiguous.

### The signed message — `cert/present-3-logs`, and nothing new

⚠ **No new certificate content is introduced.** The cases sign the certificate §6.3 and §6.3.1 already pin, so a
divergence here is a signature divergence and cannot be a preimage divergence. Both values are repeated in full so
that the section is checkable on its own:

| | |
|---|---|
| preimage (159 bytes) | `0x726e6b2e736571636572742e7631000000000000063d000000000000006501000000070000000000000001ababababababababababababababababababababababababababababababababcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcdcd0000000001406f4000000000689b2cc0000000038c6e26c25502a62aa23c5ae614f1c237da67c382b9844b539275ea3da07011cf` |
| `certDigest` = keccak256(preimage) | `0xd14177b38a313090746b0a11245510712b85ec7c47e863a66db4e84bc4d1ea39` — ⇒ **`cert/present-3-logs`, unchanged** |

⚠ **The signature is deterministic, which is what makes it a fixture at all.** RFC 6979 nonce derivation means the
key and the digest fix `(r, s)` exactly, so a second implementation must **reproduce** these bytes rather than merely
produce something that verifies. **MEASURED: three independent libraries agree byte for byte** — production
go-ethereum, `cast wallet sign --no-hash` (foundry, Rust), and `@noble/curves` (TypeScript).

### The four cases

| case | `r` | `s` | `v` | recovered signer | verdict |
|---|---|---|---|---|---|
| `sig/present-3-logs-valid` | `0xfafd3b45b4adbab0a101165078b53e481a801ad35e65e81843b31052ce190a23` | `0x6e291dd43bb229e567755c45604966328db6bb96e875de88ca4ec52032aca203` | `0x01` | `0xfff0C37702e1Ac61A477Bb38feEC4ccE30914b3e` — ⇒ **the issuer** | ⇒ **VALID** |
| `sig/present-3-logs-recovery-id-in-the-27-28-convention` | *(the same `r`)* | *(the same `s`)* | ⚠⚠ **`0x1c` = 28** | *(none — `v` is out of range before any recovery)* | ⛔ **INVALID**, `signature_encoding` |
| `sig/present-3-logs-recovery-id-flipped` | *(the same `r`)* | *(the same `s`)* | `0x00` | `0x4DE204Eb96d354F2c3f165A8cF07e34e99D8bD2E` — ⚠ **a well-formed address that is not the issuer** | ⛔ **INVALID**, `signature` |
| `sig/present-3-logs-high-s` | *(the same `r`)* | `0x91d6e22bc44dd61a988aa3ba9fb699cc2cf8214fc6d2c1b2f583996c9d899f3e` = *n* − `s` | `0x00` | `0xfff0C37702e1Ac61A477Bb38feEC4ccE30914b3e` — ⚠⚠ **the issuer, correctly** | ⛔ **INVALID**, `signature_encoding` |

The 65-byte wire forms, `r ‖ s ‖ v`, written out so no reader has to concatenate:

| case | 65 bytes |
|---|---|
| `sig/present-3-logs-valid` | `0xfafd3b45b4adbab0a101165078b53e481a801ad35e65e81843b31052ce190a236e291dd43bb229e567755c45604966328db6bb96e875de88ca4ec52032aca20301` |
| `sig/present-3-logs-recovery-id-in-the-27-28-convention` | `0xfafd3b45b4adbab0a101165078b53e481a801ad35e65e81843b31052ce190a236e291dd43bb229e567755c45604966328db6bb96e875de88ca4ec52032aca2031c` |
| `sig/present-3-logs-recovery-id-flipped` | `0xfafd3b45b4adbab0a101165078b53e481a801ad35e65e81843b31052ce190a236e291dd43bb229e567755c45604966328db6bb96e875de88ca4ec52032aca20300` |
| `sig/present-3-logs-high-s` | `0xfafd3b45b4adbab0a101165078b53e481a801ad35e65e81843b31052ce190a2391d6e22bc44dd61a988aa3ba9fb699cc2cf8214fc6d2c1b2f583996c9d899f3e00` |

⚠⚠ **`sig/present-3-logs-high-s` is the malleability case and it deserves its one sentence: it recovers the
CORRECT issuer.** `(r, n − s, 1 − v)` is a second valid ECDSA signature by the same key over the same digest, so
every check except the encoding rule passes. ⛔ **That is why the rule is an encoding rule and not a signature
rule** — without it two byte-different certificates carry the same authority, which is a free-space channel in
something the block hash covers, the same defect class §5 closes for the proof table.

⚠ **And the case that is deliberately ABSENT, because it would read as coverage while proving nothing.** The other
member of the `{27,28}` pair, `v = 0x1b = 27`, is invalid under **both** conventions — a `{27,28}` verifier maps it
to recovery id 0, which recovers `0x4DE204Eb…` rather than the issuer. ⇒ **Only the member that corresponds to the
TRUE recovery id discriminates**, which for this digest is 28. ⛔ A vector that pinned `v = 27` as invalid would
have been passed by an implementation on either convention.

### ⇒ The discrimination matrix — MEASURED, every case against the rule it guards

⚠ **Each row is a case; each column is a verifier. The first column is §3.5's rule as
`abci/rnk/sequence_cert.go`'s `signatureReason` implements it; the other three are that verifier with exactly one
rule changed.** ⇒ **A case earns its place by having a column where its verdict FLIPS**, and the flip is bolded.

| case | strict, as implemented | `v ∈ {27,28}` convention | low-S rule removed | recovery id ignored |
|---|---|---|---|---|
| `sig/present-3-logs-valid` | **VALID** | ⛔ **INVALID** — flips | VALID | VALID |
| `sig/present-3-logs-recovery-id-in-the-27-28-convention` | INVALID | ⛔ **VALID** — flips | INVALID | ⚠ **VALID** — flips too, for a different reason: this variant reads no `v` at all |
| `sig/present-3-logs-recovery-id-flipped` | INVALID | INVALID | INVALID | ⛔ **VALID** — flips |
| `sig/present-3-logs-high-s` | INVALID | INVALID | ⛔ **VALID** — flips | INVALID |

⇒ ⚠⚠ **The first two rows are the point, and they are a two-way discriminator rather than a one-way check.** An
implementation on the wrong recovery-id convention gets the **opposite** verdict on **both** of them: it rejects the
valid certificate and accepts the invalid one. **So the convention cannot be got wrong and still pass**, in either
direction — which is exactly what a one-sided fixture would have allowed.

⚠ **The third and fourth rows guard rules that a plausible implementation drops for plausible reasons**: low-S
because `ecrecover` does not require it, and the recovery id because "try both and see which one matches" is a
common shortcut. **Both shortcuts open a free-space channel**, and each has a case that catches it.

### Provenance of these four cases

| | |
|---|---|
| **signature bytes** | ⇒ **three libraries, byte-identical.** Production go-ethereum `crypto.Sign` (the vendored fork, implementation A's stack); `cast wallet sign --no-hash --private-key …` (foundry 1.5.1, Rust); `@noble/curves` 1.9.7 `secp256k1.sign` (TypeScript). ⚠ **None of the three was told the other's answer** — each derives `(r, s)` from RFC 6979 over the same digest and key |
| **recovered addresses and the whole matrix** | ⇒ **two independent stacks.** go-ethereum `SigToPub`/`PubkeyToAddress` and `ValidateSignatureValues`, and a `@noble/curves` + `@noble/hashes` recovery written against §3.5's prose. **32 assertions compared, 0 disagreements** |
| **the document itself** | ⚠ a third instrument **parses this section** — the key, the address, the digest, the four rows and the matrix — re-derives every value, and reddens if the prose disagrees with the crypto. ⛔ **It is the only one that can catch a hand-transcription error here**, because the other two check each other and not the page |
| **negative controls, all fired** | ⚠ changing one certificate field on the independent side reddened the digest guard; moving the independent `strict` verifier onto `{27,28}` reddened the matrix comparison; dropping its low-S rule reddened it differently. ⇒ **The instrument was shown to fail before it was believed** |
| **probe tree** | a working tree, **not in this repository** — §6.4 |

⛔ **NO COMMITTED DIGEST MOVED.** The certificate preimage, its digest and every value in §6.3 and §6.3.1 are
re-derived by both instruments in this section and are byte-identical to what was already pinned.

⚠ **What these cases do NOT establish, so it is not read into them.** They pin the **encoding rule** and the
**recovery** — the shape of a 65-byte signature and which address it comes back as. They say nothing about **which
`KeyId` maps to which real issuer**, which is committed state whose home §7.2 still records as undecided; and
nothing about how a `Sig` field is carried on the wire, which is `SequenceProof`'s unpinned-serialisation gap.

---

# 7. WHAT REMAINS

## 7.1 Nothing was invented, and nothing forced a stop

⚠ **Per the standing constraint, reported explicitly.** Every element is either off-the-shelf (keccak256,
secp256k1, RFC 6962 §2.1's recursion and §2.1.1's audit path, including **both** base cases) or an encoding that no
standard speaks to and that is now pinned and driven. ⇒ **The verification argument is: RFC 6962 §2.1.1, run once
per carried leaf, plus one integer comparison.**

⚠ **The one thing I added is §5's count requirement**, and it is a length check, not a construction — ⛔ but it is
**mine and in no input document**, so it is flagged as such and classified.

## 7.2 What this file does NOT settle

| item | whose | why it is still open |
|---|---|---|
| ⛔ **The committed artifact's OWNER** | maintainer / Sequencer owner | the upgrade specification §15.2's BLOCKING item. ⚠ **SEARCHED and unchanged: neither Sequencer-side repository has any crypto today** — no keccak, no secp256k1, `reactive-sequencer`'s dependencies are `@ethereumjs/rlp`, `env-var`, `pino`, `rabbitmq-client`. **The signer is greenfield in both candidate homes.** |
| ⛔ **Two-party agreement — NARROWED, not closed** | both | ⇒ **The ENCODING has it** (§6.1, revision 3: a second implementation from this document's prose, 61 assertions, 0 disagreements). ⛔ **What is open is the ISSUER's agreement** — the party that will sign has not built against these numbers, and no build fetches the vector. ⛔ Superseded: this row read *"One author's two implementations is not two parties."* |
| ⚠ **Which process signs** | Sequencer owner | the upgrade specification §15.1/§15.4 want the **writer** (TypeScript); its §15.2 wants the traversal that **serves** (Go). ⇒ **Not satisfiable by the current topology**, as the review reported. **Unchanged by this file.** |
| ⚠ **`sequenceMsgToEvent` as the sole `LogIndex` producer** | Sequencer owner | narrowed to one repository by a grep census; ⛔ **`sequencer-db-chunker` and `db-cleaner` were NOT read.** |
| ⚠ **Over-long byte values rejected at ingest** | Sequencer owner | the upgrade specification §15.2's second requirement; not re-derived here. ⚠ **It bears directly on this file: `common.BytesToHash` truncation means an over-long topic changes the leaf preimage on one side only.** ⇒ **PARTLY DISCHARGED on our side:** this repository's `abci/rnk/sequence_logs_tree_test.go` now pins the node's normalisation — short values LEFT-PADDED, over-long values reduced to their LAST 32 (or 20) bytes, zero-length reduced to the zero hash — over a sequence decoded through `Sequence.FromProto` itself, so the rule an issuer must replicate is now a committed expected value rather than an assumption. ⛔ **What is still open is the Sequencer's own behaviour**: whether it rejects such a value at ingest or forwards it. Both are implementable against the pinned rule; only one of them is currently written down anywhere. |
| ⚠ **`rlp:"optional"` on the two new fields** | maintainer | the upgrade specification §2.2's OPEN. **Untouched — and note it is now MORE attractive**, since §2's preimage no longer depends on RLP at all. |

## 7.3 The follow-up, in order

1. **Correct the upgrade specification §2.4's prose** (§1.1) and its **§2.7's `Because:`** (the RFC does define
   n = 0), and **add n = 1**.
2. **Replace the upgrade specification §2.3's `rlp(…)` formula** with §3.5's layout.
3. ✅ **DONE — the fixture and test are in this repository.** `abci/rnk/sequence_logs_tree_test.go` is the Go
   regression net over the §6.3 values, including the two cases §6.2 flags as missing — an explicit multi-receipt
   root and a byte-normalisation root — and `abci/rnk/sequence_encoding_vector.json` is the language-neutral
   artifact, carrying all forty cases as data with explicit hex inputs rather than a Go generator, read by
   `abci/rnk/sequence_encoding_vector_test.go`. ⛔ **It still has no owner** (§7.2), and item 4 below is what makes
   it enforce anything.
4. **Wire the Sequencer build to it** — ⛔ **without this, per the upgrade specification §15.2's own words, the vector is worthless.**
5. **Add the `check=proof_shape` REJECT** (§5) to `ProcessProposal`, Class 1, with no `FinalizeBlock` half.
6. ✅ **DONE in revision 2 — §6.5** (the flattener and normalisation cases) **and in revision 3 — §6.3.1**
   (the ten `leaf/*` and four `cert/*` fixtures' inputs). ⇒ **Every `leaf/*` and `cert/*` case in this file is now
   constructible by a second party from this file alone**, MEASURED by two encoders neither of which is the node's.
   ⚠ **What is still a generator, deliberately, is `tree/*` and `proof/*`** — §6.3's generator paragraph, which a
   second party MEASURED to be sufficient (it reproduced `tree/n1024-root`, the case that requires replicating Go's
   `byte(0x10+i)` wrapping for *i* up to 1023). ⛔ Writing 1024 leaves out as hex would trade a working description
   for bulk; the description stays, and §6.3.1's rule — *inputs, not code* — is discharged for every case whose
   inputs are not a rule.
7. ⚠ **Regenerate revision 1's probe tree (§6.4), or retire it.** Its two implementations describe the superseded
   layout, and a probe tree that reproduces the wrong column is a trap for the next reader — now a trap a reader of
   this repository cannot open, since the tree is not committed here.
8. ✅ **DONE in revision 4 — §6.7.** The vector had no signature case of any kind, so `v ∈ {0,1}` versus the `{27,28}` an Ethereum tool emits was unpinned in the artifact an independent issuer checks itself against. ⇒ **Four `sig/*` cases and a clearly-marked test key now pin it**, each measured to flip under the rule it guards. ⛔ **What this does NOT close is item 4**: nothing fetches these cases either.

---

# 8. ⛔ WHAT WAS WRONG IN THE REQUEST THAT COMMISSIONED THIS FILE, LOUDLY

⚠ **Three further items stood here and were removed when this file moved into the repository** — a checkpointing
instruction I could not follow as written, a contradiction between two working process documents, and a size
measurement corrected from an earlier report of mine. They were notes on how the pass was run, each resting on a
document this repository does not carry. The three below carry technical content and stay.

1. ⚠⚠ **The keccak question was raised as *"I do not think it has been registered by anyone"* — correct, and worse
   than stated.** It is not merely unregistered: **the upgrade specification contradicts itself about the
   closely-related D2**, with its §2.4's prose specifying the RFC's `0x00`/`0x01` prefixes and its own code block using ASCII tags, in adjacent
   lines (§1.1). ⇒ **So the construction's domain separation was ambiguous in the source document, not just
   undocumented.** I could not have found this without being told to build the register — **the register earned its
   place on its first use.**

2. ⚠ **The request's judgement on keccak is ADOPTED, not independently confirmed, and the difference matters.** I
   verified that the design does use keccak256 (VERIFIED, the upgrade specification §2.3/§2.4 formulas) and that RFC 6962 specifies
   SHA-256 (VERIFIED). ⛔ **I did not independently assess keccak256's cryptographic standing and am not competent
   to** — the register records the reasoning as the requester's, at the requester's own invitation to overrule
   it. **That is a labelling point, not a disagreement.**

3. ⚠ **A framing in the request that would mislead if carried forward:** *"your 6.53 KB measurement"* is the
   **deduplicated-path** figure at one operating point (n = 1024, k = 51, ~25 clusters). ⛔ It is **not** a general
   property — MEASURED, it moves from 1.69× to 5.06× of the multiproof depending on clustering, which nobody
   controls. **Cite it as "≈6.5 KB at the measured operating point", never as the cost of the scheme.**
