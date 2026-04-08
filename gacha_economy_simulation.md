# Mobile Idle RPG Gacha Economy Simulation ("Skull Up"-inspired)

## 1) Assumptions Used in the Model

To keep the simulation internally consistent, I use the following baseline assumptions:

- **Pull costs**
  - Standard banner pull (Skelly-focused): **100 Keys**
  - Featured Fiend banner pull (SSS+): **200 Keys**
  - Weapon banner pull (Divine Weapons): **250 Keys**
- **Drop rates and pity**
  - SSS+ Fiend base rate on featured: **0.8%** per pull
  - Divine Weapon base rate on weapon: **0.6%** per pull
  - Fiend hard pity: **120 pulls**
  - Weapon hard pity: **100 pulls**
- **Dupes / upgrade gates**
  - Fiend full competitive state: base copy + **5 duplicate copies** (6 total)
  - Divine Weapon full state: base copy + **3 duplicate copies** (4 total)
- **Key store pricing**
  - Small pack: **1,000 Keys = $9.99**
  - Mid pack: **6,000 Keys = $49.99**
  - Whale pack: **14,000 Keys = $99.99**
  - Effective best value used for high-spend estimates: ~$0.0071 per Key
- **Daily free key income**
  - F2P: **180 Keys/day** (events + missions + passives)
  - Mid spender: **250 Keys/day** (includes light VIP/battle pass)
  - Whale: **320 Keys/day** (max efficiency + paid accelerants)

> Notes:
> - Expected pulls without pity are approximated with geometric expectation: E[pulls] ~ 1/p.
> - With hard pity, average is pulled toward pity; for this genre, practical average often lands around 60-85% of pity when rates are low.

---

## 2) Structured System Breakdown

### A. Core Progression Roles

1. **Skellys**
   - High acquisition frequency builds early engagement.
   - Provides immediate growth feedback (collection % and team depth).
   - Serves as a soft tutorial for long-term gacha behavior.

2. **SSS+ Fiends**
   - Main aspiration tier and progression wall-breakers.
   - Power jumps are intentionally noticeable (DPS, survivability, passive multipliers).
   - Acts as the first strong monetization trigger when free progress slows.

3. **Divine Weapons**
   - Endgame differentiator and optimization sink.
   - Converts one-time acquisition into long-term spend via refinement/duplication.
   - Defines meta viability and guild/PvP competitiveness.

### B. Banner Ladder (Price Escalation)

- **Standard banner (Skelly)**: low cost, broad utility, low frustration.
- **Featured Fiend banner**: higher cost, lower rates, event-timed urgency.
- **Weapon banner**: premium cost, lowest rates, highest prestige pressure.

This creates a monetization staircase where perceived necessity increases with player investment.

---

## 3) Funnel Simulation (Behavioral Loop)

## Stage 1: Early Gratification
- Player receives free Keys.
- High Skelly hit frequency creates momentum and trust in progress.

## Stage 2: Friction Point
- Campaign/stat scaling outpaces Skelly growth.
- UI surfaces SSS+ Fiend banners with countdown timers and performance comparisons.

## Stage 3: Key Deficit Conversion
- Player cannot sustain required pulls via free income before banner expiry.
- Store offers context-sensitive key packs ("just enough for next 10-pull").

## Stage 4: Post-Purchase Outcomes
- **Success path**: Fiend obtained -> strong power spike -> player now sees weapon dependency.
- **Failure path**: near-miss outcomes (off-feature high rarity / progress meter close to pity) -> increased sunk-cost spending.

## Stage 5: Endgame Optimization Loop
- Build completion requires: Fiend + weapon + duplicates.
- New banner cycle introduces stronger alternatives (power creep), restarting chase pressure.

---

## 4) Cost Model: Unit-Level Acquisition

## A. Expected pulls per target

Using assumptions above:

- **SSS+ Fiend**
  - Best case: **1-10 pulls** (lucky spike)
  - Average case: **~90 pulls** (near pity behavior)
  - Worst case: **120 pulls** (hard pity)

- **Divine Weapon**
  - Best case: **1-10 pulls**
  - Average case: **~75 pulls**
  - Worst case: **100 pulls** (hard pity)

## B. Pulls -> Keys -> USD

### SSS+ Fiend (featured, 200 Keys/pull)
- Best case (10 pulls): 2,000 Keys
  - ~$14.3 (whale efficiency) to ~$20.0 (small-pack equivalent)
- Average (90 pulls): 18,000 Keys
  - ~$128.6 to ~$180.0
- Worst (120 pulls): 24,000 Keys
  - ~$171.4 to ~$240.0

### Divine Weapon (weapon, 250 Keys/pull)
- Best case (10 pulls): 2,500 Keys
  - ~$17.9 to ~$25.0
- Average (75 pulls): 18,750 Keys
  - ~$133.9 to ~$187.5
- Worst (100 pulls): 25,000 Keys
  - ~$178.6 to ~$250.0

---

## 5) Full Endgame Build Cost (Fiend + Weapon + Upgrades)

Target build requirement:
- Fiend copies needed: **6 total**
- Weapon copies needed: **4 total**

## A. Average-path estimate

- Fiend: 6 * 90 pulls = 540 pulls
  - 540 * 200 = 108,000 Keys
- Weapon: 4 * 75 pulls = 300 pulls
  - 300 * 250 = 75,000 Keys
- **Total average build** = **183,000 Keys**
  - USD equivalent: **~$1,307 (best pack efficiency)** to **~$1,830 (small-pack equivalent)**

## B. Worst-path estimate (full pity each copy)

- Fiend: 6 * 120 pulls = 720 pulls = 144,000 Keys
- Weapon: 4 * 100 pulls = 400 pulls = 100,000 Keys
- **Total worst build** = **244,000 Keys**
  - USD equivalent: **~$1,743 to ~$2,440**

## C. Best-path estimate (exceptionally lucky)

- Assume 10 pulls per copy average in a lucky streak:
- Fiend: 6 * 10 * 200 = 12,000 Keys
- Weapon: 4 * 10 * 250 = 10,000 Keys
- **Total best build** = **22,000 Keys**
  - USD equivalent: **~$157 to ~$220**

This spread (22k -> 244k Keys) is the core monetization variance engine.

---

## 6) Segment Simulation (30-Day Cycle)

## A. Free-to-Play

- Monthly free Keys: 180 * 30 = **5,400 Keys**
- Purchasing behavior: none.
- Pull strategy: stockpile for featured only; often skip weapon banners.
- Expected result in one banner cycle:
  - Insufficient for hard pity on Fiend (needs 24,000 Keys worst case).
  - May reach partial pity progress; completion depends on event bonuses.
- Retention risk:
  - High frustration if repeated near-miss cycles occur without completion.

## B. Mid Spender

- Free + paid flow target: ~**12,000-28,000 Keys/month**
- Typical spend: **$30-$120/month** depending on event urgency.
- Pull behavior:
  - Prioritizes one SSS+ Fiend; weapon only if early Fiend success.
- Expected state after 1-2 months:
  - 1 featured Fiend likely secured; weapon inconsistent unless lucky.
- Monetization profile:
  - Strongly sensitive to pity distance and banner timer pressure.

## C. Whales

- Monthly key access: **80,000+ Keys** via high-tier bundles.
- Typical spend: **$700-$2,000+ per month** during relevant metas.
- Pull behavior:
  - Completes Fiend + weapon + duplicate breakpoints quickly.
  - Continues spending for meta insurance (futureproofing roster).
- Monetization profile:
  - Revenue concentration very high; low sensitivity to per-pull price, high sensitivity to prestige and rank outcomes.

---

## 7) Monetization Efficiency vs Retention Risk

## High-efficiency levers

1. **RNG variance**
   - Monetizes unlucky streaks (extra purchases to reach certainty).
2. **Duplicate breakpoints**
   - Converts ownership into progression debt.
3. **FOMO banner windows**
   - Compresses decision time, raising conversion rates.
4. **Near-miss design**
   - Increases continuation probability after losses.

## Major risk factors

1. **Power creep acceleration**
   - If replacement cycle is too fast, prior spend feels invalidated.
2. **Economy inflation**
   - Rising key prices or reduced free income triggers trust erosion.
3. **RNG burnout**
   - Long fail streaks reduce session joy and increase churn intent.
4. **Hard paywalls in endgame**
   - Competitive modes become non-aspirational for non-whales, harming ecosystem health.

---

## 8) Ethical Considerations

- **Near-miss psychology** can meaningfully increase compulsive spending behavior.
- **Time-limited urgency** may pressure vulnerable users into non-deliberate purchases.
- **Opaque expected costs** (without transparent pity and rate disclosures) creates asymmetry.
- **Recommended mitigations**:
  - Display clear expected value ranges in-game.
  - Hard monthly spend controls and optional self-limits.
  - Duplicate alternatives (shards, long-term crafting).
  - Cadenced power creep with longer viability windows.

---

## 9) Design Recommendations (Actionable)

1. Keep Fiend pity visible and carry-over between banners.
2. Add deterministic long-tail paths for Divine Weapons (craft fragments).
3. Reduce duplicate requirement burden (e.g., 5 -> 3 meaningful breakpoints).
4. Protect previous investments using upgrade transfer or partial refund systems.
5. Segment offers by intent:
   - F2P-friendly accumulation events,
   - Mid-spender milestone bundles,
   - Whale prestige cosmetics that do not further widen power gap.

Result: better long-term retention while preserving top-line gacha monetization.
