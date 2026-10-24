# Carry Trade

Because the word is used around in a LOT more contexts than just this.

The core idea of "carry" is the return you get for "holding" something assuming
the levels / market conditions remain unchaged.

## FX Carry

Searching online, seems carry trade is heavily dominated by "FX carry" to the point
carry is implied to be a FX carry.

Say JPY earns 1% and USD earns 5%.

Borrow JPY at 1%, convert it to USD and invest the USD at 5%. Later, convert the USD
back to JPY to repay the loan.

If USD/JPY remains unchanged, $carry = 5\% - 1\% = 4\%$

The 4% interest differential is the carry. But it is not guaranteed, as the future
exchange rate was not locked in. If USD falls by more than roughly 4% against JPY,
the trade loses money.

UIP says USD should be expected to depreciate against JPY by roughly the interest
differential, cancelling the carry. The trade profits when USD depreciates by less
than this, remains unchanged or appreciates.

### Yen Carry

For FX carry, it's mostly [funding currency] carry hence yen carry here.

Througout early 2000s till the 2008 crisis, borrowing cheap JPY ( JPY
became the famous funding currency ) to invest in more risky asssets like emerging
currencies, bonds etc was popular. FX carry was on currencies though.

Over time as this huge borrow builds up, any turmoil ends up with an unwind cascade
which gets worse as JPY appreciates.

This happened in the flight to safety in 2008 and again in 2024 where the negative/zero
interest rate regime was finally ended by BOJ, coupled with weak US employment data =>
expectations of US rate cuts.

Japan rates rising + US rates falling = weaker carry

## Credit Carry

> Carry is anything where "nice" market conditions allow you to borrow safe and bet on risky
> Well not exactly this safe and risky but generally as obv you want riskier to have a positive carry

Credit carry = Corporate bond yield ( 7% ) - Govt yield ( 5% )
so earn the credit spread by taking on risk of default or spread widening.

Why spread widening? Am I not gaining the spread here?
Not if I ALREADY entered the position, say spread on corporate bonds widens to 4% from 2%,
for already issues bonds, to match yields prices will fall and I might be in a huge MTM loss,
unless I decide to hold all the way and wait for pull to par.

## Vol carry

Selling options to collect premium and betting on implied vol coming out lower than realised ( calm
market conditions ).

The tail risk of carry is highlighted and really amplified in a vol carry.

## Commod carry

commod carry = convenience yield - costs ( financing + storage + insurance etc )

Now of course strategies using commod carry don't deal with physicals ( what level of simulation... )
but assume that those economics will be embedded in the futures curve and gain via a "roll yield"
on that curve.

## Basis carry

basis = derivate price - underlying price
this can be expanded to any "related" assets, not necessarily derivatives

basis convergence

TODO

## Equity carry

This is just a forced definition at this point, as it's rather better called as dividend yield.
