# Bond durations

I always found the whole idea of having a "Macaulay" duration that you then need to correct pretty vague.
Macaulay was an "almost" sensitivity, that felt too much of a coincidence. Aim is to give some structure
to that problem.

## Macaulay duration

He was mostly an emirical economist, and was trying to solve this problem:

> How do we compare yields of bonds with different couponts and maturities?

Just looking at YTM is not enough. Some cases

- for the same YTM and maturity ( say 30y ), one could be a zero coupon bond while other could be the usual bullet
  bond. In one of those you have to wait a very long time before seeing any money.
- for a the same YTM, a shift in yield curve when yields change can have drasticaly different impact on prices

For a zero-coupon bond:

\[
P=\frac{100}{(1+y)^T}
\]

So,

\[
\frac{1}{P}\frac{dP}{dy}=-\frac{T}{1+y}
\]

At \(y=5\%\):

- 3Y bond: \(-3/1.05 \approx -2.86\)
- 15Y bond: \(-15/1.05 \approx -14.29\)

Hence, for a +1% yield move:

- 3Y price ≈ **−2.86%**
- 15Y price ≈ **−14.29%**

Same YTM, very different interest-rate sensitivity.

Now if I ignore the re-investment risk and assume I can reinvest coupons at the original YTM, if I hold
to maturity, my returns still equal yield but mark to market I've lost a lot, clearly these are not equal.

### Idea

What he did was try to find the "center" of the $PV$ cashflows based on how far in time youu get those.
It was not in any way related to sensitivity, rather more along the lines of an "economic" maturity instead
of real maturity.

How quickly do I get my money back is the idea? There is only a relative basis for it. You cannot use
that "year" duration in any real sense of timing.

## Sensitivity ( of price, it's always price ) to yield

just happens to be related similarly to what he did with wighted average. Though here the question
is precisely

> how does price change as the yields change

$$
P=\sum_{i=1}^{n}\frac{C_i}{(1+y)^i}
$$

$$
\frac{\partial P}{\partial y}
=
\sum_{i=1}^{n} C_i\frac{\partial}{\partial y}(1+y)^{-i}
$$

$$
\frac{\partial P}{\partial y}
=
-\sum_{i=1}^{n}\frac{iC_i}{(1+y)^{i+1}}
$$

$$
\frac{1}{P}\frac{\partial P}{\partial y}
=
-\frac{1}{P}
\sum_{i=1}^{n}\frac{iC_i}{(1+y)^{i+1}}
$$

$$
\frac{\Delta P}{P}
\approx
-\frac{1}{P}
\sum_{i=1}^{n}\frac{iC_i}{(1+y)^{i+1}}
\Delta y
$$

$$
\frac{1}{P}\frac{\partial P}{\partial y}
=
-\frac{1}{P}
\sum_{i=1}^{n}\frac{iC_i}{(1+y)^{i+1}}
$$

Factor out $\frac{1}{1+y}$:

$$
\frac{1}{P}\frac{\partial P}{\partial y}
=
-\frac{1}{1+y}
\frac{1}{P}
\sum_{i=1}^{n}\frac{iC_i}{(1+y)^i}
$$

Define Macaulay Duration:

$$
D_{\text{Mac}}
=
\frac{1}{P}
\sum_{i=1}^{n}\frac{iC_i}{(1+y)^i}
$$

Therefore,

$$
\frac{1}{P}\frac{\partial P}{\partial y}
=
-\frac{D_{\text{Mac}}}{1+y}
$$

Hence,

$$
\frac{\Delta P}{P}
\approx
-\frac{D_{\text{Mac}}}{1+y}\Delta y
$$

This explains the misterious $1+y$ factor textbooks add as adjustment and call it "modified duration".

$$
D_{\text{mod}}=\frac{D_{\text{Mac}}}{1+y}
$$
