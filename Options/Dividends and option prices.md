# Dividends and option prices

Assume ordinary cash dividends, unchanged option terms, nonnegative rates, and frictionless markets. Values are per share.

## Dividend dates and stock prices

> - Own the shares before the ex-dividend date to qualify. An eligible holder can sell on that date and retain the dividend.
> - Payment usually arrives later. Owning an option alone gives no dividend entitlement.
> - Announced dividends are normally treated as fixed; later, undeclared payments require forecasts. “Expected dividends” includes both.

Holding everything else fixed, the stock loses the present value of the dividend entitlement. Ignoring payment delay, a stock worth 100 paying 2 becomes a share worth 98 plus entitlement worth 2. Total shareholder value remains 100.

Actual prices also reflect news and orders. Reference prices and eligible orders may adjust automatically; the last-traded price updates only with a transaction and need not equal 98.

## Dividend assumptions versus the ex-dividend event

Holding today's stock price and other inputs fixed, higher future dividends favor lower call values and higher put values.

Following one option across the ex-date is a separate comparison. Consider calls with strike 90, zero interest, zero volatility, and a dividend of 2 before expiration:

| Scenario | Stock price | European call | American call |
|---|---:|---:|---:|
| No dividend | 100 | 10 | 10 |
| Dividend known, just before the ex-date | 100 | 8 | 10 |
| Same dividend scenario, just after the ex-date | 98 | 8 | 8 |

- **European:** at $S=100$, it is worth 8 with the dividend versus 10 without it. Across the ex-date it stays at 8. In the ideal model, the isolated known dividend causes no instantaneous value jump for European calls or puts.
- **American:** exercise captures value 10 through shares and dividend entitlement; holding the call across the date leaves value 8. Selling beforehand can also capture 10.

The table isolates the dividend event; actual prices can also move with news, volatility, and time.

## American exercise decisions

- **Calls:** the dividend benefit must outweigh remaining optionality and the financing cost of paying the strike sooner.
- **Puts:** the stock-price adjustment generally favors waiting through the dividend. Exercise still depends on intrinsic value versus continuation value.
- **Short calls:** assignment risk can increase before the ex-date, including exercise by holders whose decisions differ from the model.

An American price can stay at intrinsic value while exercise remains optimal. For $S=80$ and $K=100$, put intrinsic value is 20. With stock price and other inputs fixed:

| Future dividend assumption | Continuation value | American value: $\max(20,\text{continuation})$ | Decision |
|---|---:|---:|---|
| Initial | 19.80 | 20.00 | Exercise |
| Small increase | 19.95 | 20.00 | Exercise |
| Larger increase | 20.50 | 20.50 | Continue |

These tree values are illustrative. Continuation includes later exercise rights; the price rises only when waiting becomes worth more than 20.

Exercising and holding shares retains stock-price risk; selling locks in cash.

## Pricing models

| Dividend input | Treatment |
|---|---|
| Constant yield $q$ | Black-Scholes models a continuous dividend stream, not one cash payment on a specified date. |
| Discrete payments | Use amounts and ex-dividend dates. A tree or finite-difference method can model stock-price adjustments and American exercise. |

For stock price $S$, strike $K$, years remaining $\tau$, and constant continuously compounded risk-free rate $r$, the European call with constant dividend yield $q$ is

$$C_E = Se^{-q\tau}N(d_1)-Ke^{-r\tau}N(d_2),$$

$$d_1=\frac{\ln(S/K)+(r-q+\sigma^2/2)\tau}{\sigma\sqrt{\tau}},\qquad d_2=d_1-\sigma\sqrt{\tau}.$$

Here $\sigma$ is volatility and $N$ is the standard normal cumulative distribution function. The changes follow from the shareholder's return combining price growth and dividends:

- Risk-neutral total expected return is $r$. Dividends supply $q$, leaving stock-price growth of $r-q$, which enters $d_1$ and therefore $d_2$.
- Expected stock value at expiration is $Se^{(r-q)\tau}$. Discounting at $r$ gives $e^{-r\tau}Se^{(r-q)\tau}=Se^{-q\tau}$: the value of receiving the stock later without its intervening dividends.
- The strike is a future cash payment, so it remains discounted at $r$.

Setting $q=0$ recovers the standard formula. Real-world expected returns can differ from these risk-neutral expectations. This formula prices European exercise rights; American exercise still requires a separate decision.

| Quantity | Formula |
|---|---|
| Forward price | $F_{0,\tau}=Se^{(r-q)\tau}$ |
| European put-call parity | $C_E-P_E=Se^{-q\tau}-Ke^{-r\tau}$ |
| European call floor | $C_E\ge\max(Se^{-q\tau}-Ke^{-r\tau},0)$ |
| European put floor | $P_E\ge\max(Ke^{-r\tau}-Se^{-q\tau},0)$ |

A long European call and a short European put with the same strike and expiration have the payoff of buying one share for $K$ at expiration. Their price difference is the value of that commitment today:

$$\underbrace{C_E-P_E}_{\text{value today}}=\underbrace{Se^{(r-q)\tau}}_{\text{risk-neutral expected stock price at expiry}}\underbrace{e^{-r\tau}}_{\text{discount factor}}-\underbrace{Ke^{-r\tau}}_{\text{strike paid at expiry, discounted to today}}$$

$$=Se^{-q\tau}-Ke^{-r\tau}.$$

A European call can therefore be worth less than current intrinsic value. American options retain their immediate-exercise floors.

> Subtracting discrete dividends' present value from $S$ before applying European Black-Scholes is an approximation; it does not handle American exercise by itself. Special dividends may adjust strikes or deliverables, so use the contract's adjusted terms.
