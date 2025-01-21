# Yield Factors and Yield-to-Maturity (YTM)

## Yield-to-Maturity (YTM)
YTM is a way to quote bond prices. It represents the annualized return on a bond, assuming:
- All coupons are reinvested at the same rate.
- The bond is held to maturity.

### YTM Usage
- Useful for comparing similar securities, such as U.S. Treasuries with the same maturity.
- Indicates the pricing of guaranteed future cash flows with negligible credit and counterparty risks (e.g., U.S. Treasuries).
- Helps price cashflows specific to a bond across various maturities but is tied to the specific bond it is derived from.

### Limitations of YTM
- YTM is not a true discount rate for pricing cashflows in fixed-income securities due to its dependence on the specific bond.
- It is less suitable for general pricing as it assumes reinvestment at the same rate, which may not reflect actual conditions.
- In corporate valuations, a less precise discount rate (±30%) is often acceptable, but fixed income requires far greater precision (fractions of a percent).

---

## Spot Curve and Discount Rates
- The **spot curve** provides the appropriate discount rate for pricing any cashflow at any point in time, irrespective of the security or issuer.
- Unlike YTM, the spot curve can be applied universally across securities and maturities, offering accurate pricing for any schedule of payments.
- The spot curve is particularly crucial when pricing securities with varying cashflows or maturities, ensuring precision.

Base case Conditions:
  1. Remove treasuries with negative yield or yield equal 0, and remove NA
OLS
  1. At least one (for OLS) treasury maturity on each day
  2. Retain Only treasuries that have not had any cashflow removed
  3. Remove columns that have zero treasuries maturing on that date.
  4. Remove rows that have had any cashflows removed 
  5. Recurse to check Basecase Conditions

---

## Inflation-Adjusted Pricing
- Treasury Inflation-Protected Securities (**TIPS**) generate a spot curve specifically designed for pricing inflation-adjusted cashflows.
- The spot curve derived from TIPS ensures accurate valuation of cashflows accounting for inflationary changes.

---

# Zero-Coupon Bond Yield, Yield-to-Maturity (YTM), and the Spot Curve

## Zero-Coupon Bond Yield: A True Discount Rate
- The yield on a zero-coupon bond corresponds exactly to the discount rate for its maturity. This is because:
  - A zero-coupon bond has no intermediate cashflows (e.g., coupons), paying only a single lump sum at maturity.
  - The absence of interim payments means the bond's yield directly reflects the time-value of money for that specific maturity.

---

## Yield-to-Maturity (YTM): An Approximation

### YTM as an Average Rate
- YTM is a single rate that equates the bond’s price with the present value of its cashflows.
- It represents a weighted average of the discount rates applied to all cashflows from the bond.

### Errors Introduced by YTM
- YTM applies a uniform discount rate across all cashflows, which is inconsistent with the actual term structure of interest rates (typically represented by the spot curve).
- As a result:
  - Early cashflows (shorter maturities) are discounted **too little**, as the YTM underestimates short-term rates derived from the spot curve.
  - Later cashflows (longer maturities) are discounted **too much**, as the YTM overstates long-term rates compared to the spot curve.

---

## Spot Curve: The Correct Tool for Precision
- The **spot curve**, derived from zero-coupon bond yields, provides the correct discount rate for each cashflow based on its specific maturity.
- Unlike YTM, the spot curve accounts for the unique time-value of money for each point in time, ensuring:
  - Early cashflows are discounted using shorter-term (lower) rates.
  - Later cashflows are discounted using longer-term (higher) rates.

---

## Net Effect on Bond Pricing
- While YTM introduces errors in discounting individual cashflows:
  - The **under-discounting of early cashflows** is balanced by the **over-discounting of later cashflows**.
  - This compensatory effect ensures the bond’s total price, as calculated using YTM, is correct for that specific bond.
- However, the YTM-based discounting is bond-specific and cannot be used for pricing other cashflows or securities.

---

## Linking Back to Spot Curve
- The **spot curve** is a more versatile and accurate tool for pricing cashflows:
  - It provides precise discount rates tailored to the timing of each cashflow, regardless of the security.
  - In contrast, YTM is tied to the specific bond it is derived from and cannot be used universally.
- By using the spot curve, any cashflow schedule—whether from a bond, project, or other financial instrument—can be accurately discounted to its present value.

---



## Summary
The **spot curve** ensures precision and universality in pricing cashflows, whereas **YTM** serves as a bond-specific approximation that averages discount rates. Zero-coupon bond yields, as the foundation of the spot curve, provide the true discount rates necessary for precise valuation.
