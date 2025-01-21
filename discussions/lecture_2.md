# Bond Pricing, Duration, and Factor Analysis

Below is a cleaned-up and logically consistent summary of various topics related to bond pricing, dirty vs. clean prices, credit risk, liquidity, duration, and factor analysis (including PCA). All content from the original discussion is included, with improved writing and organization.

---

## Dirty Price vs. Clean Price

- **Dirty Price:**  
  Reflects the **full present value** of the bond, including accrued interest. When discounting future cash flows to get the present value, you are effectively calculating the dirty price. This is often the price reported in many contexts.

- **Clean Price:**  
  Excludes accrued interest. It is simply the dirty price minus accrued interest. Clean prices are often quoted because they are **easier to compare** over time (they remove the “undesirable” effect of accrued coupons on the bond price).

> **Key Point:** If you are given a bond price, be sure you know whether it is the **clean** or **dirty** price. We will try to clarify this when providing data.

---

## Credit Risk

- When there is a risk of default (e.g., corporate bonds), **future cash flows are discounted at a higher rate** to compensate investors for taking on additional risk.
- Using corporate bonds instead of risk-free Treasuries means the **spot curve** will incorporate a **credit spread** (the extra yield demanded over the risk-free rate).

**Example:**  
A zero-coupon bond pays \$100 in one year.  

| Security            | Price (Present Value) | Cashflow at T=1 | Implied (T=1) Discount Factor |
|---------------------|-----------------------|-----------------|--------------------------------|
| **US T-Bill**       | \$99                  | \$100           | 0.99                           |
| **Corporate Bond**  | \$95                  | \$100           | 0.95                           |

- Investors must be compensated for **additional risk**, so the **present value** of the corporate bond is lower (and hence its **yield** is higher).
- The higher yield reflects the **credit spread** above the risk-free rate.

### Which Bond to Use for Constructing a Discount Factor Curve?

- To **price risk-free assets**, use discount factors implied by **risk-free securities** (e.g., U.S. Treasuries).
- To **price risky assets**, use discount factors implied by **comparable-risk** securities (i.e., those with a similar default probability and liquidity profile).

---

## Liquidity

- **Higher liquidity** is **preferred** because it leads to a **more reliable curve**. Illiquid bonds can introduce **noise** due to stale or inaccurate prices.
- For U.S. Treasuries:
  - **On-the-run Treasuries** (the most recently issued) are more liquid.
  - **Off-the-run Treasuries** (older issues) are generally less liquid.

> **Ideal Scenario:** Construct a “pure” spot curve from **risk-free, liquid assets**. Then, if you need to price illiquid or risky bonds, **adjust** that pure discount factor curve to account for additional illiquidity or credit risk.

---

## Level Factor (Most Important from PCA)

- From **Principal Component Analysis (PCA)** of yield curves, the **level factor** (a **parallel shift**) is typically the **most significant** factor.
- Understanding how your portfolio reacts to a **shift** in the yield (spot) curve is crucial.

> **Caution on Simple Regressions:**  
> Regressing portfolio returns on a single time series of yields can be problematic. The portfolio is **non-stationary** (it changes composition over time), and you risk **wasting statistical power**. In equities, this might be analogous to a company like “Tesla turning into Coca-Cola slowly,” reflecting a fundamentally different firm over time.

---

## Duration and Convexity: Price Approximation

A common approximation for the **percentage change in bond price** is:

\[
\frac{dP}{P} \approx -D \,\Delta r \;+\; \tfrac{1}{2}C \,(\Delta r)^2,
\]

where:
- \( D \) is the **duration** (first-order sensitivity).
- \( C \) is the **convexity** (second-order sensitivity).
- \( \Delta r \) is the **parallel shift** in interest rates (e.g., 0.01 for a 1% shift).

> **Note:**  
> - Duration (\(D\)) and convexity (\(C\)) are both **positive** for typical (option-free) Treasury bonds.  
> - PCA supports the idea that **level** (captured by \(D\)) and **curvature**/convexity (captured by \(C\)) are two important factors in fixed-income markets, but the approximation itself is **not derived from PCA**.

---

## Yield Curve vs. Spot Curve

- Often, “rates” refer to the **spot discount curve**.  
- The **yield curve** and the **spot curve** contain essentially the same underlying information.  
- Duration generally refers to changes in **spot rates**, which are **highly correlated** with yields.

---

## The Negative Sign on Duration

Duration is defined as:

\[
D = -\frac{1}{P} \frac{dP}{dr}.
\]

- The negative sign ensures \(D\) is **positive** for a typical bond (since \( \frac{dP}{dr} < 0 \) for Treasuries).
- In practice, we quote \(D\) as a positive number, acknowledging that bond prices move **inversely** to rates.

---

## Matching Compounding Conventions

- **Duration** can be defined under **various compounding conventions** (e.g., semiannual, annual, continuous).
- For coupon bonds paying semiannually, it is common to use **semiannual-compounded** yield/rates. 
- The idea remains the same: we **differentiate price w.r.t. rates** and scale by \(-1/P\).

> In most practical settings, **convexity** might be **ignored** for quick estimates, but is important for larger yield shocks.

---

## Duration as a Weighted Average of Time

For a coupon bond, **Macaulay Duration** can also be viewed as the **weighted average** of the times to each cash flow (coupon + principal), where the weights are the **present values** of those cash flows divided by the **total price** of the bond.

- Example: A 10-year Treasury with semiannual coupon payments has each coupon discounted to present. Those discounted amounts form the weights.
- Higher coupons lead to **lower duration** since **more cash** is received **earlier**, reducing the bond’s sensitivity to interest rate changes.

> **Derivative Definition**: Ultimately, the “weighted average time” formula is consistent with the derivative-based definition \(D = -\frac{1}{P}\frac{dP}{dr}\).

---

## Time Series Aspect of Duration

- **Duration changes over time**, similar to **option delta** changing as underlying conditions shift.
- To **hedge** duration risk, one typically rebalances positions regularly (just as in delta-hedging an option).

> **Dollar Duration**:  
> Sometimes used for hedging. Defined as \( \text{Duration} \times \text{Bond Price} \). It gives the **dollar change** in the bond price for a 1 percentage point change in rates.

---

## Beyond Parallel Shifts: Key Rate Durations

- If the yield curve **doesn’t shift in parallel**, you can look at changes in **a few key rates** (e.g., 1-year, 5-year, 10-year) and **mix** them to see the approximate impact on your bond’s price.
- The same core **derivative** logic applies; you just **partition** the rate curve into segments and measure partial durations (or key rate durations).

---

## Factor Duration and Regression Cautions

- One can decompose yield curve movements into **factors** (e.g., via PCA) and measure a portfolio’s **factor duration** (sensitivity to each factor).
- However, using **time-series regressions** on a portfolio of multiple securities can be tricky due to:
  1. **Non-stationarity** of the portfolio (it changes composition over time).
  2. The difficulty of maintaining a “constant maturity” bond or portfolio for regression purposes.

> Often, practitioners keep a **constant maturity** security (e.g., a perpetual 10-year future or swap) to measure exposure. For a **multi-bond** portfolio, factor analysis can be done, but the **statistical power** of such regressions might be lower or unstable.

---

## Final Note

In practice:
1. **Recognize** whether you are dealing with **clean** or **dirty** prices.
2. **Consider credit risk**: if you need a risk-free curve, use **Treasuries**; if you need a risky curve, use appropriate **corporate** or other risky securities.
3. **Prefer liquidity**: an **on-the-run** Treasury curve is often the benchmark in USD markets.
4. **Use duration and convexity** (and possibly key-rate durations or factor durations) to **understand and hedge** interest rate risk.
5. **Beware of non-stationarity** in portfolio analyses and be mindful of how you measure or hedge interest rate exposures over time.

