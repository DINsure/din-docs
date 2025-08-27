# DIN: Decentralized Insurance

<figure style="text-align:center;">
  <img src="https://cdn.dorahacks.io/static/files/198e995730a326b4c9ca9c14f83bc619.jpg" alt="DIN LOGO" style="width:50%; max-width:300px; height:auto;" />
</figure>

DIN service is available on Kaia Testnet(Kairos). Visit https://dinsure.app

**Official Repo**
- [Docs Repo](https://github.com/DINsure/din-docs)
- [Contract Code Repo](https://github.com/DINsure/din-contract)
- [Web Interface Repo](https://github.com/DINsure)

**DIN Whitepaper**
- [Whitepaper (English)](whitepaper/DIN-Decentralized-Insurance-Whitepaper-ENG.pdf) | [Google Drive](https://drive.google.com/file/d/1uAXCVN4jBQTpJyOUgZlQjEG3F10E53En/view?usp=sharing)
- [Whitepaper (Korean)](whitepaper/DIN-Decentralized-Insurance-Whitepaper-KOR.pdf) | [Google Drive](https://drive.google.com/file/d/1MdmnbSWYTkV0-JbC3BdzZuJmnQTB9XQ9/view?usp=sharing)

**Pitch Decks**
- [Pitch Deck (English)](pitch-deck/DIN-Pitch-Deck-ENG.pdf) | [Google Drive](https://drive.google.com/file/d/1uAXCVN4jBQTpJyOUgZlQjEG3F10E53En/view?usp=sharing)
- [Pitch Deck (Korean)](pitch-deck/DIN-Pitch-Deck-KOR.pdf) | [Google Drive](https://drive.google.com/file/d/1Cdk0pxG2Xlc77N3w_Id4tWqsi9blECLq/view?usp=sharing)


## 1. Problem & Solution

Web3 users remain exposed to high volatility, smart contract risks, and uncertainties arising from external events, and practical protection is lacking compared with traditional finance. The only widely available mitigation, managing derivatives, requires specialized expertise and continuous oversight, making it a difficult option for most users to adopt.

DIN proposes an on-chain parametric, condition-based insurance solution to fill this gap. By combining automated settlement with multi-source oracle routing, the protocol removes complex claims processing, and offers the advantages of clear payout rules and on-chain enforceability.

Web3 사용자들은 높은 변동성, 스마트 컨트랙트 리스크, 외부 이벤트로 인한 불확실성에 계속 노출되어 있어 전통적 금융 대비 실용적인 보호 수단이 부족합니다. 유일한 보호 수단인 파생상품 운영은 전문성과 지속적인 관리가 필요해 쉽게 채택하기 어려운 선택지입니다.

DIN은 이러한 공백을 메우기 위해 온체인 파라메트릭(조건 기반) 보험을 제안합니다. USDT를 사용한 보험료 및 보상 자동 정산 기능과, 다중 소스 오라클 라우터를 결합한 DeFi 보험 솔루션을 통해 복잡한 보험 심사 과정을 제거하고, 명확한 지급 규칙과 온체인 실행이라는 이점을 제공합니다.

## 2. DIN Introduction

DIN is a decentralized insurance infrastructure built on the Kaia blockchain that connects policy buyers and underwriters through a two-sided, tranche-based marketplace.

Policy buyers simply choose desired conditions from DIN’s insurance catalog and pay premiums in USDT to subscribe, upon which they receive a KIP17 NFT insurance certificate. Once coverage is active and the maturity is reached, payouts are executed automatically according to the agreed conditions, providing a practical and reliable hedging tool within the DeFi environment.

Additionally, DIN operates a two-sided marketplace where participants can underwrite coverage by depositing capital and earn premiums, creating a new investment opportunity for DeFi investors to capture both insurance premium income and staking yields.

DIN은 Kaia 블록체인 위에서 운영되는 탈중앙화 보험 인프라로 작동하며, 구매자와 예치자(판매자, 언더라이터)를 연결하는 양면 시장을 제공합니다.

보험 구매자는 DIN의 보험 카탈로그에서 원하는 조건을 선택하고 USDT로 보험료(프리미엄)을 지불하면 바로 보험에 가입할 수 있으며, KIP17 NFT 보험 증서가 제공됩니다. 보험이 체결되어 기간이 도래하면 조건에 따라 자동으로 보험료가 지급되며, DeFi 환경에서 실용적이고 신뢰할 수 있는 위험 헤지 수단을 제공합니다.

이에 더해, DIN은 보험에 USDT를 예치(판매, 언더라이팅)하고 프리미엄을 얻을 수 있는 양면시장을 제공합니다. DeFi 투자자들에게는 보험 프리미엄 뿐만 아니라, 보험 기간 중에 리스테이킹 운영을 통한 추가 스테이킹 이자를 함께 챙길 수 있는 새로운 투자 기회를 제공합니다.

## 3. How it Works

Users select a product from a public catalog, then pay premiums in USDT to subscribe or deposit USDT into a tranche to act as an underwriter, and any unmatched funds are automatically refunded at sale close. Matched positions are recorded on-chain and represented by `KIP-17` insurance certificates, while deterministic matching and USDT-denominated accounting provide transparent, auditable state for frontends and external indexers.

At maturity the `SettlementEngine` calls the `OracleRouter`, which selects `Orakl` for standard price feeds or `DINO` for bespoke events, validates freshness and divergence, and finalizes observations via `assertion, liveness, dispute and settle` phases when required. Re-stake activity is restricted to whitelist-approved pools, the `YieldRouter` must preserve sufficient liquidity coverage, and settlements are protected by idempotency guards, timelocks and emergency pause controls, with all actions logged on-chain for independent verification.

For detailed technical structure and contract source codes, visit our Git Repo: https://github.com/DINsure/din-contract

사용자는 공개 카탈로그에서 상품을 선택한 뒤 USDT로 보험료를 지불해 가입하거나 트랜치에 USDT를 예치해 보험 예치자(판매자, 언더라이터)로 참여하며, 체결되지 않은 자금은 판매 종료 시 자동으로 환급됩니다. 체결된 포지션은 온체인에 기록되어 `KIP-17` 보험 증서로 제공됩니다. 확정적인 매칭 시스템과 USDT 기준 회계는 프론트엔드와 외부 인덱서가 검증 가능한 투명한 상태를 제공합니다.

만기에는 `SettlementEngine`이 `OracleRouter`를 호출해 표준 가격에는 `Orakl`을, 커스텀 이벤트에는 `DINO`를 선택하여 신선도와 괴리를 검증하고, DINO 사용 시 `Assertion, Liveness, Dispute, Settle` 절차로 최종 관측값을 확정합니다. 재예치는 화이트리스트 승인 풀로 제한되며 `YieldRouter`는 충분한 유동성 커버리지를 유지해야 하고, 정산은 중복 방지 보호, 타임록, 비상 정지 등으로 안전하게 보호되며 모든 행위는 독립 검증을 위해 온체인에 기록됩니다.

자세한 구조 설계와 컨트랙트 코드는 Git Repo에서 확인할 수 있습니다. https://github.com/DINsure/din-contract


## 4. DIN Ecosystem

DIN’s ecosystem comprises three core primitives that together sustain protocol integrity and growth: the **DIN Token**, **DINO** the optimistic oracle, and **DINGO** the governance framework.

**DIN Token** functions as the utility instrument for governance staking, oracle bonds, and targeted incentives, it is designed with transparent supply and vesting rules and is used sparingly for purposes that enhance market depth or bootstrap new categories, while accounting and payouts remain denominated in USDT to protect claim capacity from token volatility.

**DINO(DIN Oracle)** is an optimistic oracle tailored for bespoke conditions and special-event adjudication, it operates via an assertion, liveness, dispute, settle lifecycle where DIN-backed bonds secure economic incentives for honest reporting and allow efficient resolution of edge cases like weather, political events that standard feeds cannot cover. DINO parameters such as bond size, liveness windows, and dispute economics are tiered by tranche risk and are published on-chain to ensure predictable governance and operational safety.

**DINGO(DIN Governance)** is the governance framework that will progressively assume control over protocol parameters, it begins with multisig and timelock safeguards managed by the team, then transitions to token-enabled proposal and voting processes that govern fees, oracle routing, re-stake whitelists, and tranche limits, while role-based staking and reputation requirements help maintain participation quality. DINGO’s staged decentralization model ensures that operational safety and community oversight advance together.

**DIN 토큰**, **DINO**, **DINGO** 3개의 핵심 요소로 구성된 DIN 생태계는 전반적인 보험 프로토콜의 안정성과 확장성을 뒷받침합니다.

**DIN 토큰** 은 거버넌스 스테이킹, 오라클 보증금, 목표형 인센티브 수단으로 설계되어 투명한 공급과 베스팅 정책 하에서 제한적으로 사용됩니다, 핵심 회계는 여전히 USDT로 유지되어 토큰 가격 변동이 보험 지급 능력에 영향을 주지 않습니다.

**DINO(DIN Oracle)** 는 맞춤형 조건과 특수 이벤트에 대한 판정을 위해 설계된 낙관적 오라클로, `Assertion, Liveness, Dispute, Settle`의 절차를 통해 동작합니다. 주장자와 이의제기자는 DIN 토큰으로 보증금을 예치하며, 이 구조는 기후 보험, 정치 이벤트 보험처럼 표준 피드로 처리하기 어려운 사례를 경제적 인센티브와 공개 규칙으로 효율적으로 해결할 수 있게 합니다. DINO의 파라미터는 트랜치 위험도에 따라 계층화되어 온체인에 공개됩니다.

**DINGO(DIN Governance)** 는 프로토콜 파라미터의 점진적 이양을 위한 거버넌스 프레임워크로, 초기에는 팀의 멀티시그와 타임록으로 안정성을 확보하고 이후에는 거버넌스로 권한이 점차 이전되며 토큰 기반 제안과 투표로 수수료, 오라클 라우팅, 재예치 화이트리스트, 트랜치 한도 등을 관리하게 됩니다. 거버넌스 참여를 위해서는 DIN 스테이킹과 평판 요건을 도입하여 참여자들의 신뢰를 보장하며, 단계적 탈중앙화는 운영 안전성과 커뮤니티 감시가 함께 이루어지도록 설계되었습니다.


## 5. Operation & Roadmap

![roadmap_mini.png](https://cdn.dorahacks.io/static/files/198e99b577cf9caa769157948c8b5e86.png)

Initial operations are team-led to build operational stability and trust, followed by staged onboarding of whitelist underwriters and progressive transfer of governance to the community via the DINGO framework. The roadmap moves from testnet and MVP validation to mainnet expansion with targeted DINO-driven products and, ultimately, an open marketplace governed by token-based participation and performance-aligned incentives.

**Phase 1 — Testnet & MVP:** Focuses on integrating and validating core infrastructure (`Product Catalog`, `TranchePool`, `SettlementEngine`, `OracleRouter`, `YieldRouter`) on testnet, confirming deterministic matching and Auto-Refund behavior, and establishing baseline security through an external audit and bug bounty. Add support on LINE Mini DApp for ecosystem expansion

**Phase 2 — Mainnet & Pilots:** Phase 2 expands to mainnet with targeted DINO-driven special-event products, gradual enlargement of whitelist re-stake targets and risk limits, and enterprise/DAO pilot programs, while preserving transparency via additional audits, public operational reports, and narrowly scoped DIN incentives with vesting.

**Phase 3 — Progressive Opening & Governance:** Phase 3 onboards professional underwriters and product designers, stages delegation of selected parameters to DINGO governance with role-based staking and reputation requirements, and transitions toward an open marketplace with cross-chain integrations and enterprise APIs.

DIN aims to evolve into the **Kaia ecosystem’s core DeFi insurance infrastructure**, founded on trust, transparency, and capital efficiency.

초기 운영은 팀 주도로 안정적 실행과 초기 사용자 및 파트너 신뢰 확보에 중점을 둡니다, 팀은 라운드 운영과 초기 상품 설계, 보수적 노출 한도 설정, 면밀한 모니터링과 리포팅을 직접 수행하며, 중요한 운영은 멀티시그와 타임록으로 보호됩니다. 손해율, 체결률, 유동성 커버리지, 금고 현금흐름과 같은 핵심 KPI를 상시 관찰하고, 단계별 체크리스트를 통해 라운드 규모나 상품 확장 여부를 결정합니다.

**1단계 — 테스트넷 및 MVP:** `Product Catalog`, `TranchePool`, `SettlementEngine`, `OracleRouter`, `YieldRouter` 등 핵심 인프라를 테스트넷에서 통합, 검증하고 보험 매칭과 Auto-Refund 등의 보험 지급을 확인하며, 외부 감사와 버그바운티로 초기 신뢰를 확보하는 데 집중합니다. 생태계 확장을 위한 LINE Mini DApp 지원도 추가합니다.

**2단계 — 메인넷 확장 및 파일럿:** 2단계는 메인넷으로 확장하여 DINO 기반 특수 이벤트 상품을 도입하고 화이트리스트 재예치 대상과 위험 한도를 점진적으로 확대하며, 엔터프라이즈·DAO 파일럿과 추가 감사 및 공개 운영 리포트와 제한적 DIN 인센티브(베스팅 포함)를 통해 수요와 투명성을 검증합니다.

**3단계 — 점진적 개방 및 거버넌스 전환:** 3단계는 전문 인수자와 상품 설계자를 온보딩하고 일부 운영 파라미터를 DINGO 거버넌스로 단계적으로 이양하며, 역할 기반 스테이킹과 평판 요건으로 참여 품질을 보장하면서 크로스체인 통합과 기업용 API를 갖춘 오픈 마켓플레이스로 전환합니다.

DIN은 궁극적으로 신뢰와 투명성, 자본 효율을 축으로 **Kaia 생태계의 핵심 DeFi 보험 인프라**로 성장할 것입니다.

## 6. Contact

For questions or contributions, reach us at: contact@dinsure.app

Project site: https://dinsure.app | Source: https://github.com/DINsure

## 7. License & Rights

All rights reserved. (C) 2025 DIN Team.
