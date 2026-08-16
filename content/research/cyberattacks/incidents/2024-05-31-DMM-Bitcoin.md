---
date: 2024-05-31
target-entities: DMM Bitcoin
entity-types:
  - Exchange
attack-types:
  - Private Key Leak
  - Phishing
title: "DMM Bitcoin Suffers $305 Million Bitcoin Hack"
loss: 305000000
---

## Summary

On May 31, 2024, Japanese cryptocurrency exchange [DMM Bitcoin](https://bitcoin.dmm.com/) disclosed an [unauthorized leak of Bitcoin from its wallet](https://bitcoin.dmm.com/news/20240531_01) amounting to [4,502.9 BTC, approximately 48.2 billion yen ($305 million)](https://www.coindesk.com/business/2024/05/31/japanese-crypto-exchange-dmm-bitcoin-suffers-305m-hack). The exchange stated that the outflow was not caused by a breach of its core trading system, and immediately froze withdrawals, halted new account openings, and restricted spot trading to sell orders only. DMM Bitcoin [guaranteed all customer Bitcoin deposits in full](https://techcrunch.com/2024/05/31/hackers-steal-305-million-from-dmm-bitcoin-crypto-exchange/) and later secured approximately [50 billion yen ($320 million) in support from group companies](https://invezz.com/news/2024/06/05/dmm-bitcoin-to-compensate-customers-affected-by-the-hack/) to procure replacement BTC. Chainalysis ranked the incident as the [seventh-largest crypto hack ever recorded](https://x.com/chainalysis/status/1796571757341765916) at the time. In February 2025, Japan's National Police Agency, the FBI, and the U.S. DoD Cyber Crime Center [jointly attributed the theft](https://www.npa.go.jp/bureau/cyber/pdf/20250204_tt.pdf) to the North Korean state-linked TraderTraitor threat group, considered part of the Lazarus Group.

## Attackers

The theft was [jointly attributed](https://www.npa.go.jp/bureau/cyber/pdf/20250204_tt.pdf) by Japan's National Police Agency (Kanto Regional Police Bureau National Cyber Department and the Tokyo Metropolitan Police Department), the FBI, and the U.S. Department of Defense Cyber Crime Center (DC3) to **TraderTraitor**, a North Korean cyber threat actor considered part of the [Lazarus Group](https://www.npa.go.jp/bureau/cyber/pdf/20250204_tt.pdf), a subordinate organization of North Korean state authorities. The investigation found the initial access was obtained through a [North Korean social engineering scheme](https://www.npa.go.jp/bureau/cyber/pdf/20250204_tt.pdf) targeting an employee, rather than a technical breach of exchange infrastructure.

On-chain investigator [ZachXBT traced more than $35 million](https://coinedition.com/zachxbt-uncovers-new-evidence-in-305-million-dmm-bitcoin-hack-investigation/) of the stolen funds being laundered through the Cambodian online marketplace Huione Guarantee, identifying similarities in off-chain indicators with prior Lazarus operations. The laundering pattern involved channeling the stolen BTC through a transaction mixer, bridging from Bitcoin to Ethereum or Avalanche via THORChain, Threshold, or Avalanche Bridge, and then swapping into other assets. In July 2024, [Tether blacklisted a Huione-linked wallet](https://coinedition.com/zachxbt-uncovers-new-evidence-in-305-million-dmm-bitcoin-hack-investigation/) holding 29.6 million USDT on Tron, into which approximately $14 million of DMM hack proceeds had flowed within three days.

## Losses

- [4,502.9 BTC](https://www.coindesk.com/business/2024/05/31/japanese-crypto-exchange-dmm-bitcoin-suffers-305m-hack) stolen in a single unauthorized outflow
- Approximately [48.2 billion yen ($305 million)](https://cryptonews.com/news/bitcoin-hack-japanese-exchange-305-million/) at the time of the incident
- Ranked by Chainalysis as the [seventh-largest cryptocurrency hack in history](https://x.com/chainalysis/status/1796571757341765916) at the time of the theft
- For scale comparison: the loss was the largest at a Japanese exchange since the [Coincheck theft of 58 billion yen ($532 million)](https://cryptonews.com/news/bitcoin-hack-japanese-exchange-305-million/) in 2018, and approached the scale of the 2014 Mt. Gox collapse ($450 million)

## Timeline

- **May 31, 2024:** DMM detects and discloses an [unauthorized leak of 4,502.9 BTC](https://bitcoin.dmm.com/news/20240531_01) from its wallet, states that customer deposits will be "fully guaranteed," and implements emergency restrictions: withdrawal freezes, suspension of new account screenings, spot trading limited to sell orders, and no new leveraged positions.
- **May 31, 2024:** International press confirms the [$305 million loss](https://www.coindesk.com/business/2024/05/31/japanese-crypto-exchange-dmm-bitcoin-suffers-305m-hack); Chainalysis [ranks it the 7th largest crypto hack ever](https://x.com/chainalysis/status/1796571757341765916).
- **June 2024:** DMM Group announces it will procure the equivalent amount of leaked BTC with support from group companies; the company subsequently [raises approximately 50 billion yen ($320 million)](https://invezz.com/news/2024/06/05/dmm-bitcoin-to-compensate-customers-affected-by-the-hack/) to fund the guarantees. Japan's Financial Services Agency [demands a detailed report](https://invezz.com/news/2024/06/05/dmm-bitcoin-to-compensate-customers-affected-by-the-hack/) on the hack and the compensation plan.
- **June 2024:** Arkham Intelligence [offers a 1,000 ARKM token bounty](https://x.com/ArkhamIntel/status/1796563505782337949) for information on the incident.
- **July 2024:** [ZachXBT publishes tracing evidence](https://coinedition.com/zachxbt-uncovers-new-evidence-in-305-million-dmm-bitcoin-hack-investigation/) linking the hack to Lazarus Group laundering through Huione Guarantee; Tether blacklists a Huione-linked wallet holding 29.6 million USDT that had received ~$14 million in hack proceeds.
- **February 4, 2025:** The NPA, FBI, and DC3 [jointly attribute](https://www.npa.go.jp/bureau/cyber/pdf/20250204_tt.pdf) the theft to North Korean TraderTraitor actors, detailing the social engineering scheme used to obtain initial access, and issue alerts on mitigation measures.

## Security Failure Causes

**Private key compromise via social engineering:** The [joint NPA/FBI/DC3 investigation](https://www.npa.go.jp/bureau/cyber/pdf/20250204_tt.pdf) concluded that North Korean actors obtained unauthorized access to the wallet's private key through a targeted social engineering scheme against an employee, rather than exploiting a vulnerability in the exchange's core systems. DMM Bitcoin's own statement emphasized the leak originated from [its wallet rather than a defect in the exchange platform](https://bitcoin.dmm.com/news/20240531_01).

**Hot wallet concentration risk:** The attacker was able to drain 4,502.9 BTC — the majority of the exchange's liquid holdings — in a single outflow, indicating that a compromise of one key set gave access to a large share of custodied funds.

**Laundering infrastructure gaps:** Post-theft tracing showed the stolen BTC was [rapidly moved through mixers and cross-chain bridges (THORChain, Threshold, Avalanche Bridge)](https://coinedition.com/zachxbt-uncovers-new-evidence-in-305-million-dmm-bitcoin-hack-investigation/) and converted to other assets, with over $35 million passing through Huione Guarantee. Intervention (such as the Tether blacklist of a recipient wallet) occurred only after the funds had already been dispersed, limiting recovery options.

**Mitigation context:** Following the incident, the joint agencies' alert emphasized that North Korean social engineering campaigns against cryptocurrency companies were ongoing and recommended verification of communications, restriction of privileged access, and monitoring for suspicious contact targeting employees with wallet custody responsibilities.
