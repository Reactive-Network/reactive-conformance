# Reactive Network — conformance artifacts

Byte-level artifacts that hold **two independent implementations to the same bytes**.

Each artifact here is consumed by more than one codebase, written in more than one language. Where two
implementations must agree on a hash, a signature preimage or a wire encoding, neither implementation's own
test suite can detect a disagreement — each is self-consistent. The agreement is held by an artifact, and only
if both sides read the *same* artifact.

## What is here

| path | what it pins |
|---|---|
| `vectors/sequence-encoding-vector.json` | the byte-level construction of a sequence certificate: leaf and node preimages, Merkle roots, audit-path serialisation, the certificate preimage, and one signature case |
| `docs/sequence-encoding-construction.md` | the construction's derivation — every digest above, case by case, with the reasoning and the departures from RFC 6962 |

```
vectors/sequence-encoding-vector.json
  sha256  8f31655e70e0af65056b7ffbf510ce1d0846e27e3bc777216af1a84be8b9cd48
  bytes   33668
  schema  rnk.sequence-encoding-vector.v1
  cases   40
```

## How to consume it

Fetch it **by commit and verify the hash**. Do not vendor a copy — a copied artifact is two artifacts that
agree until they do not, which is the failure this repository exists to prevent.

A consumer should pin `{commit, path, sha256}` together and fail its build when the hash does not match. It
should not fall back to a bundled copy, and it should not skip the check when the fetch is unavailable: a build
that goes green while enforcing nothing is the outcome the whole arrangement is meant to make impossible.

## ⚠ Where the authority lives, and why it is not here

**These artifacts are a distribution, not the authority.** The normative copy of the sequence encoding vector
lives in the node implementation, because a change to that encoding is a **consensus** change — it decides
which blocks a chain accepts. Holding the normative artifact where consensus lives means the encoding cannot
change without a node release, and the party bearing the cost of a drift is the party holding the artifact.

So the direction of trust runs: the node repository defines the bytes; this repository publishes them
unchanged; consumers verify against the hash above. A copy here differing from the node's by a single byte
fails every consumer's hash check immediately and loudly — which is the intended behaviour, and is why no
separate divergence check is needed.

Publication is deliberate rather than automatic: the artifact changes only when the encoding changes, which is
a release-gated event, so the publication step belongs to that event rather than to a scheduled job.

## ⚠ Two limits, stated because their absence would read as an oversight

**The construction document cites paths inside the node implementation, which is not public.** Those citations
are correct — they point at the normative source — but an external reader cannot follow them. The document is
published here so that every digest can at least be *located* and its derivation read, rather than arriving as
opaque bytes.

**The instruments that produced these digests are not published anywhere.** The generator, the cross-language
comparison harness and the independent second implementation used to check them are working artifacts
belonging to neither consumer. So this repository lets a digest be **located** and **compared against**; it
does not yet let one be **re-derived**. Giving those instruments a home is the natural next use of this
repository.

## ⛔ If a digest appears to have moved

It is a finding, not a value to update. Every case here was transcribed from a derivation, and a value that no
longer matches means either that an implementation has drifted or that the artifact was edited — both of which
want investigating before anything is changed to agree with them.
