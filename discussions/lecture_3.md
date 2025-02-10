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
- **Gross market Value**: Tons of swaps are held in offesetting positions, for instance taking an offestting swap to get out of a previous swap. Net wise, much smaller, one swap up, one swap down. 
- **Duration**: Duration of fixed (have duration). Floating rate note has near 0 duration, before duration. A lot of hedgind using Swaps is about making duration anyway one wants. 
- **Swap spread**: Treasury YTM less the Swap fixed rate usually positive due to credit risk of swap counterparty. If buy bond on a repo, and enter a swap to receive float, pay fixed, and buying treasuries is better than being long on swap, gonna earn the spread (annualised) or half the spread on semiannual basis, due to bigger coupon. 
- **Swap curve**: Current fixed rate on a particular day for all maturities.
- **Currency Swaps**: Exchange principal and interest in different currencies.
- **Parameters**:
  - **Maturity**
  - **Frequency of swaps**
  - **Notional amount**

### Swap Pricing Basics
- Example: A swap exchanging 5% fixed and floating rates on a $1 million notional.
- Market value of a swap:
  - Spread × Notional.
- Original swap rat 4.26 change to 4.08, you can reprice using 4.26 as coupon and YTM using new rate of 4.08. The fixed leg payments are locked at coupon = s₁ = 4.26%. Discount these cash flows using the new market rate s₂ = 4.08%
  - V_swap = N * [ 1 - Z(0,T) - (s₁/f) * Σ(i=1 to M) Z(0,T_i) ]
  - Since s₂ < s₁, this will result in a negative value for a fixed-rate payer (positive for fixed-rate receiver), as the fixed payments are locked in at a higher rate than current market rates.
- If YTM of treasury < Swap rate but coupon rate>Swap rate, make more sense to short treasury, because treasury is going to depreciate. 

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
Value_swap(t, T, swap rate) = P_float(t, T; 0) - P_tbond(t, T; coupon_swap)

- Frequency (f) and swap dates (T_i) omitted for simplicity.

### Swap Rate Determination
- Swap rate (s) is set such that the swap value is 0 at initiation (t=0):

s such that Value_swap(0, T, s) = 0

### Swap Pricing Formula
- For swaps with equal frequency of fixed and floating payments:
  - Payment frequency: f
  - Total payments: M = f * T
  - Payment dates: T_i, with T_M = T (maturity)

Value of the swap at \(t=0\):

Value_swap(0, T; s) = 100 [ 1 - Z(0, T) - (coupon_swap/f) * Σ(i=1 to M) Z(0, T_i) ]

#### Solving for the Swap Rate
s(0, T; f) = f * (1 - Z(0, T)) / Σ(i=1 to M) Z(0, T_i)

Where:
- Z(0, T): Discount factor for maturity T.

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