# Black–Scholes

Before we get to options, recall the log-return equation for geometric Brownian motion (GBM). Assume constant drift $\mu$ and volatility $\sigma$, with both parameters annualized and elapsed time $T$ measured in years.

$$\boxed{\ln(S_T/S_0) \overset{d}{=} (\mu-\tfrac12\sigma^2)T + \sigma\sqrt{T}Z}, \quad Z \sim N(0,1).$$

Here, $S_0$ is the starting price and $S_T$ is the price at time $T$. The symbol $\overset{d}{=}$ means equality in distribution.

$\sigma$ is the annualized volatility of log returns: $\ln(S_T/S_0)$ has standard deviation $\sigma\sqrt{T}$. It is not the standard deviation of the simple return $S_T/S_0-1$, though the two are close over short intervals with small price changes.

The components are:

- $\mu T$: the drift contribution.
- $-\tfrac12\sigma^2T$: the Itô correction to log growth.
- $\sigma\sqrt{T}Z$: the random contribution, equal in distribution to $\sigma W_T$, where $W_t$ is standard Brownian motion.

The drift and Itô correction scale with $T$. The random contribution has standard deviation $\sigma\sqrt{T}$.

## Pricing a call

Let $K$ be the strike, $S_0$ the current stock price, $T$ the time to expiry in years, and $r$ the continuously compounded annual risk-free rate.

Assume a European call on a non-dividend-paying stock, constant $r$ and $\sigma > 0$, and frictionless continuous trading. Take $S_0,K,T > 0$.

At expiry, the call's payoff is

$$C_T = \max(S_T-K,0).$$

Black–Scholes gives its value today:

$$\boxed{C_0=\underbrace{S_0N(d_1)}_{\text{PV of expected stock received}}-\underbrace{Ke^{-rT}N(d_2)}_{\text{PV of expected strike paid}}}$$

Here, $N(x) = P(Z \leq x)$ is the standard normal cumulative distribution function, with $Z \sim N(0,1)$.

### The terms in $d_1$ and $d_2$

$$\boxed{d_1 = \frac{\ln(S_0/K)+rT+\tfrac12\sigma^2T}{\sigma\sqrt{T}}}.$$

$$\boxed{d_2 = \frac{\ln(S_0/K)+rT-\tfrac12\sigma^2T}{\sigma\sqrt{T}} = d_1-\sigma\sqrt{T}}.$$

- $\ln(S_0/K)$: log moneyness, measuring how far the current price is above or below the strike in log terms.
- $rT$: the growth contribution under risk-neutral pricing.
- $\tfrac12\sigma^2T$: the volatility adjustment, with opposite signs in $d_1$ and $d_2$.
- $\sigma\sqrt{T}$: the standard deviation of the log return over the remaining time.

### How GBM leads to $N(d_2)$: probability of exercise

Under the risk-neutral measure $Q$, the stock's drift is $r$ instead of its real-world drift $\mu$. Let $Z = W_T^Q/\sqrt{T} \sim N(0,1)$, where $W^Q$ is standard Brownian motion under $Q$. The GBM log-return equation is

$$\boxed{\ln(S_T/S_0) = (r-\tfrac12\sigma^2)T + \sigma\sqrt{T}Z}.$$

A call expires in the money when $S_T > K$. Expressing this condition in log returns gives

$$\ln(S_T/S_0) > \ln(K/S_0).$$

Substitute the GBM equation:

$$(r-\tfrac12\sigma^2)T + \sigma\sqrt{T}Z > \ln(K/S_0).$$

Subtract the expected log return and divide by $\sigma\sqrt{T} > 0$:

$$\sigma\sqrt{T}Z > \ln(K/S_0)-(r-\tfrac12\sigma^2)T.$$

$$Z > \frac{\ln(K/S_0)-(r-\tfrac12\sigma^2)T}{\sigma\sqrt{T}}.$$

Using $-\ln(K/S_0) = \ln(S_0/K)$, we can write the threshold as $-d_2$:

$$\boxed{Z > -\underbrace{\frac{\ln(S_0/K)+(r-\tfrac12\sigma^2)T}{\sigma\sqrt{T}}}_{d_2}}.$$

Therefore,

$$P^Q(S_T > K) = P^Q(Z > -d_2).$$

By symmetry of the standard normal distribution,

$$\boxed{P^Q(S_T > K) = P^Q(Z < d_2) = N(d_2)}.$$

GBM makes log returns normal. The quantity $d_2$ measures how far the log strike lies below the risk-neutral expected log price at expiry, in standard deviations. Applying $N$ gives the risk-neutral probability of exercise.

### What $N(d_1)$ means

$N(d_1)$ is the stock-price-weighted probability of exercise. Each outcome is weighted by $S_T/E^Q[S_T]$, so higher terminal stock prices count more.

Let $\mathbf1_{\{S_T>K\}}$ equal $1$ when the call finishes in the money and $0$ otherwise. The expected stock received is the probability of exercise times the expected stock price conditional on exercise:

$$E^Q[S_T\mathbf1_{\{S_T>K\}}] = \underbrace{P^Q(S_T>K)}_{\text{Probability of exercise}} \times \underbrace{E^Q[S_T\mid S_T>K]}_{\text{Expected stock price if ITM}}.$$

Under risk-neutral GBM,

$$P^Q(S_T>K) = N(d_2).$$

$$E^Q[S_T\mid S_T>K] = S_0e^{rT}\frac{N(d_1)}{N(d_2)}.$$

The unconditional expected stock price is $E^Q[S_T] = S_0e^{rT}$. The ratio $N(d_1)/N(d_2)$ adjusts it upward because we are considering only outcomes where the call finishes in the money.

Multiplying the exercise probability by the conditional expectation cancels $N(d_2)$:

$$\boxed{E^Q[S_T\mathbf1_{\{S_T>K\}}] = N(d_2)\times S_0e^{rT}\frac{N(d_1)}{N(d_2)} = S_0e^{rT}N(d_1)}.$$

Discounting to today gives the stock component:

$$\boxed{e^{-rT}E^Q[S_T\mathbf1_{\{S_T>K\}}] = S_0N(d_1)}.$$

### Why does $d_1$ have a plus sign?

Recall that

$$d_2 = \frac{\ln(S_0/K)+(r-\tfrac12\sigma^2)T}{\sigma\sqrt{T}}.$$

The minus $\tfrac12\sigma^2$ comes from the Itô correction in GBM log returns.

For the stock component, each exercise outcome is weighted by the terminal stock price:

$$S_T = S_0e^{(r-\tfrac12\sigma^2)T+\sigma\sqrt{T}Z}.$$

With a strike of \$100, a terminal price of \$150 contributes more to the payoff than \$110. The factor responsible for this weighting is

$$e^{\sigma\sqrt{T}Z}.$$

It gives more weight to high values of $Z$, which correspond to higher terminal stock prices. After normalizing, this exponential weighting shifts the normal distribution's mean from $0$ to $\sigma\sqrt{T}$, leaving its variance at $1$.

The exercise threshold is still $Z > -d_2$. Under the shifted distribution, its probability becomes $N(d_2+\sigma\sqrt{T})$. Therefore,

$$\boxed{d_1 = d_2+\sigma\sqrt{T} = \frac{\ln(S_0/K)+(r+\tfrac12\sigma^2)T}{\sigma\sqrt{T}}}.$$

This changes the volatility adjustment from $-\sigma^2/2$ to $+\sigma^2/2$.

### Why is there no explicit discount factor in the stock component?

The stock component is a probability-weighted conditional expectation, discounted to today.

Both payoff components are discounted. For the stock component, the cancellation is

$$\boxed{e^{-rT}E^Q[S_T\mathbf1_{\{S_T>K\}}] = e^{-rT}S_0e^{rT}N(d_1) = S_0N(d_1)}.$$

The strike payment $K$ is fixed, so we discount it to today and weight it by the exercise probability. The stock price changes, and under risk-neutral pricing its expected value already includes growth at the risk-free rate. That growth factor $e^{rT}$ cancels the discount factor $e^{-rT}$, leaving $S_0N(d_1)$.
