# Attestant: Learn2Earn on Hedera (UI prototype)

> **Beta.** Static design prototype: a landing page and an interactive product UI mock-up.

**Attestant** is a Learn2Earn platform where *proof travels with the person who earned it*. Candidates take issuer-run courses and earn verifiable, **soulbound** credentials on the **Hedera** network. Organisations hire against those credentials instead of re-running vetting, and funders get paid back when training leads to a job.

This repository holds the **front-end design** of the product. The working Hedera testnet implementation lives in **[testify](https://github.com/fidaaltf58/testify)**.

---

## The problem

Three parties fail at the same moment, for the same reason:

- **Candidate**: finishes a course but can't prove it to anyone who wasn't there.
- **Employer**: meets that candidate, then re-runs verification someone else already did.
- **Funder**: paid for the course but can't find out whether it led to a job.

## The one rule

> *Whatever confers access cannot be bought. Whatever can be bought confers nothing.*

## Five on-chain assets

| Asset | Kind | What it does | Held by |
|---|---|---|---|
| **XP Tokens** | soulbound | Accrue through the small events of learning; the engagement layer, per issuer | Candidate |
| **Course Credentials** | soulbound | Issuer-signed proof that a specific competency was completed | Candidate |
| **Reputation Credentials** | soulbound | What others (employers, peers) attest about you | Candidate |
| **Reward Tokens** | tradeable | Reserve-backed, Rand-denominated, spendable at approved vendors. They open no doors. | Candidate |
| **Impact Certificates** | tradeable | Mint when a first credential is followed by a co-signed employment event | Issuer, never the candidate |

## How the loop closes

```
Funder capitalises pool ──► Reserve pool (issuer-held)
                                   │
                                   ▼
             Learner earns XP + Reward Tokens through courses
                                   │
                                   ▼
          Credential ──► Employment event (org + candidate co-sign)
                                   │
                                   ▼
          Impact Certificate mints (issuer-owned) ──► sold back to funder
                                   │
                                   └──► capital recycles into more skilling
```

## Architecture (as designed)

- **HTS (Hedera Token Service)** issues the XP, credential, reward, and impact tokens.
- **HCS (Hedera Consensus Service)** publishes credentials, outreach records, and the issuer-key registry.
- **Per-issuer sovereignty:** one DAO per issuer, with voting weight equal to the soulbound XP held with that issuer.
- **Non-custodial onboarding:** the operator creates the candidate's Hedera account at signup and hands over the key, so no wallet install is needed to start.
- **Verification without a middleman:** issuer keys resolve through a public HCS registry via mirror nodes, never through an operator-hosted API.
- **Postings as predicates:** organisations write job requirements as queries over a candidate's holdings, and qualification returns yes or no. Candidates choose what else to reveal.

## What's in this repo

| File | Description |
|---|---|
| `attestant-landing.html` | Marketing landing page: problem, the one rule, asset ledger, loop diagram, product preview, architecture, and calls to action for candidates, organisations, and funders |
| `attestant-app-ui.html` | Interactive product UI mock-up with two personas: **Candidate** (dashboard, courses, job board, credentials, wallet, governance, settings) and **Organisation** (dashboard, courses, post a job, search candidates, issue credential, employment events) |

Both files are self-contained: plain HTML with inline CSS and JavaScript, and no build step or dependencies.

## Running it

Open either file in a browser:

```bash
git clone https://github.com/fidaaltf58/DDIB.git
cd DDIB
start attestant-landing.html      # Windows
# open attestant-landing.html     # macOS
# xdg-open attestant-landing.html # Linux
```

Or serve the folder locally:

```bash
python -m http.server 8000
# → http://localhost:8000/attestant-landing.html
```

All data shown in the UI is mock data.

## Related

- **[testify](https://github.com/fidaaltf58/testify)**: Node.js backend and live UI that implement this design on Hedera testnet (account signup, XP and reward tokens, soulbound credential NFTs, HCS outreach records).

## Author

**Fidaa Letaief** · [@fidaaltf58](https://github.com/fidaaltf58)
