# Risk-neutral pricing

For one gamble, at zero interest:

- $X$: the random payout, without subtracting the entry fee; 100 if you win, 0 if you lose.
- $P$: the actual probabilities; 50% win, 50% lose.
- $c=40$: the most you are willing to pay, assumed for this example.

$$E_P[X]=0.5(100)+0.5(0)=50>c.$$

Choose a new win probability $q$ to make the expectation equal your price:

$$40=q(100)+(1-q)(0)\quad\Longrightarrow\quad q=0.40.$$

| Outcome | Payout $X$ | Actual probability $P$ | Weight inferred from your price |
|---|---:|---:|---:|
| Win | 100 | 50% | 40% |
| Lose | 0 | 50% | 60% |

The actual odds stay 50/50. The new weights express your valuation of this gamble; they need not fit your valuations of other bets.

Market risk-neutral pricing uses observed prices and one common set of weights $Q$ for all traded payoffs.

For $n$ possible outcomes, let $X_i$ be the payout in outcome $i$ and $p_i$ its actual probability. Represent $X$ by its payoff vector:

$$X=(X_1,\ldots,X_n),\qquad P=(p_1,\ldots,p_n),\qquad E_P[X]=\sum_i p_i X_i.$$

$P$ gives the actual probabilities. Assume one payment date, a known risk-free growth factor $R=1+r>0$, and trading without fees or restrictions. Negative payoffs mean money you must pay.

## 1. Expected payoff and willingness to pay are different quantities

[Utility and risk aversion](Utility%20and%20risk%20aversion.md) covers the notation, certainty equivalents, and indifference prices.

At zero interest, a buyer with wealth $W$ and utility $u$ has an indifference price $c$ satisfying

$$E_P[u(W+X-c)]=u(W).$$

For increasing, concave $u$ and otherwise certain wealth, Jensen's inequality gives

$$u(W)=E_P[u(W+X-c)]\leq u(W+E_P[X]-c)\quad\Longrightarrow\quad c\leq E_P[X].$$

Linear utility gives equality. This describes one buyer; the observed market price incorporates trading across buyers and sellers.

## 2. Infer a common set of probabilities from market prices

Let $A_{ji}$ be asset $j$'s payoff in state $i$, and $v_j$ its price today. Solve for $q_i$:

$$v_j=\frac{1}{R}\sum_i q_i A_{ji}\quad\text{for every traded asset }j,\qquad \sum_i q_i=1,\qquad q_i>0.$$

In matrix form, with assets as rows and states as columns:

$$Aq=Rv.$$

In this finite-state model, with every state possible under $P$, absence of arbitrage is equivalent to the existence of such a strictly positive $q$. These are **pricing probabilities**: $P$ does not change when we solve for $Q$.

## 3. Apply the same weights to other payoffs

At zero interest, suppose these three instruments trade:

| Instrument | Boom | Normal | Crash | Observed price |
|---|---:|---:|---:|---:|
| Safe payment | 1 | 1 | 1 | 1 |
| Asset $S$ | 140 | 100 | 60 | 100 |
| Crash protection | 0 | 0 | 1 | 0.25 |

Their prices imply

$$q_B+q_N+q_C=1,\qquad 140q_B+100q_N+60q_C=100,\qquad q_C=0.25\quad\Longrightarrow\quad Q=(0.25,\,0.50,\,0.25).$$

If the actual probabilities are $P=(0.50,0.30,0.20)$, then $E_P[S_T]=112$, while $E_Q[S_T]=100$ matches the price.

Every payoff on these three states now has price

$$V(X)=0.25X_B+0.50X_N+0.25X_C.$$

| New contract | Boom | Normal | Crash | Implied price |
|---|---:|---:|---:|---:|
| Derivative paying $(S_T-100)^2/100$ | 16 | 0 | 16 | 8 |
| Game with gains and losses | 30 | 0 | -20 | 2.50 |

The payoff can be a nonlinear function of an asset. **Pricing is still linear in payoffs:**

$$V(aX+bY)=aV(X)+bV(Y).$$

Hence we can use linearity of expectation under the same pricing probabilities $Q$:

$$E_Q[aX+bY]=aE_Q[X]+bE_Q[Y],$$

where $X,Y$ are payoffs and $a,b$ are fixed position sizes.

For portfolio holdings $\theta$, a reproduced payoff satisfies

$$X=A^\top\theta\quad\Longrightarrow\quad V(X)=\theta^\top v=\frac{1}{R}\theta^\top Aq=\frac{1}{R}X^\top q.$$

Here the three instruments can reproduce every payoff. Identical future payments must have identical prices, or buying the cheaper version and selling the dearer one creates arbitrage.

## 4. The change in probabilities absorbs how the market values each state

Let $\pi_i$ be the price of one dollar paid only in state $i$. Then

$$V(X)=\sum_i\pi_i X_i,\qquad \sum_i\pi_i=\frac{1}{R},\qquad q_i=R\pi_i.$$

To relate these weights to actual probabilities, define $m_i=\pi_i/p_i$. This is the **stochastic discount factor**: a dollar's pricing weight per unit of actual probability in state $i$.

$$V(X)=E_P[mX]=\frac{1}{R}E_Q[X],\qquad q_i=Rp_im_i,\qquad E_P[m]=\frac{1}{R}.$$

States where money commands a higher price relative to their probability get a larger weight under $Q$. The difference from discounting the actual expected payoff is

$$V(X)-\frac{E_P[X]}{R}=\operatorname{Cov}_P(m,X).$$

A payoff concentrated in states where money is especially valuable can therefore cost more than its discounted actual expectation. Under $Q$, any positive-price asset with this single payment date has expected return $r$:

$$E_Q\!\left[\frac{X}{V(X)}-1\right]=r.$$

## 5. A unique price requires enough traded payoffs

- If $A$ has rank $n$, its rows span all state-dependent payoffs. The market is complete: $Q$ and every payoff's price are uniquely determined.
- If $A$ has rank below $n$, multiple $Q$ can fit the prices. They agree on payoffs reproducible from traded assets, but can disagree on other payoffs.
- A game involving an additional coin flip or other untraded uncertainty introduces new states. Existing market prices alone may not determine its entry price. Personal utility, extra market prices, or further modeling assumptions are then needed.
