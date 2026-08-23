---
date: 2025-05-22
target-entities: Cetus Protocol
entity-types:
  - DeFi
attack-types:
  - Smart Contract Exploit
  - Integer Overflow
title: "Cetus Protocol Suffers $223 Million Liquidity Math Exploit"
loss: 223000000
---

## Summary

On May 22, 2025, Cetus Protocol, the largest decentralized exchange on the Sui blockchain, was [drained of approximately $223 million](https://rekt.news/en/cetus/) when an attacker exploited an integer-overflow flaw in the protocol's concentrated-liquidity math. The attacker borrowed tokens via a flash swap, opened a liquidity position spanning a narrow tick range, and abused a faulty overflow check in the shared `checked_shlw(u256)` function of the integer-mate math library so that a [single-unit deposit minted the pool's entire liquidity](https://blog.verichains.io/p/cetus-protocol-hacked-analysis), then withdrew it for real SUI and USDC. Sui validators [froze $162 million](https://rekt.news/en/cetus/) of the stolen funds mid-heist through an emergency consensus vote, while over $60 million had already been bridged to Ethereum via Wormhole and converted to roughly 21,000 ETH. Zellic, whose audit of Cetus was completed 41 days before the exploit, stated the flaw lived in the integer-mate library's `checked_shlw` method, which [was not in the scope of its audit](https://rekt.news/en/cetus/). Cetus later offered the attacker a $6 million whitehat settlement, then a [$5 million bounty for information leading to arrest](https://rekt.news/en/cetus/); the attacker never responded. Verichains subsequently identified the same vulnerable shared math function in [other Sui protocols](https://blog.verichains.io/p/multiple-sui-projects-previously) (Kriya, FlowX, Turbos), two of which quietly patched it.

## Attackers

The attacker's identity remains unknown. No attribution has been published by Cetus, Sui Foundation, or law enforcement as of August 17, 2026. On-chain investigators tracked the exploit to a Sui address, with funds bridged to Ethereum wallet [0x0251536BfcF144B88e1aFa8fe60184Ffdb4cAF16](https://rekt.news/en/cetus/), which received approximately 20,000 ETH in a [batch transfer](https://rekt.news/en/cetus/) (tx `0x787a0bc6305f26c9c6b78155f3271d4f3b8c321245881ee068a84dba04c8c2c0`) from the exploit transaction proceeds. Cetus and Inca Digital [published an on-chain message](https://rekt.news/en/cetus/) offering the attacker a whitehat settlement — keep 2,324 ETH (~$6M) and return the rest — followed by a $5 million bounty announcement for identification and arrest, funded with support from Inca Digital and the Sui Foundation. Neither elicited a response.

## Losses

- [Over $223 million](https://rekt.news/en/cetus/) drained from Cetus Protocol liquidity pools on May 22, 2025; [over $260 million](https://blog.verichains.io/p/cetus-protocol-hacked-analysis) per Verichains' initial damage estimate
- [$162 million frozen](https://rekt.news/en/cetus/) by Sui validators via emergency vote mid-attack; [$60+ million already bridged](https://cryptonews.com/news/cetus-protocol-hacked-for-200m-sui-price-crashes-as-60m-usdc-moved-to-ethereum) to Ethereum via Wormhole and converted to ~21,000 ETH
- Sui ecosystem tokens dumped [at least 75-80% in minutes](https://rekt.news/en/cetus/); SUI fell ~7%, [CETUS token fell 40%](https://blog.verichains.io/p/cetus-protocol-hacked-analysis)
- Every Cetus AMM pool was affected; neighboring Sui DEXs Bluefin and Momentum [paused all activity](https://rekt.news/en/cetus/) as a precaution
- Same shared-vulnerability exposure found post-incident at Kriya ($10M TVL), FlowX ($4.6M TVL), and Turbos ($10.3M TVL) — [~$24.6M combined TVL](https://rekt.news/en/cetus/) on the same broken math

## Timeline

- **May 22, 2025 (~10:30 UTC):** Attacker executes the flash-swap + overflow exploit on the SCA/SUI pool ([exploit transaction](https://suivision.xyz/txblock/ETCaBBiffASZ3oXBBcoM6VYd3NcTb5T1Sqo4xLECKZws?tab=Overview)), draining liquidity across every Cetus AMM pool.
- **May 22, 2025:** Over $60M bridged to Ethereum via Wormhole as USDC, swapped to ~21,000 ETH; funds consolidated to wallet 0x0251536BfcF144B88e1aFa8fe60184Ffdb4cAF16.
- **May 22, 2025:** Sui validators execute an emergency vote and [freeze $162 million](https://rekt.news/en/cetus/) of attacker funds; Cetus pauses its smart contracts; Bluefin and Momentum pause as precautions; ecosystem tokens crash up to 80%.
- **May 22, 2025:** [Verichains publishes](https://blog.verichains.io/p/cetus-protocol-hacked-analysis) root-cause analysis using its Revela Move decompiler, identifying the mis-sized overflow check in `checked_shlw(u256)`.
- **~May 23, 2025:** Zellic clarifies the vulnerability was in the integer-mate library's `checked_shlw` method, [outside its audit scope](https://rekt.news/en/cetus/) (audit completed April 11, 2025 — 41 days before the exploit).
- **~May 23, 2025:** Cetus and Inca Digital publish an on-chain whitehat offer: return funds, keep 2,324 ETH (~$6M).
- **May 23, 2025:** With no attacker response, Cetus announces a [$5M bounty](https://rekt.news/en/cetus/) for identification and arrest of the hacker, supported by Inca Digital and Sui Foundation.
- **May 27, 2025:** Sui Foundation [announces an on-chain community vote](https://blog.sui.io/cetus-incident-response-onchain-community-vote/) on a protocol upgrade to reclaim the frozen attacker funds without requiring the attacker's signature.
- **Post-incident:** Verichains reveals the same vulnerable shared math function in [multiple other Sui projects](https://blog.verichains.io/p/multiple-sui-projects-previously); Kriya and FlowX patch silently; Turbos claims independence.
- **~June 2025:** Cetus announces a [recovery/compensation plan](https://rekt.news/en/cetus/) for affected liquidity providers, backed by Sui Foundation support.

## Security Failure Causes

**Mis-sized overflow check in shared math library (root cause):** The `checked_shlw(u256)` function in the integer-mate library was designed to abort when a 256-bit value shifted left by 64 bits would overflow. Its upper-bound constant was [wrong by a factor of 2^64](https://blog.verichains.io/p/cetus-protocol-hacked-analysis) (`0xFFFFFFFFFFFFFFFF << 192` instead of `1 << 192`), so sufficiently large shifts wrapped silently modulo 2^256 instead of aborting.

**Liquidity math trusted the broken shift:** `get_delta_a` used `checked_shlw` to scale intermediates by 2^64 when computing required token deposits. After the silent wrap, the computed deposit collapsed to a [trivially small residue — often 1 unit](https://blog.verichains.io/p/cetus-protocol-hacked-analysis) — regardless of the pool's true liquidity, letting the attacker mint the entire pool liquidity for a single token.

**Audit scope excluded the dependency that broke:** Cetus had passed multiple audits, including Zellic's completed April 11, 2025. The vulnerability lived in the integer-mate library, which Zellic [confirmed was not in scope](https://rekt.news/en/cetus/) of its audit. The mathematical foundation the protocol depended on was excluded from the audit that was completed 41 days before it collapsed.

**Flash-loan leverage amplified a math bug into pool drainage:** The attacker combined the overflow with a flash swap (borrowing 20,402,195,370,006 SCA units — approximately 20.4 trillion), opening a [200-tick-wide position](https://blog.verichains.io/p/cetus-protocol-hacked-analysis) at ticks 300,000–300,200, minting full pool liquidity for 1 unit, then removing exactly the flash-loan-sized liquidity slice to repay and keep the residual — all in one transaction. Dedaub noted the protocol [had overflow checks, but not on this path](https://rekt.news/en/cetus/).

**Shared dependency = systemic risk:** The same `checked_shlw` function was copy-pasted across the Sui ecosystem. Verichains found it in [Kriya, FlowX, and Turbos](https://blog.verichains.io/p/multiple-sui-projects-previously) (~$24.6M combined TVL); Kriya and FlowX patched after the Cetus meltdown, and Turbos carried the vulnerable-but-unused code (["dead code is not safe code"](https://blog.verichains.io/p/multiple-sui-projects-previously)). No pre-incident process existed to track shared-math exposure across protocols.

**Emergency response strained decentralization norms:** Per the Sui Foundation, the freeze was executed through a [validator/community vote and a protocol upgrade](https://blog.sui.io/cetus-incident-response-onchain-community-vote/) that reclaimed the frozen funds without the attacker's signature. Rekt characterizes the same response as an effective but [centralized override of normal protocol rules](https://rekt.news/en/cetus/) — effective because attacker funds were still on Sui when the vote passed, while the $60M already on Ethereum was beyond reach.
