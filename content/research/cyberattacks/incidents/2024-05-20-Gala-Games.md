---
date: 2024-05-20
target-entities: Gala Games
entity-types:
  - GameFi
attack-types:
  - Access Control Compromise
title: "Gala Games Suffers 5 Billion GALA Mint via Compromised Minter Account"
loss: 22500000
---

## Summary

- On May 20, 2024, an attacker gained control of a [dormant MINTER account](https://rekt.news/gala-games-rekt/) on the GALA token contract of blockchain gaming platform Gala Games and minted 5 billion GALA tokens, valued at approximately $200-216 million at the time ([Halborn](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024)).
- The attacker sold roughly 592 million GALA for approximately [5,913 ETH (~$21.8-22.5 million)](https://www.theblock.co/news/web3/2024-05-21-gala-games-exploiter-returns-21-million-taken-from-the-200-million-exploit-295723) over roughly two hours before Gala invoked the contract's address blocklist to freeze the remaining ~4.4 billion minted tokens ([Halborn](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024)).
- The following day the exploiter returned the ETH to Gala-controlled wallets; Gala suffered no realized treasury loss. GALA fell roughly 15-19% during the sell-off.
- Root cause was access-control failure on a single privileged minter key that had been dormant for approximately 180 days with no rotation or monitoring.

## Attackers

- No attacker has been publicly named as of May 2024 (the latest date covered by available primary sources). Gala stated the token contract itself was not breached — rather, the [mint authority was compromised](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024) — and CEO Eric Schiermeyer stated a culprit had been identified and that the company was working with law enforcement ([CoinDesk](https://www.coindesk.com/markets/2024/05/21/gala-games-hacker-returns-23m-in-eth-founder-proposes-buy-and-burn/)).
- The incident came three days after Gala's President of Blockchain stepped down to an unpaid advisor role; media coverage noted this timing alongside historical co-founder litigation, but no public evidence connected personnel changes to the exploit.

## Losses

- 5 billion GALA minted via the compromised MINTER account, valued at approximately $200-216 million at time of minting ([rekt.news](https://rekt.news/gala-games-rekt/) / [Halborn](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024)).
- The attacker converted [~592 million GALA into 5,913 ETH (~$21.8-22.5 million)](https://www.theblock.co/news/web3/2024-05-21-gala-games-exploiter-returns-21-million-taken-from-the-200-million-exploit-295723) before the blocklist froze the address.
- The stolen ETH was [returned in full on May 21, 2024](https://www.coindesk.com/markets/2024/05/21/gala-games-hacker-returns-23m-in-eth-founder-proposes-buy-and-burn/); realized net loss to Gala treasury was zero.
- The remaining ~4.4 billion minted GALA were frozen via the contract's blocklist function ([Halborn](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024)).
- GALA price fell approximately [15%](https://www.theblock.co/news/ecosystems/2024-05-20-gala-games-hacked-gala-token-plummets-295520) during the sell-off window.

## Timeline

- **2021:** Co-founder Eric Schiermeyer sued co-founder Wright Thurston in litigation that included allegations regarding approximately [8.65 billion GALA (~$130 million)](https://www.theblock.co/post/248897); these amounts were allegations in the lawsuit, not established court findings.
- **May 2023:** The GALA V2 token contract launched, which included an address-blocklist capability later used to freeze the exploiter's address.
- **November 2022:** A wallet appeared to mint billions of GALA on the V1 contract, briefly crashing the token ~25% before Gala denied an attack ([CryptoTimes](https://cryptotimes.io/gala-games-denies-hack-after-gala-token-crashes-25/)); this pGALA-era event preceded and motivated the V2 migration.
- **May 17, 2024:** President of Blockchain Jason Brink moved to an unpaid advisor role; several staff resigned ([rekt.news](https://rekt.news/gala-games-rekt/)).
- **May 20, 2024:** The attacker minted 5 billion GALA via the dormant MINTER account and began swapping to ETH; Gala invoked the blocklist after roughly two hours of swapping ([Halborn](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024)).
- **May 21, 2024:** The exploiter returned 5,913.2 ETH to Gala-controlled wallets; Schiermeyer announced a buy-and-burn proposal for the frozen tokens and DWF Labs purchased 28 million GALA ([CoinDesk](https://www.coindesk.com/markets/2024/05/21/gala-games-hacker-returns-23m-in-eth-founder-proposes-buy-and-burn/)).

## Security Failure Causes

- **Single privileged minter key without multisig protection (root cause):** The MINTER account held a private key capable of minting the entire token supply, controlled by one party without multisig or timelock protection. The key sat dormant for ~180 days before compromise, with no rotation or usage alerting ([Halborn](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024)).
- **Mint authority persisted across the V1-to-V2 migration:** The mint role remained active on the deployed contract rather than being revoked or redistributed, so a single key compromise translated directly into unlimited supply fabrication.
- **Anomaly response depended on manual intervention:** The blocklist function existed on V2 but was invoked only after roughly two hours of swapping; no automated circuit breaker halted unusual minting or large sells at the contract level ([Halborn](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024)).
