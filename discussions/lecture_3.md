# Notes on Bonds, Swaps, and Pricing

## Bonds Overview

### Yield to Maturity (YTM)
- YTM is like a price for bonds and can change over time.
- Coupons, however, remain constant for fixed-rate bonds.

### Floating Rate Bonds
- **Coupon Variation**: Coupons vary based on short-term interest rates.
- **Pricing**:
  - If the coupon matches the discount rate, the bond price remains constant at face value.
  - Example: Using backward induction with a one-period maturity.
- **Reset Mechanism**:
  - Price at reset is **100**.
  - In-between coupon periods, the price may vary.
  - Coupons are set based on current short-term interest rates (e.g., 3-month T-bill rate) and locked in for the period.
- **Duration Characteristics**:
  - Near maturity, the bond has a duration close to **0** because rates reset frequently.
  - After resetting, prices stabilize, reducing duration risk.
- **Comparison to 3-Month T-Bills**:
  - Floating rate bonds reset weekly but pay coupons quarterly.
  - They exhibit lower duration risk than 3-month T-bills, making them a safer option.
- **Ownership**:
  - Often held by money market funds as they act like a risk-free asset.

## Floating vs. Fixed Corporate Bonds
- **Fixed vs. Floating Preference**:
  - Rising interest rates favor floating-rate bonds.
- **Reset Frequency**:
  - Floating corporate bonds usually reset quarterly (e.g., September rate determines December's coupon).
- **Duration**:
  - Duration moves from **0.5** (right after resetting) to **0** at the end of the period.

---

## Swaps Overview

### Key Components of Swaps
- **Rate Swaps**: Exchange fixed and floating rates.
- **Currency Swaps**: Exchange principal and interest in different currencies.
- **Parameters**:
  - **Maturity**
  - **Frequency of swaps**
  - **Notional amount**

### Swap Pricing Basics
- Example: A swap exchanging 5% fixed and floating rates on a $1 million notional.
- Market value of a swap:
  - Spread × Notional.

### Floating Rate in Swaps
- Floating rate (e.g., SOFR) is locked in for a defined period (e.g., December 2024 rate for one period out).
- Gross market value of swaps is significant due to exchanges across multiple parties.

---

## Swap Valuation

### Replicating a Swap
- From the perspective of **paying-fixed, receiving-floating**, the swap is replicated by:
  - **+ Floating-rate bond**
  - **- Fixed-rate bond**

### Swap Value Formula
\[
\text{Value}_{\text{swap}}(t, T, \text{swap rate}) = P_{\text{float}}(t, T; 0) - P_{\text{tbond}}(t, T; \text{coupon}_{\text{swap}})
\]

- Frequency (\(\freq\)) and swap dates (\(T_i\)) omitted for simplicity.

### Swap Rate Determination
- Swap rate (\(\swaprate\)) is set such that the swap value is **0** at initiation (\(t=0\)):

\[
\swaprate \text{ such that } \text{Value}_{\text{swap}}(0, T, \swaprate) = 0
\]

### Swap Pricing Formula
- For swaps with equal frequency of fixed and floating payments:
  - Payment frequency: \(\freq\)
  - Total payments: \(M = \freq \cdot T\)
  - Payment dates: \(T_i\), with \(T_M = T\) (maturity).

Value of the swap at \(t=0\):

\[
\text{Value}_{\text{swap}}(0, T; \swaprate) = 100 \left[ 1 - Z(0, T) - \frac{\text{coupon}_{\text{swap}}}{\freq} \sum_{i=1}^M Z(0, T_i) \right]
\]

#### Solving for the Swap Rate
\[
\swaprate(0, T; \freq) = \freq \cdot \frac{1 - Z(0, T)}{\sum_{i=1}^M Z(0, T_i)}
\]

Where:
- \(Z(0, T)\): Discount factor for maturity \(T\).

---

## Swaps, Forwards, and Floaters

### Swaps as Bonds
- A swap can be replicated by holding:
  - **Paying-fixed**: 
    - Long floating-rate bond (FRN) with the same underlying variable rate.
    - Short fixed-rate bond.
- **Cashflows**:
  - Pay fixed rate via the short fixed-rate bond.
  - Receive floating rate via the long FRN.
- At maturity:
  - Offsetting face values result in no notional exchange.

### Swaps as Forwards
- A forward is equivalent to a single-date swap.
- A swap can be viewed as a portfolio of forward contracts.
- A forward rate agreement (FRA) is essentially a one-time swap.


## 1. Impact of Reset Frequency on Duration

- **Duration Definition**: Measures a bond's price sensitivity to interest rate changes.
- **Effect of Reset Frequency**:
  - **Weekly Resets**: 
    - Align more closely with market rates.
    - Reduce sensitivity to interest rate changes.
    - **Lower duration**, making it behave like a short-term risk-free asset.
  - **Quarterly Resets**:
    - Lag behind market rate adjustments.
    - Increase interest rate sensitivity.
    - **Higher duration**.

**Conclusion**: More frequent resets (e.g., weekly) **decrease duration**, making the bond safer from interest rate fluctuations.

---

## 2. Why Treasury Includes a Spread (\( \text{spread} \)) at Issuance

- Although FRNs trade at **par** on reset dates, they might not trade at par on **issuance dates**. A spread (\( \text{spread} \)) is added to ensure pricing at par on issuance.

### Reasons for Including the Spread:
1. **Market Conditions at Issuance**:
   - Floating rates might not fully reflect current market conditions (e.g., demand/supply imbalances or yield curve distortions).
   - A spread adjusts the coupon to ensure par pricing.

2. **Credit and Liquidity Premiums**:
   - Even risk-free Treasury FRNs may require a small premium to compete with other instruments or account for liquidity.

3. **Initial Price Adjustment**:
   - Without a spread, slight mismatches between the expected floating rate and actual coupon could cause the bond to price above or below par.
   - A spread ensures the present value of future cash flows equals par.

4. **Investor Demand**:
   - Investors may seek a slightly higher return for floating-rate risk, especially during periods of uncertainty.

**Conclusion**: The spread ensures FRNs price at **par on issuance** by correcting for deviations due to market dynamics, credit considerations, and investor expectations.

--- 