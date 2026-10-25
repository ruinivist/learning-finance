# Early exercise: American vs European options

- American options can be exercised before expiration on permitted dates.
- European options can be exercised only at expiration.
- Both types can be sold before expiration.
- A short American option can be assigned before expiration, even when exercise is economically suboptimal for the holder.

Assume identical contract terms, no dividends, nonnegative rates, and frictionless markets unless stated otherwise.
Examples are per share and ignore fees and bid-ask spreads.

## Value and price floors

The American holder can choose to wait, so

$$
V_A \ge V_E, \qquad \text{early-exercise premium} = V_A - V_E \ge 0.
$$

The premium can be zero. Subscripts $A$ and $E$ mean American and European; $C$ means call and $P$ means put. Here $V$ is option value, $S$ the stock price, $K$ the strike, $r$ the continuously compounded risk-free rate, and $\tau$ the years remaining.

Intrinsic value is $\max(S-K,0)$ for a call and $\max(K-S,0)$ for a put.

| Option | Floor from immediate exercise | No-arbitrage price floor |
|---|---|---|
| European call | No immediate-exercise right | $\max(S-Ke^{-r\tau},0)$ |
| American call | $\max(S-K,0)$ | Also $\max(S-Ke^{-r\tau},0)$ |
| European put | No immediate-exercise right | $\max(Ke^{-r\tau}-S,0)$ |
| American put | $\max(K-S,0)$ | $\max(K-S,0)$ |

An American option must be worth at least intrinsic value. For calls without dividends, the European floor already meets that guarantee. For puts, immediate exercise can raise the floor.

Examples with $r=5\%$ and $\tau=1$:

- **Call**, $S=100$, $K=90$: intrinsic value is 10; both price floors are $100-90e^{-0.05}\approx14.39$. Delaying the strike payment accounts for the 4.39 difference.
- **Put**, $S=10$, $K=100$: European floor is about 85.12; American floor is 90.

These are lower bounds, not necessarily actual prices.

## Why a call without dividends should not be exercised early

Waiting preserves:

- Interest earned by postponing the strike payment.
- The right to walk away if the stock falls below the strike.

There is no dividend income lost by waiting. Under these assumptions, early exercise adds no value and $C_A=C_E$.

Start with the same assets: a call with strike 80 plus 80 cash. Either exercise now and hold shares, or keep the call and invest the cash. With one year remaining, 80 grows to $80e^{0.05}\approx84.10$ at 5%.

| Interest rate | Stock price at expiration | Exercise now and hold shares | Keep call and cash |
|---|---:|---:|---|
| 0% | 120 | 120 | Exercise: shares worth 120 |
| 0% | 50 | 50 | Let expire: 80 cash |
| 5% | 120 | 120 | Exercise: 124.10 total (120 in shares + 4.10 cash) |
| 5% | 50 | 50 | Let expire: 84.10 cash |

For any final stock price $S_T$, the difference in wealth at expiration is

$$
W_{\text{keep call}}-W_{\text{exercise now}}=(K-S_T)^+ + K(e^{r\tau}-1)\ge0.
$$

Here $x^+=\max(x,0)$. The two terms are downside protection and interest. Early exercise is never strictly better; at zero rates with no relevant uncertainty, the choices can tie.

In risk-neutral pricing, the stock's expected growth rate is also $r$. The stock remains risky, and its real-world expected return can differ. The comparison above holds for every final stock price, so it needs no growth forecast.

## When a put should be exercised early

Exercising a put means delivering stock and receiving $K$. The decision balances:

- Interest earned by receiving the strike sooner.
- The value of keeping the option, including future exercise opportunities.

With other inputs fixed in the standard model, higher interest rates generally favor early put exercise; higher volatility favors waiting.

A deep-in-the-money put has less additional payoff available from further stock declines. With $K=100$ and $S=10$, intrinsic value is 90; even a fall to zero adds only 10. Early exercise becomes more likely, but is not automatic.

Exercise when intrinsic value is at least continuation value:

$$
P_A=\max\big((K-S)^+,\ \text{continuation value}\big).
$$

A binomial tree estimates continuation value using time remaining, rates, volatility, and dividends. It preserves the right to exercise later.

Example: $K=100$, one year remaining, $r=5\%$, volatility 20%, and no dividends. Approximate values from a 1,500-step binomial tree:

| Stock price | Intrinsic value | European Black-Scholes value | American value | Model decision |
|---|---:|---:|---:|---|
| 80 | 20.00 | 16.98 | 20.00 | Exercise |
| 85 | 15.00 | 13.34 | 15.32 | Continue |
| 95 | 5.00 | 7.63 | 8.45 | Continue |

> At $S=85$, the European value is below intrinsic, yet keeping the American put is worth more than exercising. Comparing European Black-Scholes value with intrinsic alone is insufficient.

| Quantity | Calculation at $S=85$ | Meaning |
|---|---|---|
| Early-exercise premium | $P_A-P_E=15.32-13.34=1.98$ | Value of extra exercise opportunities, including future ones |
| Value above intrinsic (extrinsic value) | $P_A-(K-S)^+=15.32-15=0.32$ | Value sacrificed by exercising now |

A positive early-exercise premium does not mean exercise is optimal today.

When exiting, compare the executable option bid with net exercise proceeds after costs. Selling captures more if that bid is higher.

## Locking in a profit

Holding the call can still lose money. To lock in profit, sell it.

Suppose $S=100$, $K=80$, the call cost you 12, and you can now sell it for 23:

| Action | Cash received, net of strike payment | Locked-in profit |
|---|---:|---:|
| Sell the call | 23 | 11 |
| Exercise and immediately sell shares | $100-80=20$ | 8 |

Selling preserves the $23-20=3$ of value above intrinsic. You can then invest the proceeds at the risk-free rate. Exercising and holding shares leaves you exposed to stock-price changes.

If you want to own shares, selling the call and buying stock can also preserve that extra value, subject to prices and costs.

## When early exercise can matter

- A call with dividends may be worth exercising before an ex-dividend date if the dividend benefit outweighs remaining optionality and the cost of paying the strike sooner.
- Negative rates or unusual funding and borrowing conditions can change the call argument.

The closed-form Black-Scholes formulas price European exercise rights. American pricing generally requires a tree or finite-difference method comparing intrinsic value with continuation value, including future exercise opportunities.

## Problems

1. You own an American call with $S=105$, $K=90$, three months remaining, no dividends, and positive interest rates. You paid 7 and can sell it for 18. To lock in profit, should you sell, exercise and sell the shares, or exercise and keep the shares? Calculate the profit.

2. You can buy a fresh American call with $S=105$ and $K=90$ for 12. Is there an arbitrage? Show the cash flows. Does the premium paid for an earlier position matter?

3. An American put has $S=85$, $K=100$, European value 13.34, and American value 15.32. Should you exercise now? Which value matters?

4. For the put in problem 3, calculate the early-exercise premium and the value above intrinsic. Why can the former be positive while exercising today is suboptimal?

5. With no dividends, zero interest rates, positive volatility, and time remaining, should a call or put be exercised early? Does raising rates to 5% guarantee that put exercise becomes optimal?

6. An American call is in the money and the stock goes ex-dividend tomorrow. Should you automatically exercise today? What would you gain and sacrifice? Would holding the resulting shares lock in profit?

7. You are short an American call without dividends, with positive interest rates. Can optimal-exercise theory rule out early assignment?

8. Let $S=10$, $K=100$, $r=5\%$, $\tau=1$, and volatility be zero. Calculate the European put value. Is its price below intrinsic an arbitrage? What if an American put could be bought at the same price?

## Answers

1. Sell the call: profit is $18-7=11$. Exercise and immediate sale capture intrinsic value of $105-90=15$, giving profit $15-7=8$. Exercise and holding leave stock-price exposure. The original premium cancels when comparing selling with exercising; selling preserves the extra $18-15=3$.

2. Buy the call for 12, pay 90 to exercise, and sell the share for 105. Net profit is $105-90-12=3$. This is a fresh purchase, so the old premium is irrelevant. If an existing call originally cost 7 and could now be sold for 12, selling would realize 5 profit; exercising and selling the share would realize 8.

3. Continue or sell. Intrinsic value is $100-85=15$, while keeping the American put is worth 15.32. Exercise sacrifices 0.32. The European value excludes future early-exercise opportunities and cannot substitute for American continuation value.

4. Early-exercise premium is $15.32-13.34=1.98$; value above intrinsic is $15.32-15=0.32$. The first includes the right to exercise at future dates. Those rights can be valuable even when using them today sacrifices value.

5. Neither benefits from early exercise under these assumptions. At zero rates, paying or receiving the strike sooner has no interest benefit, while waiting preserves option rights. For a share plus a put, exercising now gives $K$ cash; waiting gives $\max(S_T,K)$ at expiration. Positive rates make early put exercise more likely, but it still requires intrinsic value to be at least continuation value.

6. Exercise only if the dividend benefit outweighs the remaining option value and the financing cost of paying the strike sooner. Acquire the shares before the ex-dividend date to qualify. Exercise gives shares, so holding them retains stock-price risk. Selling the call locks in its sale value; exercising and selling shares today captures intrinsic value but forfeits the upcoming dividend entitlement.

7. No. The holder retains the contractual exercise right and may make a mistake or face conditions outside the model. Optimal-exercise theory describes the value-maximizing decision under specified assumptions; it does not require holders to follow it.

8. The zero-volatility Black-Scholes limit gives $P_E=Ke^{-r\tau}-S=100e^{-0.05}-10\approx85.12$. Intrinsic value is 90. The European holder cannot exercise immediately, so the gap creates no immediate-exercise arbitrage. With positive volatility, 85.12 is the lower bound, not necessarily the actual price. If the American put were priced the same, buy it for about 85.12, buy a share for 10, and exercise to receive 100: profit is about $100-10-85.12=4.88$. Its value must be at least 90. Both styles require paying the option premium upfront; exercise timing creates the difference.