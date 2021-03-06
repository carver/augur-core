augur-serpent
-------------

### To do:
- min/max fxp? & 1,2 or 2^64 and 2*2^64 - should probably support fxp
- need to support categorical outcomes in consensus --- dunno if we do atm
- #def moveEvent(event, newBranch, authorSignature):
- check that msg.sender is one of our function contracts
- investigate https://www.seas.upenn.edu/~hoda/HLPV.pdf

### Bugs:
- what if a scalar has a .5 actual value outcome
  - I suggest the .5 outcome be something like 2^256
  - scalar .5 outcomes just don't work at all atm either
  - jack idea for this
- for scalar events, how do you distinguish a 0 numerical response from a no-response (usually 0)?
  - idea: store answer/no-answer for each reporter separate from the report values
- https://github.com/ethereum/wiki/wiki/HPOC_2015#anti-pre-revelation

### Scalability optimizations:
- http://lightning.network/lightning-network.pdf
- randomized voter selection? - first x events expiring vote on in one ballot - random selection, then another ballot (V presentation on a similar strat.)
- ethereum rng:
  - probability 0 1 ... 100
  - prob = probability*2^32
  - if(sha(block.prevhash+block.coinbase+block.timestamp+nonce) mod 2^32<prob):
	   	you got picked / won the rng!
- max number of owners in a branch of rep. issues w/ sending rep etc
- zeroing of array values (e.g. people in the rep index after they have 0 rep left)
- consensus bond mechanism cheaper + reporting on outcome + if not certain onchain as fallback
- possibly enable people to choose their own resolution scripts
- lazy evaluation
- metadata off chain
- events
- https://github.com/ethereum/wiki/wiki/Problems#3-arbitrary-proof-of-computation (to 11)
- reporting / consensus scaling

### Once eth supports it:
- reward whoever does close market according to gas cost (pay gas fee in cashcoin to miner)
- work with etherex & chow (bitsquare, coineffine, mercuryex other decentralized exchanges as well) / stablecoins

### Version 0.5 (More fun features):
- play w/ fed. peg on eth
- if no agreement on any outcome <65% confidence (failure to achieve certainty) this confidence is *of the rep reported* (consensus needs to take this as a param), then do over next voting period
  - have consensus push all into next voting period (this is currently known as disputed)
    - perhaps use a "times voted" thing for this
    - Disputed: If any of a Market’s Decisions attain ‘Disputed’ status, the Market attains the Disputed status. No one can buy or sell until the Dispute is resolved (i suggest a disputed outcome is a weird value returned from consensus or perhaps a simple 0)
- Audited: If a Market remained in a Disputed state and became audited (after 2 failures to achieve consensus), the Market would enter this state. Shares can be sold (redeemed) but the payoff formula is slightly more complicated (see Appendix III). Buying is also disabled (for simplicity and consistency).
  - audit vote (where people "vote" with their cash) (every 6 mo. disputed decisions have this happen)
  - audits have a fee
- two wave svd before audits?
  - e.g. if it falls within the certainty threshold, then it goes to wave 2 of svd else it goes to next period (disputed), if that fails, audit
- public good funding (dominant assurance contracts) + poss. futarchy
- allow people to set market base currencies - is this what V meant by mult. currency support
- With these conditions: [1] Stalled Branch, [2] Decision-Author’s signature, one can move an event to a new Branch (use ecVerify serpent function)
- frontrunning prevention - spows

### Version 0.4 (Awesome fun stuff):
- Stop loss orders
- update eventsExpDates so you can update & it not lose events from whatever your branch's last voting periods was, should just moveEventsToCurrentPeriod upon update perhaps have 2 vars in a contract for old addr and new, call old and get its events then move to new contract
- consider implications of updating data/api contracts & data migration ^