# Brownian motion

These notes aim to convey the intuition without a full mathematical treatment.

## A random walk

Say we start at $S_0 = 0$. At each step, the increment is $X_i = +1$ or $-1$, each with probability $1/2$.

Assume the increments are independent, and we take $n$ steps.

The displacement is $S_n = \sum_{i=1}^{n} X_i$. What are $E[S_n]$ and $\operatorname{Var}(S_n)$?

By linearity of expectation, $E[S_n] = nE[X_i] = 0$. Independence is not needed here.

Independence makes the covariances zero, so $\operatorname{Var}(S_n) = \sum_{i=1}^{n} \operatorname{Var}(X_i) = n\operatorname{Var}(X_i)$.

Since $E[X_i^2] = 1$ and $E[X_i] = 0$, $\operatorname{Var}(X_i) = 1 - 0^2 = 1$.

Therefore, $\operatorname{Var}(S_n) = n$.

**The standard deviation after $n$ steps is $\sqrt{n}$.**

## Relation to normals

$$S_n = \sum_{i=1}^{n} X_i$$

The increments $X_i$ are independent. Their sum has variance $n$ and standard deviation $\sqrt{n}$.

Divide by $\sqrt{n}$ to get a sum with mean $0$ and variance $1$. By the central limit theorem (CLT),

$$\frac{X_1 + \cdots + X_n}{\sqrt{n}} \xrightarrow{d} N(0,1) \quad \text{as } n \to \infty.$$

Here, $\xrightarrow{d}$ means convergence in distribution. The normalized sum approaches a standard normal distribution; it is not exactly normal for finite $n$.

For large $n$, the original, unscaled sum is approximately $N(0,n)$.

If $Z_i \sim N(0,1)$ and $c$ is a constant, scaling gives

$$cZ_i \sim N(0,c^2).$$

Now let each step last a fixed time $\Delta t > 0$, so $n$ steps cover $t = n\Delta t$. In the Brownian motion model, increments over non-overlapping intervals are independent and exactly normal, with variance equal to the elapsed time.

For the $i$th increment, $\Delta W_i = W_{i\Delta t} - W_{(i-1)\Delta t}$,

$$\boxed{\Delta W_i \overset{d}{=} \sqrt{\Delta t}\,Z_i}, \quad Z_i \sim N(0,1).$$

The symbol $\overset{d}{=}$ means equality in distribution. Equivalently,

$$\boxed{W_{t+\Delta t} - W_t \sim N(0,\Delta t)}.$$

Why $Z_i$? Each increment uses an independent draw from $N(0,1)$; the subscript identifies the $i$th draw. We can construct the increments as

$$\boxed{\underbrace{\Delta W_i}_{\text{Random movement}} = \underbrace{\sqrt{\Delta t}}_{\text{Time scale}} \times \underbrace{Z_i}_{\text{Random shock}}}.$$

---

## Properties of Brownian motion

A _standard Brownian motion_ \(W_t\), also called a Wiener process, is a continuous-time stochastic process satisfying four properties:

**1. It starts at zero.**

$$W_0=0.$$

**2. It has independent increments.**

Movements over non-overlapping time intervals are independent.

For example, \(W_2-W_1\) and \(W_3-W_2\) are independent. Knowing the movement during the first interval tells us nothing about the movement during the second.

**3. It has stationary, normally distributed increments.**

For \(0\leq s<t\),

$$\boxed{W_t-W_s\sim N(0,t-s).}$$

Stationarity means the distribution depends only on the _length_ of the interval, not its starting time.

Consequently,

$$E[W_t-W_s]=0,$$

$$\operatorname{Var}(W_t-W_s)=t-s.$$

Setting \(s=0\), we obtain

$$\boxed{W_t\sim N(0,t).}$$

Thus, the **variance grows linearly with time**, while the standard deviation grows with its square root:

$$\operatorname{SD}(W_t)=\sqrt t.$$

**4. Its paths are continuous.**

Brownian motion does not jump discontinuously. However, its paths are almost surely nowhere differentiable.

Intuitively, the movement remains irregular regardless of how closely we examine it. This is one reason ordinary calculus is insufficient for working with Brownian motion.

### Covariance

For any $s,t \geq 0$,

$$\boxed{\operatorname{Cov}(W_s,W_t)=\min(s,t).}$$

To derive it, suppose \(s<t\). We can write

$$W_t=W_s+(W_t-W_s).$$

Then

$$\operatorname{Cov}(W_s,W_t)=\operatorname{Var}(W_s)+\operatorname{Cov}(W_s,W_t-W_s).$$

The second term is zero because future increments are independent of past movements.

Therefore,

$$\operatorname{Cov}(W_s,W_t)=s.$$

This gives the general result.

### Martingale property

Brownian motion is also a _martingale_.

Given everything we know up to time \(s\), the expected value at a future time \(t>s\) is simply its current value:

$$\boxed{E[W_t\mid\mathcal F_s]=W_s.}$$

Here, \(\mathcal F_s\) represents all information available up to time \(s\).

This follows because future Brownian increments have conditional expectation zero.

A martingale has no predictable drift conditional on its current information.

---

## Brownian motion with drift and volatility

So far, standard Brownian motion has zero expected movement and unit variance per unit time.

We can generalize it by introducing two parameters:

- \(\mu\): the _drift_, controlling the expected direction and rate of movement.
- \(\sigma\): the _volatility_, controlling the magnitude of random fluctuations.

Define

$$\boxed{X_t=X_0+\mu t+\sigma W_t.}$$

This is called _arithmetic Brownian motion_ (ABM), or Brownian motion with drift.

We can interpret its three components:

$$X_t=\underbrace{X_0}_{\text{Starting value}}+\underbrace{\mu t}_{\text{Drift}}+\underbrace{\sigma W_t}_{\text{Random movement}}.$$

Because \(W_t\sim N(0,t)\),

$$X_t\sim N(X_0+\mu t,\sigma^2t).$$

> basically you give a new mean assuming the randoms cancel out, and to get var of $\sigma^2$ scale by that

Therefore,

$$\boxed{E[X_t]=X_0+\mu t}$$

and

$$\boxed{\operatorname{Var}(X_t)=\sigma^2t.}$$

**The important distinction is that expected displacement scales with \(t\), while the standard deviation of random displacement scales with \(\sqrt t\).**

### Looking at a small time interval

Over a small interval \(\Delta t\),

$$\Delta X=\mu\Delta t+\sigma\Delta W.$$

We know that

$$\Delta W\overset d=\sqrt{\Delta t}Z,\qquad Z\sim N(0,1).$$

Substituting,

$$\boxed{\Delta X\overset d=\mu\Delta t+\sigma\sqrt{\Delta t}Z.}$$

This is a particularly useful equation.

It says that movement over a short interval consists of:

1. A predictable drift component, \(\mu\Delta t\).
2. A random component, \(\sigma\sqrt{\Delta t}Z\).

In continuous-time notation, we write

$$\boxed{dX_t=\mu\,dt+\sigma\,dW_t.}$$

This is a _stochastic differential equation_ (SDE).

Unlike an ordinary differential equation, an SDE contains a random component driven by Brownian motion.

---

## From arithmetic to geometric Brownian motion

Arithmetic Brownian motion models **absolute changes**.

For example, suppose \(X_t=100\) and a particular shock causes it to decrease by 5. The same shock would also cause a decrease of 5 if \(X_t=200\).

But stock prices are usually modeled in terms of _percentage changes_, rather than fixed absolute changes.

A \$5 movement represents a 5% change for a \$100 stock, but only a 2.5% change for a \$200 stock.

We therefore want a model in which the size of each movement is proportional to the current stock price.

This motivates _geometric Brownian motion_ (GBM):

$$\boxed{dS_t=\mu S_t\,dt+\sigma S_t\,dW_t.}$$

Dividing by \(S_t\),

$$\boxed{\frac{dS_t}{S_t}=\mu\,dt+\sigma\,dW_t.}$$

Interpretation:

- \(dS_t/S_t\) represents the instantaneous proportional price change.
- \(\mu\,dt\) is the drift contribution.
- \(\sigma\,dW_t\) is the random contribution.

Notice how similar this is to arithmetic Brownian motion. The difference is that GBM applies the drift and random shock to _proportional changes_, rather than absolute changes.

For a small time interval, we can approximate

$$\boxed{\frac{\Delta S}{S}\approx\mu\Delta t+\sigma\sqrt{\Delta t}Z.}$$

For example, if annualized volatility is 20%, the standard deviation of the random proportional movement over one quarter of a year is approximately

$$0.20\sqrt{0.25}=0.10.$$

So the standard deviation of the random return component is approximately 10%.

An important consequence of GBM is that, starting from a positive price, the stock price remains positive.

---

## Solving geometric Brownian motion

We now have

$$\frac{dS_t}{S_t}=\mu\,dt+\sigma\,dW_t.$$

Our goal is to obtain an expression for \(S_T\) in terms of the starting price \(S_0\).

At first glance, we might try integrating both sides and conclude

$$\ln(S_T/S_0)=\mu T+\sigma W_T.$$

**But this is incorrect.**

The problem is that the ordinary calculus identity \(d\ln S=dS/S\) does not hold without a correction when \(S\) follows a stochastic process driven by Brownian motion.

### Why do we need a correction?

Recall the Taylor expansion

$$\ln(1+x)=x-\frac{x^2}{2}+\frac{x^3}{3}-\cdots.$$

For small \(x\),

$$\ln(1+x)\approx x-\frac{x^2}{2}.$$

Now let \(x\) represent a small proportional stock-price change:

$$x=\frac{\Delta S}{S}\approx\mu\Delta t+\sigma\Delta W.$$

Then

$$\Delta\ln S\approx\frac{\Delta S}{S}-\frac12\left(\frac{\Delta S}{S}\right)^2.$$

The important observation is that Brownian increments are of order \(\sqrt{\Delta t}\).

Consequently, their squares are of order \(\Delta t\), and cannot simply be discarded.

This is captured by Brownian motion's _quadratic variation_ and the symbolic Itô rule

$$(dW_t)^2=dt.$$

Terms involving \(dt^2\) or \(dt\,dW_t\) vanish at the relevant order, but the squared Brownian increment contributes.

Therefore,

$$d\ln S_t=\mu\,dt+\sigma\,dW_t-\frac12\sigma^2dt.$$

Rearranging,

$$\boxed{d\ln S_t=(\mu-\frac12\sigma^2)dt+\sigma\,dW_t.}$$

This result is obtained formally using **Itô's lemma**.

### Integrating over time

Assume \(\mu\) and \(\sigma\) are constant.

Integrating from time 0 to time \(T\),

$$\ln S_T-\ln S_0=(\mu-\frac12\sigma^2)T+\sigma W_T.$$

Therefore,

$$\boxed{\ln(S_T/S_0)=(\mu-\frac12\sigma^2)T+\sigma W_T.}$$

Since \(W_T\overset d=\sqrt T Z\), we can write

$$\boxed{\ln(S_T/S_0)\overset d=(\mu-\frac12\sigma^2)T+\sigma\sqrt T Z.}$$

Exponentiating gives

$$\boxed{S_T\overset d=S_0e^{(\mu-\frac12\sigma^2)T+\sigma\sqrt T Z}.}$$

This is the terminal stock-price distribution under geometric Brownian motion.

### Interpreting the volatility correction

The term

$$-\frac12\sigma^2T$$

is the _Itô correction_.

Its presence reflects the difference between arithmetic growth and logarithmic growth.

Under GBM,

$$E[S_T]=S_0e^{\mu T},$$

but

$$E[\ln(S_T/S_0)]=(\mu-\frac12\sigma^2)T.$$

Volatility reduces expected **logarithmic** growth relative to the drift parameter \(\mu\), even though the expectation of the stock price itself remains \(S_0e^{\mu T}\).

---

## Connecting geometric Brownian motion to Black–Scholes

The Black–Scholes model assumes that the underlying stock follows GBM with constant volatility.

However, when pricing derivatives, we don't generally use the stock's real-world expected return \(\mu\).

Instead, we use a _risk-neutral probability measure_.

Under the assumptions of Black–Scholes, including no dividends and a constant risk-free interest rate \(r\), the stock-price dynamics under this measure become

$$\boxed{\frac{dS_t}{S_t}=r\,dt+\sigma\,dW_t^Q.}$$

Here, \(W_t^Q\) is Brownian motion under the risk-neutral measure \(Q\).

The drift is now \(r\), rather than \(\mu\).

The justification comes from no-arbitrage pricing and hedging arguments, which we can study separately.

Using the GBM result derived above,

$$\boxed{\ln(S_T/S_0)=(r-\frac12\sigma^2)T+\sigma W_T^Q.}$$

At a fixed maturity, we can write this in distribution as

$$\ln(S_T/S_0)\overset d=(r-\frac12\sigma^2)T+\sigma\sqrt T Z,$$

where \(Z\sim N(0,1)\) under \(Q\).

Now introduce the strike price \(K\).

Using

$$\ln(S_T/K)=\ln(S_0/K)+\ln(S_T/S_0),$$

we obtain

$$\boxed{\ln(S_T/K)\overset d=\underbrace{\ln(S_0/K)}_{\text{Current log moneyness}}+\underbrace{(r-\frac12\sigma^2)T}_{\text{Log drift}}+\underbrace{\sigma\sqrt T Z}_{\text{Random movement}}.}$$

This is the equation connecting Brownian motion to the Black–Scholes pricing formula.

---

## Deriving \(d_2\)

Consider a European call option with strike \(K\).

It finishes in the money if

$$S_T>K.$$

Equivalently,

$$\ln(S_T/K)>0.$$

Substituting the log-price distribution,

$$\ln(S_0/K)+(r-\frac12\sigma^2)T+\sigma\sqrt T Z>0.$$

Rearranging,

$$Z>-\frac{\ln(S_0/K)+(r-\frac12\sigma^2)T}{\sigma\sqrt T}.$$

Define

$$\boxed{d_2=\frac{\ln(S_0/K)+(r-\frac12\sigma^2)T}{\sigma\sqrt T}.}$$

The condition becomes

$$Z>-d_2.$$

Let $N(x) = P(Z \leq x)$ be the standard normal cumulative distribution function. By symmetry,

$$P^Q(Z>-d_2)=N(d_2).$$

Thus,

$$\boxed{P^Q(S_T>K)=N(d_2).}$$

**Interpretation:** \(N(d_2)\) is the risk-neutral probability that the call finishes in the money.

The logarithmic moneyness term measures how far the stock starts from the strike. The drift term adjusts for the evolution of log prices, and the denominator measures the standard deviation of the log return.

---

## Where does \(d_1\) come from?

We have derived \(d_2\) from the probability that the stock finishes above the strike.

Now consider the actual payoff of a call:

$$C_T=\max(S_T-K,0).$$

Using an indicator function,

$$C_T=S_T\mathbf1_{\{S_T>K\}}-K\mathbf1_{\{S_T>K\}}.$$

The first component depends on the stock's value when the option finishes in the money.

The second component depends only on whether the option finishes in the money.

Under risk-neutral pricing,

$$C_0=e^{-rT}E^Q[C_T].$$

Therefore,

$$C_0=e^{-rT}E^Q[S_T\mathbf1_{\{S_T>K\}}]-Ke^{-rT}P^Q(S_T>K).$$

We already know that

$$P^Q(S_T>K)=N(d_2).$$

For the first component, higher stock-price outcomes contribute more to the expectation.

Since the terminal stock price contains the factor \(e^{\sigma\sqrt T Z}\), this weights large positive normal shocks more heavily.

Mathematically, weighting a standard normal density by \(e^{aZ}\), and normalizing it, shifts the mean by \(a\).

Here,

$$a=\sigma\sqrt T.$$

This produces the shifted quantity

$$\boxed{d_1=d_2+\sigma\sqrt T.}$$

Substituting our expression for \(d_2\),

$$\boxed{d_1=\frac{\ln(S_0/K)+(r+\frac12\sigma^2)T}{\sigma\sqrt T}.}$$

The stock component of the discounted expected payoff evaluates to

$$e^{-rT}E^Q[S_T\mathbf1_{\{S_T>K\}}]=S_0N(d_1).$$

Hence \(d_1\) differs from \(d_2\) because we are now weighting outcomes by stock value, not merely counting how frequently the stock finishes above the strike.

---

## The Black–Scholes formula

Combining the two payoff components gives the European call option pricing formula:

$$\boxed{C_0=S_0N(d_1)-Ke^{-rT}N(d_2),}$$

where

$$\boxed{d_1=\frac{\ln(S_0/K)+(r+\frac12\sigma^2)T}{\sigma\sqrt T}}$$

and

$$\boxed{d_2=d_1-\sigma\sqrt T.}$$

The relationship to the original Brownian motion model is now clear:

- Brownian motion describes the random shocks.
- Geometric Brownian motion uses these shocks to model proportional stock-price changes.
- Itô's lemma introduces the log-growth correction.
- Risk-neutral pricing replaces the physical drift with the risk-free rate under the pricing measure.
- \(d_2\) comes from the risk-neutral probability of finishing above the strike.
- \(d_1\) comes from weighting those outcomes by the terminal stock price.

For a European put, put-call parity gives

$$P_0=C_0-S_0+Ke^{-rT},$$

which simplifies to

$$\boxed{P_0=Ke^{-rT}N(-d_2)-S_0N(-d_1).}$$

These formulas assume the standard Black–Scholes setting: European exercise, a non-dividend-paying underlying, constant volatility and interest rates, and frictionless continuous trading.
