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
- The swap rate reflects the market's expectation of the future path of the floating rate, averaged over the term of the swap. This rate should theoretically align with the equivalent term spot rate, which is the yield on a zero-coupon bond maturing at the same time as the swap's maturity.


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

# Swaps and Duration Management

## 1. Why Are Swaps Used Frequently?

- **Swaps allow institutions to manage interest rate exposure efficiently** without buying or selling bonds.
- They can **replicate a combination of Treasury bonds and Floating-Rate Notes (FRNs)**:
  - **Treasury Bonds**: Have long duration (e.g., 30-year maturity → duration ~15-20 years).
  - **FRNs**: Have near **zero duration**, resetting periodically to market rates.
- **Swaps provide flexibility**:
  - Adjust portfolio duration without changing bond holdings.
  - Hedge against interest rate movements.

---

## 2. How Swaps Are Used to Change Duration

- **Interest Rate Swaps** modify duration by exchanging fixed and floating cash flows.
- **Duration of a Swap**:
  - A **fixed-rate payer swap** **increases duration** because the party is exposed to fixed payments, making them sensitive to interest rate changes.
  - A **floating-rate payer swap** **decreases duration** because the floating payments adjust with market rates, reducing sensitivity.

### **Using Swaps to Adjust Portfolio Duration**
- **Increase Duration**: Enter into a **pay floating, receive fixed** swap.
  - Example: A company holding floating-rate liabilities (low duration) can **increase duration** by swapping them into fixed payments.
- **Decrease Duration**: Enter into a **pay fixed, receive floating** swap.
  - Example: A bond fund with long-duration assets can **reduce duration** by swapping fixed-rate cash flows for floating ones.

---

## 3. Example: Reducing Duration with a Swap

**Scenario**:  
- Suppose we hold **Treasury bonds with 30-year maturity**.
  - Duration ≈ **15-20 years** (due to coupon payments).
- We want to **reduce duration to near zero**.

**Solution: Enter a 30-Year Swap**
1. **Pay Fixed Rate** → Duration ≈ **-20 years**.
2. **Receive Floating Rate** → Duration ≈ **0**.

- The **fixed-rate exposures cancel out**.
- The remaining exposure is to **floating-rate payments** (low duration).
- **Result**: The portfolio duration is reduced to near zero.

---

## 4. Frequency of Payments Assumption

- **Swaps typically assume equal frequency of fixed and floating payments** to simplify valuation.
- In practice, conventions vary:
  - **Fixed Leg**: Often **semi-annual payments** in the U.S. (like fixed-rate Treasury bonds).
  - **Floating Leg**: Typically **quarterly payments** (e.g., based on SOFR or LIBOR before its phase-out).

### **When to Pay Fixed vs. Floating**
- **Pay Fixed, Receive Floating**:
  - Used when expecting **rates to rise** (lock in lower fixed rates).
  - Increases duration (acts like holding a fixed-rate bond).
- **Pay Floating, Receive Fixed**:
  - Used when expecting **rates to fall** (benefit from declining floating payments).
  - Reduces duration (acts like holding a floating-rate bond).

---

## **Conclusion**
Swaps are widely used because they provide a **flexible and cost-effective way to adjust duration** without the need to buy or sell bonds. By structuring swaps appropriately, institutions can hedge interest rate risk, optimize portfolio exposure, and match liabilities to assets efficiently.


# Swap Pricing Formulas

## 1. Understanding the Swap Components

### **Swap Structure**
The swap consists of two legs:
- **Floating-Rate Leg** (modeled as a Floating Rate Note, FRN)
- **Fixed-Rate Leg** (modeled as a fixed coupon bond)

The swap value at any time $t$ is given by:

$$
value_{swap}(t,T;swaprate) = P_{\text{float}}(t,T;0) - P_{fixed}(t,T;cpn_{swap})
$$

where:
- $P_{\text{float}}$: Price of the floating-rate bond.
- $P_{\text{fixed}}$: Price of the fixed-rate bond.
- $ cpn_{swap} $ : Fixed coupon rate (the swap rate swaprate) .

### **Key Assumptions**
- The swap has **equal frequency of fixed and floating payments**.
- The **floating bond price is 100** at each reset date $T_i$.
- The **discount factor $Z(0,T_i)$** represents the present value of $1 received at time $T_i$, using the risk-free curve.

---

## 2. Valuing the Swap at $t = 0$

Since the swap is constructed as a **long floating-rate bond** and **short fixed-rate bond**, its value is:

$$
value_{swap}(0,T;swaprate) = 100 - 100 \left[ \sum_{i=1}^{M} Z(0,T_i) \frac{cpn_{swap}}{freq} + Z(0,T) \right]
$$

### **Breaking Down the Formula**
#### **Floating Leg (First Term: $100$)**
- The floating bond **resets to par** at each payment date.
- Since we assume **no spreads or market frictions**, its value at reset is always **par (100)**.

#### **Fixed Leg (Second Term)**
- The fixed bond pays periodic coupons $ \frac{cpn_{swap}}{freq} $, discounted by $ Z(0,T_i) $.
- The principal 100 is also discounted at maturity $ T $, giving the term $ Z(0,T) $.

#### **Final Expression**
Factor out 100 from both terms:

$$
value_{swap}(0,T;swaprate) = 100 \left[1 - Z(0,T) - \frac{cpn_{swap}}{freq} \sum_{i=1}^{M} Z(0,T_i) \right]
$$

---

## 3. Solving for the Swap Rate $ swaprate $

At swap initiation ($ t=0 $), the swap is priced such that its value is **0**:

$$
value_{swap}(0,T;swaprate) = 0
$$

Setting the above expression to zero:

$$
1 - Z(0,T) - \frac{cpn_{swap}}{freq} \sum_{i=1}^{M} Z(0,T_i) = 0
$$

Solving for $ cpn_{swap} $ (the swap rate):

$$
swaprate(0,T;freq) = freq \cdot \frac{1-Z(0,T)}{\sum_{i=1}^{M} Z(0,T_i)}
$$

---

## 4. Interpretation of the Swap Rate Formula

- $ swaprate $ is the **fair fixed rate** that equates the present value of fixed and floating payments.
- The numerator $ (1 - Z(0,T)) $ represents the **discounted value of the notional amount at maturity**.
- The denominator $ sum_{i=1}^{M} Z(0,T_i) $ represents the **present value of all fixed payments**.

### **Intuition**
- The swap rate is a **weighted average** of implied forward rates over the swap's lifetime.
- The formula shows that the swap rate depends on:
  - The **frequency of payments** ($ freq $).
  - The **shape of the yield curve** (via $ Z(0,T_i) $).
  - The **total maturity** $ T $.

---

## 5. Key Takeaways
- **At initiation ($ t=0 $), the swap value is set to 0** by choosing a fixed rate that balances fixed and floating cash flows.
- **The swap rate ($ swaprate $) represents the fair fixed rate** at which the present values of both legs match.
- **Swaps effectively transform cash flows** between fixed and floating, allowing institutions to hedge interest rate risk.
