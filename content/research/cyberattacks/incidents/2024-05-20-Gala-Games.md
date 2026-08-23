---
date: 2024-05-20
target-entities: Gala Games
entity-types:
  - Blockchain Gaming Platform
attack-types:
  - Access Control Compromise
title: "Gala Games Suffers $216 Million GALA Token Mint Exploit"
loss: 216000000
---

## Summary

On May 20, 2024, an attacker gained control of a [dormant MINTER account](https://rekt.news/gala-games-rekt/) on the GALA token contract of blockchain gaming platform Gala Games and minted 5 billion GALA tokens worth approximately [$216 million](https://rekt.news/gala-games-rekt/). The attacker sold roughly 592 million GALA — about [$21.8-22.5 million](https://www.theblock.co/news/web3/2024-05-21-gala-games-exploiter-returns-21-million-taken-from-the-200-million-exploit-295723) in ETH — over roughly two hours before Gala invoked the contract's address blocklist to freeze the remaining ~4.4 billion minted tokens ([Halborn](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024)). In an unusual resolution, the exploiter [returned 5,913.2 ETH (~$22.5 million)](https://www.theblock.co/news/web3/2024-05-21-gala-games-exploiter-returns-21-million-taken-from-the-200-million-exploit-295723) to wallets under Gala control the following day, leaving Gala with no net loss of treasury funds. GALA fell roughly [15-19%](https://www.coindesk.com/markets/2024/05/21/gala-games-hacker-returns-23m-in-eth-founder-proposes-buy-and-burn/) during the sell-off. Gala CEO Eric Schiermeyer stated a culprit had been identified and that the company was [working with the FBI and DOJ](https://www.coindesk.com/markets/2024/05/21/gala-games-hacker-returns-23m-in-eth-founder-proposes-buy-and-burn/), though no public charging or enforcement followed. The incident came three days after Gala's President of Blockchain [stepped down to an unpaid advisor role](https://rekt.news/gala-games-rekt/), fueling unconfirmed insider speculation.

## Attackers

No attacker has been publicly named. Gala stated the token contract itself was not breached — rather, the [mint authority was compromised](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024) — and that the culprit had been identified with law-enforcement cooperation underway ([CoinDesk](https://www.coindesk.com/markets/2024/05/21/gala-games-hacker-returns-23m-in-eth-founder-proposes-buy-and-burn/)). Security commentary focused on the access-control failure: the compromised MINTER key had been [dormant for approximately 180 days](https://rekt.news/gala-games-rekt/). The timing — three days after the President of Blockchain's demotion and amid [public co-founder litigation dating to 2021](https://www.theblock.co/post/248897) — prompted insider speculation in media coverage, but no attribution was ever confirmed and Halborn characterized the insider theory as a hypothesis rather than a finding.

## Losses

- [5 billion GALA minted](https://rekt.news/gala-games-rekt/), worth approximately $216 million at peak valuation (~$200 million per [Halborn's estimate](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024)).
- The attacker cashed out [~592 million GALA for 5,913 ETH (~$21.8-22.5 million)](https://www.theblock.co/news/web3/2024-05-21-gala-games-exploiter-returns-21-million-taken-from-the-200-million-exploit-295723) before the blocklist froze the address.
- The stolen ETH was [returned in full the next day](https://www.coindesk.com/markets/2024/05/21/gala-games-hacker-returns-23m-in-eth-founder-proposes-buy-and-burn/), so Gala suffered no realized treasury loss.
- The remaining ~4.4 billion minted GALA were [frozen via the blocklist function](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024).
- GALA price fell approximately [15-19%](https://www.theblock.co/news/ecosystems/2024-05-20-gala-games-hacked-gala-token-plummets-295520) on the incident.

## Timeline

- **2021:** Approximately [8.65 billion GALA were stolen (~$130 million)](https://www.theblock.co/post/248897) in a prior incident; co-founder Schiermeyer sued co-founder Thurston in a dispute that included claims over the stolen tokens.
- **May 2022:** The [V2 token contract added an address-blocklist capability](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024) — the control that would later stop the 2024 drain.
- **November 2022:** A wallet appeared to mint billions of GALA, briefly crashing the token ~25% before Gala denied an attack ([CryptoTimes](https://cryptotimes.io/gala-games-denies-hack-after-gala-token-crashes-25/)).
- **May 17, 2024:** President of Blockchain Jason Brink [moved to an unpaid advisor role](https://rekt.news/gala-games-rekt/); several staff resigned.
- **May 20, 2024:** The attacker minted 5 billion GALA via the dormant MINTER account and began swapping to ETH; Gala [invoked the blocklist](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024) after roughly two hours.
- **May 21, 2024:** The exploiter [returned 5,913.2 ETH](https://www.theblock.co/news/web3/2024-05-21-gala-games-exploiter-returns-21-million-taken-from-the-200-million-exploit-295723) to Gala-controlled wallets; Schiermeyer announced a [buy-and-burn proposal](https://www.coindesk.com/markets/2024/05/21/gala-games-hacker-returns-23m-in-eth-founder-proposes-buy-and-burn/) for the frozen tokens and DWF Labs purchased 28 million GALA.

## Security Failure Causes

**Single privileged minter key without multisig protection (root cause):** The MINTER account held a private key capable of minting the entire token supply, controlled by one party with no multisig or timelock. The key sat [dormant for ~180 days](https://rekt.news/gala-games-rekt/) before compromise — a period with no rotation, no anomaly monitoring, and no usage alerting, per [Halborn's analysis](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024).

**Mint authority persisted on a legacy account:** The V2 contract retained the mint role rather than revoking or redistributing it, so a single key compromise translated directly into unlimited supply fabrication.

**Anomaly response depended on manual intervention:** The blocklist function existed since 2022 but was only invoked after ~[two hours of swapping](https://www.halborn.com/blog/post/explained-the-gala-games-hack-may-2024); no automated circuit breaker halted minting or large sells at the contract level.

**Governance turbulence as an unquantified insider-risk surface:** The demotion of the President of Blockchain three days prior and the [ongoing co-founder litigation](https://www.theblock.co/post/248897) created the conditions media coverage flagged for insider speculation — unconfirmed, but a reminder that key-custody practices during organizational upheaval are an attack surface audits do not cover.
