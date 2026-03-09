# VASPcode Specification v0.1

**Status:** Working Draft  
**Maintained by:** [VASPdirectory](https://vaspdirectory.com)  
**Repository:** [github.com/vaspdirectory/vaspcode](https://github.com/vaspdirectory/vaspcode)  
**Last updated:** 2026-03-09

## What is VASPcode?

VASPcode is a human-readable identifier for licensed and registered Virtual Asset Service Providers (VASPs).

Each VASPcode uniquely identifies one legal entity operating under a specific regulatory licence or registration. VASPdirectory uses VASPcode as the primary key across its global VASP registry.

## Format

A VASPcode has three parts, separated by hyphens:

{CC}-{BRAND}-{ROLE}

**Regex:** `^[A-Z]{2}-[A-Z0-9]{2,10}-[A-Z]{2}$`

**Maximum length:** 16 characters (including hyphens)

| Part | Name | Rules | Example |
|------|------|-------|---------|
| CC | Country Code | ISO 3166-1 alpha-2 code of the entity's country of incorporation | HK, SG, US |
| BRAND | Brand Identifier | 2–10 uppercase alphanumeric characters (A–Z, 0–9). The recognisable trading or brand name of the entity. | BINANCE, HASHKEY, COINBASE |
| ROLE | Activity Type | 2 uppercase letters from the controlled vocabulary below | EX, CU, PA |

### Examples

| VASPcode | Entity | Explanation |
|----------|--------|-------------|
| GB-BITSTAMP-EX | Bitstamp Limited | UK-incorporated, Bitstamp brand, exchange |
| US-BINANCEUS-EX | BAM Trading Services Inc. | US-incorporated, Binance.US brand, exchange |
| IE-COINBASE-CU | Coinbase Custody International Limited | Ireland-incorporated, Coinbase brand, custody |
| MT-CRYPTOCOM-EX | Foris DAX MT Limited | Malta-incorporated, Crypto.com brand, exchange |
| HK-HASHKEY-EX | Hash Blockchain Limited | Hong Kong-incorporated, HashKey brand, exchange |
| JP-BITFLYER-EX | bitFlyer, Inc. | Japan-incorporated, bitFlyer brand, exchange |

## Country Code (CC)

The country code is the ISO 3166-1 alpha-2 code of the **country of incorporation** of the legal entity — not the country of licence.

A single entity may hold licences in multiple jurisdictions. The country of incorporation is a permanent, objective fact about the entity that does not change when it gains or loses licences. The likelihood of a licensed entity redomiciling is low, so this keeps VASPcodes relatively stable.

| Scenario | CC used |
|----------|---------|
| Entity incorporated in Ireland, licensed by AMF France via passporting | IE |
| Entity incorporated in BVI, registered in Singapore | VG |
| Entity incorporated in Malta, MiCA-passported across the EU | MT |
| Entity incorporated in Hong Kong, licensed in Hong Kong | HK |

### Special cases

- **Free zones (ADGM, DIFC, AIFC):** Use the country code of the sovereign state. ADGM and DIFC entities use AE; AIFC entities use KZ.
- **Multiple entities, same brand, same country:** Differentiate using the ROLE suffix (e.g. AU-CRYPTOCOM-EX and AU-CRYPTOCOM-PA). If both entities share the same role, append a short suffix to BRAND — either descriptive or numeric, at VASPdirectory's discretion (e.g. HK-HASHKEYCL-EX for a clearing entity, or HK-HASHKEY2-EX). The base BRAND plus any suffix must together stay within the 2–10 character BRAND limit.

## Brand Identifier (BRAND)

The BRAND block identifies the entity's operating brand or group name.

| Rule | Detail |
|------|--------|
| Length | 2–10 characters |
| Charset | A–Z and 0–9 only (no spaces, dots, or special characters) |
| Case | Always uppercase |
| Uniqueness | BRAND is not globally unique — the full VASPcode (CC-BRAND-ROLE) is the unique identifier |
| Assignment | Based on the primary trading name or consumer-facing brand |

### Naming conventions

| Brand | BRAND code | Notes |
|-------|-----------|-------|
| Binance | BINANCE | |
| Binance.US | BINANCEUS | Separate operating entity from Binance global |
| Binance Japan (K.K.) | BINANCEJP | Regional suffix for distinct local entity |
| Crypto.com | CRYPTOCOM | Dots removed |
| Kraken | KRAKEN | |
| Bybit | BYBIT | |
| Gate.io | GATEIO | Dots removed |
| OKX | OKX | Short names kept as-is |
| HashKey | HASHKEY | |

## Activity Type (ROLE)

The ROLE suffix describes the entity's **primary regulated activity**. It does not capture every service the entity provides.

### Controlled vocabulary

| Code | Activity | When to use |
|------|----------|-------------|
| EX | Exchange / Trading Platform | Any entity operating a trading venue for virtual assets — spot, derivatives, securities tokens, or multilateral trading |
| CU | Custody / Safekeeping | Entities primarily holding virtual assets on behalf of clients |
| PA | Payment / Money Services | Entities primarily licensed for payment services, money transmission, e-money issuance, or remittance involving virtual assets |
| BR | Broker-Dealer | Entities primarily executing or arranging trades on behalf of clients |
| AD | Advisory | Entities licensed to provide investment or asset management advice relating to virtual assets |
| TR | Trust Company | Entities licensed as trust companies whose primary charter is fiduciary services |
| IN | Investment / Issuance | Entities primarily engaged in fund management, collective investment, token issuance, or asset management |

### Choosing a ROLE when an entity has multiple activities

If an entity holds multiple licence types, apply this priority:

1. **EX** — if the entity operates any trading platform
2. **CU** — if primarily a custodian
3. **BR** — if primarily a broker-dealer
4. **PA** — if primarily a payment/money services business
5. **TR** — if primarily a trust company
6. **AD** — if primarily an advisory firm
7. **IN** — if primarily a fund/investment manager

VASPcode identifies the entity, not the licence.

## VASPcode Lifecycle

### Assignment

A VASPcode is assigned when a legal entity first appears in the VASPdirectory registry.

### Permanence

Once assigned, a VASPcode does not normally change — even if the entity's licence is suspended, revoked, or expires; the entity ceases operations; or the brand changes ownership.

In exceptional cases (for example, mergers or major legal name changes), VASPdirectory may update the VASPcode. When a VASPcode is updated, the prior code is marked Deprecated and linked to the successor code.

### Status

| Status | Meaning |
|--------|---------|
| Active | Entity holds at least one active licence or registration |
| Suspended | Entity's licence has been suspended by a regulator |
| Deprecated | Entity no longer operates as a VASP. Deprecated codes are never reassigned. |

## Governance

VASPdirectory maintains this specification and assigns all VASPcodes during the v0.x period. The controlled vocabulary (ROLE codes) may be extended in future versions. This specification follows semantic versioning; breaking changes to the format will increment the major version number.

Feedback and suggestions are welcome via [GitHub Issues](https://github.com/vaspdirectory/vaspcode/issues).

## Licence

This specification is published under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

[![CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)
