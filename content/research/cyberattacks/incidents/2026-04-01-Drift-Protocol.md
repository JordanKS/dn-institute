---
date: 2026-04-01
target-entities: Drift Protocol
entity-types:
  - DeFi Protocol
attack-types:
  - Social Engineering
  - Multisig Key Compromise
  - Oracle Manipulation
title: "Drift Protocol: $285 Million Exploit via Compromised Admin Keys"
loss: 285000000
---

## Summary

On April 1, 2026, beginning at approximately [16:05 UTC](https://www.chainalysis.com/blog/lessons-from-the-drift-hack/), an attacker gained admin control of **Drift Protocol**, the largest decentralized perpetual futures exchange on Solana, and drained an estimated **[USD 285 million](https://www.trmlabs.com/resources/blog/north-korean-hackers-attack-drift-protocol-in-285-million-heist)** (over 50% of its TVL) from its vaults — the largest DeFi hack of 2026 and the [second-largest security failure in Solana's history](https://www.chainalysis.com/blog/lessons-from-the-drift-hack/), behind only the USD 326 million Wormhole bridge hack of 2022. The attack combined three coordinated elements documented across the post-mortems: attackers [manufactured a fake token (CarbonVote, "CVT") and manipulated Drift's oracle into pricing it as collateral](https://rekt.news/drift-protocol-rekt); abused Solana's ["durable nonce" feature](https://cointelegraph.com/news/drift-280-million-hack-questions-circle-response) to obtain pre-signed transactions from Security Council signers; and used those signed transactions to hand over admin control, raise withdrawal caps, and [drain roughly $285 million in real assets](https://www.quillaudits.com/blog/hack-analysis/drift-protocol-multisig-exploit). Helius CEO Mert [raised the first public alarm](https://x.com/mert/status/2039391215284519045) roughly an hour before Drift's [official acknowledgment](https://x.com/DriftProtocol/status/2039404931778535427), which told users not to deposit and added that "this is not an April Fools joke." No compensation plan has been published; Drift said it is working with [Asymmetric Research and OtterSec](https://x.com/DriftProtocol/status/2041574840524493091) and joining the Solana Foundation's STRIDE program.

## Attackers

Attribution points to North Korean (DPRK) state-linked actors. On April 2, [TRM Labs](https://www.trmlabs.com/resources/blog/north-korean-hackers-attack-drift-protocol-in-285-million-heist) said its investigation suggested the hack was "likely perpetrated by North Korean hackers." The same day, [Elliptic told CoinDesk](https://www.coindesk.com/business/2026/04/02/north-koreans-hackers-likely-behind-the-usd286-million-drift-protocol-exploit-elliptic) the actors were likely DPRK-linked, calling it the eighteenth such operation Elliptic tracked in 2026. [Chainalysis](https://www.chainalysis.com/blog/lessons-from-the-drift-hack/) said preliminary on-chain indicators were consistent with previously attributed DPRK operations, though formal attribution was then pending.

On April 4, [Drift published an Incident Background Update](https://x.com/DriftProtocol/status/2040611161121370409) and, working with the SEAL 911 team, assessed [with medium-high confidence](https://x.com/DriftProtocol/status/2040611161121370409) that the operation was carried out by **UNC4736**, a DPRK state-affiliated group also tracked as AppleJeus or Citrine Sleet — with on-chain fund flows linked to actors behind the [October 2024 Radiant Capital (~$53M) hack](https://www.halborn.com/blog/post/explained-the-radiant-capital-hack-october-2024). Drift stressed the [individuals who appeared in person were not North Korean nationals](https://x.com/DriftProtocol/status/2040611161121370409), noting DPRK operations layer third-party intermediaries with fully constructed identities.

## Losses

- Estimated [~$285 million (over 50% of TVL)](https://www.chainalysis.com/blog/lessons-from-the-drift-hack); the reported per-asset drain total was ~$285.26 million.
- The largest single drawdown, per the on-chain analysis, was **JLP (Jupiter): 42.72M tokens ≈ $159.35M**; then **USDC: 71.42M ≈ $71.42M**; **cbBTC: ~164.35 BTC ≈ $11.29M**; **USDT: 5.65M ≈ $5.65M**; with smaller drawdowns across USDS, WETH, dSOL, WBTC, Fartcoin, JitoSOL, syrupUSDC, INF, mSOL, bSOL, EURC, zBTC, USDY, and JUP. [Full audit breakdown on the on-chain analysis](https://rekt.news/drift-protocol-rekt).
- The vault balance [fell from about $309 million to about $41 million](https://rekt.news/drift-protocol-rekt) during the drain, later falling below $8 million.
- The DRIFT token [fell more than 40%](https://www.trmlabs.com/resources/blog/north-korean-hackers-attack-drift-protocol-in-285-million-heist) after the exploit.
- TRM reported most stolen funds were bridged to Ethereum within hours; per investigator ZachXBT, [over $230 million in USDC crossed Circle's Cross-Chain Transfer Protocol (CCTP) to Ethereum in 100+ transactions over about six hours](https://x.com/zachxbt/status/2039566991858794981), while SOL was bridged separately via Chainflip.

## Timeline

- **~October 2025:** A group [posing as a quantitative trading firm approached Drift contributors at a crypto event](https://x.com/DriftProtocol/status/2040611161121370409) and began months of relationship-building, including a Telegram group.
- **December 2025 – January 2026:** The group [onboarded an "Ecosystem Vault" on Drift and deposited over $1M of its own capital](https://www.theblock.co/post/396361/drift-links-280-million-exploit-to-six-month-social-engineering-op-run-by-suspected-north-korean-actors) to build legitimacy.
- **March 11–12, 2026:** On-chain staging began with a [10 ETH Tornado Cash withdrawal](https://rekt.news/drift-protocol-rekt); the attacker then created CarbonVote (CVT) with hundreds of millions of units minted and a wash-traded near-$1 price history.
- **March 23:** The attacker [created durable nonce accounts](https://rekt.news/drift-protocol-rekt), some linked to Drift Security Council members, and within days obtained a pre-signed nonce from a replacement signer.
- **Late March:** Drift [migrated its Security Council multisig to  2-of-5 threshold with zero timelock](https://rekt.news/drift-protocol-rekt) — removing the review delay.
- **April 1, ~16:05 UTC:** The [pre-signed transactions fired](https://rekt.news/drift-protocol-rekt); an attacker took over Drift's State account, created a highly-permissive CVT collateral position, lifted withdrawal caps, and a cascade of withdrawals (about [128 seconds of active drain](https://www.quillaudits.com/blog/hack-analysis/drift-protocol-multisig-exploit)) emptied major vaults. [Drift suspended deposits and withdrawals](https://x.com/DriftProtocol/status/2039417136729227425) while confirming an active attack.
- **April 2, 2026:** [TRM and Elliptic](https://www.coindesk.com/business/2026/04/02/north-koreans-hackers-likely-behind-the-usd286-million-drift-protocol-exploit-elliptic) publicly attributed the theft to likely DPRK actors.
- **April 4, 2026:** [Drift published its Incident Background Update](https://x.com/DriftProtocol/status/2040611161121370409), the six-month operation and an UNC4736 (medium-high confidence) designation.
- **April 9, 2026:** [Chainalysis published its analysis](https://www.chainalysis.com/blog/lessons-from-the-drift-hack/); Drift later posted an interim update recognizing the impact on users and builders.

## Security Failure Causes

**Social engineering into developer teams (initial access):** Per Drift's own post-mortem, the operators [built in-person and working relationships with contributors over about six months](https://x.com/DriftProtocol/status/2040611161121370409), then shared repository / TestFlight software that likely carried a zero-click code-execution vector (VSCode/Cursor file-open bug flagged since late 2025).

**Multisig "durable nonce" pre-approval abuse:** Solana's legitimate durable-nonce capability (pre-sign for non-expiring future execution) enabled [pre-signed admin transfers from Security Council members](https://cointelegraph.com/news/drift-280-million-hack-questions-circle-response); signers approved work they did not realize contained hidden admin authorizations — what Drift characterized as targeted social-engineering / transaction misrepresentation.

**Zero-timelock Security Council migration:** The [2-of-5 threshold with zero timelock](https://rekt.news/drift-protocol-rekt) meant any two signers could authorize immediate, irreversible admin changes with no delay — TRM flagged the [removal of this review window as a central safety failure](https://www.trmlabs.com/resources/blog/north-korean-hackers-attack-drift-protocol-in-285-million-heist).

**Oracle manipulation via fake collateral:** A worthless fake asset with a few thousand dollars in seed liquidity and heavy wash trading was treated by Drift's oracles as collateral worth hundreds of millions of dollars — TRM cited this as a need for [minimum-liquidity thresholds, time-weighted pricing, and circuit breakers](https://www.trmlabs.com/resources/blog/north-korean-hackers-attack-drift-protocol-in-285-million-heist).

**Admin authority without layered controls:** The signer key held full control over market creation, oracle assignment, and withdrawal limits with no comparable protections, so a human-chosen compromise was enough to strip the vaults. Drift's authority model had been reviewed in a [2024 Neodyme security audit](https://rekt.news/drift-protocol-rekt) that treated it as an acceptable trust assumption — a reminder that no code audit can catch a human compromise.