# FAIAS — ownership and integrity proof

**Owner:** Wonder Attah
**Standard:** FAIAS v1.3.2 — Financial AI Independent Assurance Standard
**Created:** 30 July 2026 · **Re-signed:** 30 July 2026 (v1.0.1) and 31 July 2026 (v1.0.2 and v1.0.3, the v1.0.3 attestation itself reading 1 August 2026); 25 August 2026, the v1.1.0 refresh batch; then 27 August 2026 as v1.1.1, the correction batch following two hostile documentation audits — replacing, at the same label, a 26 August v1.1.1 signing never distributed beyond the signing device; 15 September 2026 as v1.2.0, the September 2026 refresh batch; 28 September 2026 as v1.2.1, the correction and evidence batch of 19 September 2026; 3 October 2026 as v1.3.0, the pre-publication batch of 3 October 2026; 3 October 2026 as v1.3.1, the structural release of 3 October 2026; and 3 October 2026 as v1.3.2, the corrections release of 3 October 2026

---

## What exists

| Artefact | What it is |
|---|---|
| `.git/` | Git repository, authored Wonder Attah. The public repository starts at the v1.3.2 signing in one commit. The maintainer's private repository holds the full history, described here. **First commit `3f97bd97bbe8f62e1f37ec0dc5d4dd11cba5fdaa`, 2026-07-30T06:02:00Z; its tree reproduces root `38cd33d4…f102b8405c`, recorded as the first signing (signing history below).** The history was rewritten on 28 September 2026 to remove material outside the standard; authorship, dates and commit messages are unchanged, and every commit identifier changed. Before the rewrite the first commit was `0fe4c8d6c81d84b551c8ee4a19fa5815021c2fd6`, which every earlier attestation names as the commit at first signing: it holds the earliest signed manifest (root `02a9ac29…ab37eb7`, 52 files; its signature verifies against the public key below), and in it the licence statement in `00_Admin/OWNERSHIP_AND_LICENCE.md` and `README.md` named a licensee; both were generalised the same day and the manifest regenerated (root `38cd33d4…f102b8405c`) before the v1.0.1 signing was committed at `021a4818…` (2026-07-30T20:29:51Z; `dc57adf6…` after the rewrite). The rewritten first commit holds both files at their generalised content, so the signed manifest it carries matches 50 of its 52 files. The original history is preserved in a git bundle (sha256 `8d0c2ed5…1bd0`, timestamped 28 September 2026), retained by the owner. In the private repository, later commits carry the corrections and the re-signed manifest. Run `git log -1` for the current head rather than relying on a hash quoted here, which goes stale on every commit. **The repository holds FAIAS only — nothing but the standard, by design. That separation supports the claim that FAIAS is independently authored work** |
| `MANIFEST.sha256` | SHA-256 of every one of the 273 content files |
| `MANIFEST.sha256.sig` | Ed25519 signature over the manifest |
| `ATTESTATION.txt` | Owner, manifest root hash, file count, manifest scope, the commit at first signing, and the root hash this one supersedes |
| `MANIFEST_v1.0.1.sha256` to `MANIFEST_v1.3.1.sha256`, each with its `.sig`; `ATTESTATION_v1.3.0.*` and `ATTESTATION_v1.3.1.*` | The superseded signings. Each archived manifest and its signature verify against the public key below, so each earlier root in the signing history can be checked. The attestations of v1.3.0 and v1.3.1 are archived with their signatures and OpenTimestamps proofs. The attestations of v1.0.1 to v1.2.1, with their signatures and OpenTimestamps proofs, are kept privately (see "How anyone verifies it"); those proofs carry Bitcoin block attestations (v1.0.1: Bitcoin blocks 960309/960311/960337; v1.0.2: blocks 960360/960362; v1.0.3: blocks 960429/960430/960481/960506; v1.1.0: blocks 964009/964013/964033/964042; v1.1.1: blocks 964302/964304/964307/964338 — those three upgraded 12 September 2026; v1.2.0: blocks 967085/967086/967098/967150, upgraded 24 September 2026; see below). Of the two 30 July 2026 roots in the signing history below, `02a9ac29…` verifies from commit `0fe4c8d`, preserved in the archive of the original history, and no signature over `38cd33d4…` survives, and the 26 August v1.1.1 signing, `5bafbc8a…`, was not distributed and is not archived here |
| `ATTESTATION.txt.sig` | Ed25519 signature over the attestation |
| `faias_public_key.pem` | Public key — share this freely |
| `faias_private_key.pem` | Private key. Never in either repository: excluded by `.gitignore` and held by the owner outside it |

**Manifest root hash:** `275b19056e562fd52a7d6a3d0f7a7affed91f335a686a75b8dfc30ff127bc5a9` (v1.3.2, signature 3 October 2026; the last signed root before it is `56b58a42…` v1.3.1, 3 October 2026)

**Public key fingerprint (SHA-256 of DER):** `c1d41da6317cfb96c2faa2b966292f9cf5534f63f73f566ed426217ca9510272`

```
-----BEGIN PUBLIC KEY-----
MCowBQYDK2VwAyEAXLoBF4qvFwiyl+hb3XwSW/5qPHlJTAMJG3CIDbLPUcM=
-----END PUBLIC KEY-----
```

### What the manifest covers

Every file under the standard root, excluding four things: `.git/`, `ownership/`, `00_Admin/ANALYSIS_LOG.md`, and `00_Admin/ARCHIVE/` (superseded planning artefacts, retained for record, excluded from the share by the owner's ruling).

The first two are excluded because a manifest cannot contain its own hash. The analysis log is excluded because it is a live working record: it is appended to after each review and it records the manifest root itself, so including it would mean every log entry invalidated the signature over the standard. The `v1.0`-named duplicate compiled pair that the v1.0.1 and v1.0.2 attestations excluded was deleted on 31 July 2026, as were the superseded `v1.0.1` compiled outputs; the compiled editions inside the manifest are the pair the manifest itself names, each superseded pair having been deleted at its re-signing, with the private repository's git history as the retention record. All exclusions are stated inside the signed attestation, so they are part of what the signature covers rather than undisclosed omissions. The analysis log and the archive are kept in the maintainer's private repository and are not in the public repository.

### Signing history

| Root hash | Files | Occasion |
|---|---|---|
| `02a9ac29…ab37eb7` | 52 | Earliest signed manifest, 30 July 2026, at commit `0fe4c8d` (06:02Z), preserved in the archive of the original history; the rewritten first commit, `3f97bd9`, carries it and matches 50 of its 52 files. The licence statement in two files named a licensee. Not recorded in any attestation before v1.2.1; superseded the same day by the row below |
| `38cd33d4…f102b8405c` | 52 | Recorded as the first signing, 30 July 2026, after the licence statement was generalised. Not committed, and no signature over it survives; the manifest reproduces exactly from the `0fe4c8d` tree with the two generalised files at their `021a481` content, which is the tree of the rewritten first commit, `3f97bd9` |
| `4f37064c…9453bf64c516` | 52 | Re-signed 30 July 2026, after the OWASP (2025 edition) LLM03/LLM05 correction and the rebuild of the compiled Word and PDF outputs |
| `87d006c8…748f1d16` | 52 | Re-signed 31 July 2026 as v1.0.2: 11 broken internal references corrected across 10 files (V2_Risk_Battery → V2_IRQ_Battery, container paths removed), PROJECT_PLAN.md marked superseded, README version line corrected, compiled outputs rebuilt (1,461 pages) |
| `24fcefef…f5c9e376` | 52 | Re-signed 31 July 2026 as v1.0.3 (the archived attestation reads "signed: 1 August 2026"; see the note under "Anchoring the date" below): thirteen new IRQs (93 → 106; subdomains 40 → 44), all 27 claim criticalities re-derived against the criticality test (16C/10H/1M), scope exclusion for AI-enabled attack on the institution's controls, 25 regulatory-register additions (62 → 87), five methodology additions with no rating changes, corrections per CORRECTION_LOG_2026-08-01, compiled outputs rebuilt (1,613 pages) |
| `28f73086…817d929c` | 52 | Re-signed 25 August 2026 as v1.1.0: one new IRQ (106 → 107, IRQ-AGT-014), one new claim (27 → 28, CLM-28 Critical), thirteen playbook sheets restoring 1:1 (107 procedures, 445.0 reviewer-days), rating-currency mechanism with the P-scale on 23 canvases, 28 regulatory-register additions (87 → 115), OWASP 2025-edition pins and refresh-gate corrections, compiled outputs rebuilt (1,463 pages) |
| `5b3f8674…45b39a1e` | 52 | Re-signed 27 August 2026 as v1.1.1 — replacing, at the same label, a 26 August v1.1.1 signing (root `5bafbc8a…13637ff0`) never distributed beyond the signing device; the replacement adds five incident-register rows on the owner's instruction (Robodebt, MiDAS, TOEIC, FTC v. Rite Aid, the 2026 evaluation-containment cluster) and the CMORG May-2025 cover-date correction. The batch: produced under four commissioned discovery audits and a closure verification against the signed baseline: attribution-truth errata (27 SYSC 19D → SYSC 4.1.1R/4.1, four "BCBS 233" → BCBS 239/SS1/23, six SYSC 15A.6 → operative rules, DORA/OWASP/NIST/PRIN/DISP/ISO/AI-Act pinpoints), register enrichment (regulatory 124/24 sections, academic 115, labs 64 — 303 total), Related-IRQs canvas-authoritative for all 107 with a mechanised checker, ID scheme rebuilt (44 subdomains), numeric-provenance doctrine with 113 disclosure labels across all nine playbooks, TP-HUM-003 E2 L3 → L2, TP-CON-007 fabricated method pair deleted, claims register illegal-limb construction with CLM-20/CLM-24 High → Critical (19C/8H/1M), closure residuals fixed and undeclared-truthful changes disclosed, compiled outputs rebuilt (1,483 pages at this signing, verified as built) |
| `937f1d30…ea9743fc` | 52 | Re-signed 15 September 2026 as v1.2.0: the September 2026 refresh batch — two new IRQs (107 → 109: IRQ-MOD-016 ★2, IRQ-CON-010 ★1) with procedures (455.0 reviewer-days), §6A.6 capability-envelope notes, §7A, URO-1 resolved by affirmation and four new observations, RES-004/RES-006 re-anchored at ★2, registers 158 regulatory / 139 academic / 100 labs / 37 incidents, canvas additions from the September window's primaries, errata; three earlier OpenTimestamps proofs upgraded; two blind closure audits by independent adversarial passes resolved before signing |
| `6ff60b28…05c8d8ff` | 54 | Re-signed 28 September 2026 as v1.2.1: the correction and evidence batch of 19 September 2026 — incident register 37 → 46 rows, with a column naming the IRQs whose canvases cite each row, verification-status markers and a rule that row numbers are permanent; regulatory register 158 → 163 entries across 32 sections; canvas evidence additions citing register rows, and two widenings at an unchanged rating (IRQ-CON-001, IRQ-RES-007) with their procedures; errata against the primaries, the corrected rows and passages re-checked against their sources on 24, 25, 26, 27 and 28 September 2026 where a source could be reached, and recorded in CORRECTION_LOG_2026-09-19 with what each was checked against; `.gitattributes` added so every path is stored byte-for-byte; 109 IRQs and every rating unchanged; the v1.2.0 OpenTimestamps proof upgraded |
| `16734a6e…cd9f5831` | 56 | Re-signed 3 October 2026 as v1.3.0: the pre-publication batch of 3 October 2026 — published under CC BY 4.0 (`LICENSE` added); the standard presented as a baseline that supports several uses; the opinion layer and its templates illustrative and aligned with ISAE 3000, not conformant to it; the non-production rule stated once; governance roles stated as functions held by the maintainer; document versions given by the release; errata recorded in CORRECTION_LOG_2026-10-03; 109 IRQs |
| `56b58a42…747a12de` | 273 | Re-signed 3 October 2026 as v1.3.1: the structural release of 3 October 2026 — each Review Canvas of the nine domains and each test procedure in its own file (107 canvases, 109 procedures; the two exemplar canvases stay in `V2_IRQ_Battery/EXEMPLAR_CANVASES.md`), listed in its domain file; the text of every canvas and procedure, and the introductory and closing text of every domain file, unchanged apart from CRLF → LF line endings; a migration map added (`00_Admin/MIGRATION_2026-10-03.md`); three cross-references pointed to the item file; five retained logs given a head note; the README version line and file map updated; the compiled Word and PDF editions rebuilt |
| `275b1905…127bc5a9` | 273 | Re-signed 3 October 2026 as v1.3.2: the corrections of 3 October 2026 after a full read of the standard before publication — titles, dates, links and quotations corrected at the primary; regulatory restatements brought into line with the text; internal inconsistencies removed; the non-production rule's application to a provider's generally available API stated; the Sponsor's role and three firm-side owners stated; Tier 3's additional condition labelled; TP-HUM-002 given IRQ-HUM-002's refusal-durability limb; canvas footers give the release version; URO-6 opened on IRQ-DAT-009 and URO-2 to URO-5 recorded as past their signing-batch limit; a signing batch under ASSURANCE_MODEL.md §6A.2; no IRQ, claim, ★ rating, risk profile or procedure's reviewer-day figure changed (`00_Admin/CORRECTION_LOG_2026-10-03.md` §8); the compiled Word and PDF editions rebuilt |

The manifest root, not the version label, is the definitive identifier for a version of this standard.

---

## How anyone verifies it

Anyone with the repository and the public key runs:

```bash
# 1. Every file matches the manifest — nothing altered since signing
sha256sum -c ownership/MANIFEST.sha256

# 2. The manifest carries the owner's signature
openssl pkeyutl -verify -pubin -inkey ownership/faias_public_key.pem \
  -rawin -in ownership/MANIFEST.sha256 -sigfile ownership/MANIFEST.sha256.sig

# 3. The attestation carries the owner's signature
openssl pkeyutl -verify -pubin -inkey ownership/faias_public_key.pem \
  -rawin -in ownership/ATTESTATION.txt -sigfile ownership/ATTESTATION.txt.sig

# 4. The repository is clean, and the head commit's identity and author
git fsck && git log --format='%H %an %aI' -1
```

Steps 1 to 3 passing prove: this content, unmodified, signed by the holder of that private key. Step 4 shows the commit that holds it; the git dates are set by the committing machine (see below). In the private repository, the first commit (`git rev-list --max-parents=0 HEAD`) is `3f97bd97…`, the rewritten first commit that the attestation's first-signing line names; the public repository starts at v1.3.2 and does not carry it.

Signed attestations for releases before v1.3.0 are kept privately by the maintainer and can be shown on request.

---

## What this proves, and what it does not

**Proves:** integrity — the content has not changed since signing — and authorship control, in that only the holder of that private key could have produced these signatures. Set against the source registers and the correction logs in the standard, that is a strong authorship position.

**Does not prove:** the *date*. Git commit dates and file timestamps are set by the local machine and can be altered trivially. The signature binds content to a key, not to a moment in time. A challenger who claimed earlier authorship would attack the date, not the hash.

### Anchoring the date — status

**Done, and Bitcoin-attested for every signing from v1.0.1 to v1.2.0; the v1.2.1, v1.3.0 and v1.3.1 proofs await upgrade, and the v1.3.2 proof is submitted at signing and upgraded once confirmed.** Every signing from v1.0.1 onward carries an OpenTimestamps commitment over its attestation, submitted to four independent calendars at signing. The proofs for releases before v1.3.0 are kept privately with their attestations.

- **v1.0.1** — submitted 30 July 2026, `ots upgrade` run 31 July 2026; the proof, kept privately with the superseded attestation as `ATTESTATION_v1.0.1.txt.ots`, carries **three Bitcoin block attestations (blocks 960309, 960311 and 960337)**.
- **v1.0.2** — **blocks 960360 and 960362** (kept privately as `ATTESTATION_v1.0.2.txt.ots`).
- **v1.0.3, v1.1.0 and v1.1.1** — upgraded together on **12 September 2026**, each now carrying **four independent Bitcoin block attestations**: v1.0.3 at blocks 960429, 960430, 960481 and 960506 (kept privately as `ATTESTATION_v1.0.3.txt.ots`); v1.1.0 at blocks 964009, 964013, 964033 and 964042 (kept privately as `ATTESTATION_v1.1.0.txt.ots`); and v1.1.1 at blocks 964302, 964304, 964307 and 964338 (kept privately as `ATTESTATION_v1.1.1.txt.ots`).
- **Note, 26 September 2026:** the v1.0.3 proof's earliest Bitcoin attestation, block 960429, carries block time 1785514044 (2026-07-31T16:07:24Z), with blocks 960428 and 960430 at 16:03:06Z and 16:09:41Z; the proof commits the archived attestation's exact bytes, which read "signed: 1 August 2026". The attestation text was therefore committed to Bitcoin on 31 July 2026. On the owner's ruling of 26 September 2026 the signing history above dates the v1.0.3 signing 31 July 2026 and records beside it the date the archived attestation bears. The archived attestation stands as signed.
- **v1.2.0** — upgraded on **24 September 2026**, carrying **four Bitcoin block attestations**: blocks 967085, 967086, 967098 and 967150 (kept privately as `ATTESTATION_v1.2.0.txt.ots`).
- **v1.2.1** — submitted to the four calendars at its signing (kept privately as `ATTESTATION_v1.2.1.txt.ots`); it depends on the calendars until it is upgraded once the commitments are confirmed in Bitcoin blocks.
- **v1.3.0** — submitted to the four calendars at its signing (`ATTESTATION_v1.3.0.txt.ots`); it depends on the calendars until it is upgraded once the commitments are confirmed in Bitcoin blocks.
- **v1.3.1** — submitted to the four calendars at its signing (`ATTESTATION_v1.3.1.txt.ots`); it depends on the calendars until it is upgraded once the commitments are confirmed in Bitcoin blocks.
- **v1.3.2** — submitted to the four calendars at signing (`ATTESTATION.txt.ots`); it depends on the calendars until it is upgraded once the commitments are confirmed in Bitcoin blocks.

No proof before v1.2.1 now depends on a calendar server remaining available, and each remains valid evidence for its own root, superseded or current. **One limit is stated rather than glossed:** the block heights above are those the four calendars returned on `ots verify` and `ots upgrade`; no local Bitcoin node was available on the machine the upgrade was run from, so the block headers themselves have not been independently verified here.


---

## Re-signing

**Re-sign after any material change to the standard.** Regenerate the manifest, re-sign, commit, and record the new root hash here. A signature over stale content is worse than none, because it invites the argument that the signed version and the circulated version are different documents.

---

*Generated 30 July 2026. Revised on re-signing, 30 July 2026 (v1.0.1), 31 July 2026 (v1.0.2 and v1.0.3), 25 August 2026 (v1.1.0), 27 August 2026 (v1.1.1), 15 September 2026 (v1.2.0), 28 September 2026 (v1.2.1), 3 October 2026 (v1.3.0), 3 October 2026 (v1.3.1) and 3 October 2026 (v1.3.2); cleaned for publication on 3 October 2026, one edition for the public and the private repository.*
