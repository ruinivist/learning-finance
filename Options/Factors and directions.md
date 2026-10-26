# Factors and directions

## Interest rate

Higher rates raise call premiums and lower put premiums, holding other inputs fixed. Assume European options on a stock with no dividends, constant volatility, and Black-Scholes pricing. Here $S_0$ is today's stock price, $K$ the strike, $\tau$ years to expiry, and $r$ the continuously compounded annual risk-free rate.

These are three ways to justify the same underlying financing effect; they do not add together as separate effects.

### 1. Black-Scholes

Under the risk-neutral measure $Q$,

$$E^Q[S_\tau]=S_0e^{r\tau}.$$

Higher $r$ shifts terminal stock prices upward while $K$ stays fixed. Calls benefit; puts lose value. A put's payoff is $\max(K-S_\tau,0)$: it falls as the stock rises, but stops at zero.

Discounting also matters. Let $A=S_0e^{-\sigma^2\tau/2+\sigma\sqrt{\tau}Z}$, where $\sigma$ is annualized volatility and $Z\sim N(0,1)$ under $Q$. Today's premiums are

$$C_0=E^Q[\max(A-Ke^{-r\tau},0)].$$

$$P_0=E^Q[\max(Ke^{-r\tau}-A,0)].$$

Higher $r$ reduces $Ke^{-r\tau}$ while leaving $A$ unchanged. The call expression rises; the put expression falls, with each payoff floored at zero. This establishes the directions within the model, rather than predicting actual stock-price moves.

### 2. Paying or receiving the fixed strike later

A call lets you defer paying $K$ until expiry. Higher rates make that delay more valuable because the cash can earn more interest. A put lets you receive $K$ at expiry; higher rates make that future receipt worth less today. Both follow from the strike's present value, $Ke^{-r\tau}$, falling as $r$ rises.

### 3. Financing a delta hedge

A delta-neutral hedge offsets the option position's sensitivity to the stock price with shares.

- Short call or long put: buy shares to hedge. Higher rates increase borrowing costs or interest forgone on cash. A call seller needs more premium; a put buyer is willing to pay less.
- Long call or short put: short shares to hedge. In the model, the proceeds earn interest. Higher rates let a call buyer pay more or a put seller accept less. Lower rates hurt these positions.

For existing positions, higher rates help long calls and short puts, and hurt short calls and long puts. The premium already paid or received stays fixed; the price to close changes.

> Sensitivity to interest rate is $\rho$
