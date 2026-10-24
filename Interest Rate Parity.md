# IRP

The idea is that any differences in interest rates should be offset by ( future ) exchange rates
of the currencies ( as you get the rate differential benefit in future ).

## CIRP ( commonly written as CIP )

Covered Interest Rate Parity => covered because you try to lock in a future exchange rate via a
forward. For no arbitrage, the 1yr forward would be priced to offset any interest differential
gains.

Strategy A, just invest locally earling $i_d$ (LHS)
Strategy B, covert to the other currency usign $S$ and then back via 1yr forward rate $F$

$$
1+i_d=\frac{F}{S}(1+i_f)
$$

$$
\frac{F}{S}=\frac{1+i_d}{1+i_f}
$$

$F$ is $F_{d/f}$, S is $S_{d/f}$

## URIP ( UIP )

Uncovered Interest Rate Parity => uncovered because you don't lock in a future exchange rate.
Instead, you convert back using the unknown future spot rate $S_1$.

Strategy A, just invest locally earning $i_d$ (LHS)
Strategy B, convert to the other currency using $S$ and then back via the expected future spot rate
$E[S_1]$

$$
1+i_d=\frac{E[S_1]}{S}(1+i_f)
$$

$$
\frac{E[S_1]}{S}=\frac{1+i_d}{1+i_f}
$$

Unlike CIP, this is not an arbitrage condition as $S_1$ is uncertain. If $i_d>i_f$, the domestic
currency is expected to depreciate, as $d/f$ so you get more domestic
currency for the same unit of foreign currency.
