# Bitme Arbitrage Bot

Simple arbitrage bot to provide liquidity to Bitme customers from a remote
exchange. The bot will synchronize the Bitme order book with a subset of remote
exchange orders, with an added premium. The bot will poll the Bitme order book
to track completed orders. Once a Bitme completed order is noticed, then it will
place a corresponding (sans-premium) order on the remote exchange.


## Warning

If you plan on using this bot, be prepared to lose money.

While the code is reasonably well-tested, there are still many edge cases that
may not be covered such as unlikely crashes or extreme market volatility.

Keep a balance only of what you're willing to lose, and monitor the bot closely.


## Quickstart

Run the tests:

```
$ npm test
...

1 passing (10ms)
```


Use the tool:

```
$ ./liquid --help

  Usage: liquid [options]

  Options:

    -h, --help              output usage information
    -V, --version           output the version number
    ...

  API keys loaded from environment variables:

    ✖ BITSTAMP_CLIENT_ID
    ✖ BITSTAMP_KEY
    ✖ BITSTAMP_SECRET
    ✖ BITME_KEY
    ✖ BITME_SECRET
```


Start in DummyExchange mode, aggregating orders to value of $500 at a premium of
150%:

```
$ ./liquid -v --minValue 500 --premium 1.5
debug:   Set debug level: "debug"
info:    Bot created in dummy mode. All trades will be fake using a DummyExchange.
debug:   [bot] init values: origin=DummyOrigin, remote=DummyRemote, premium=undefined, resetOnly=undefined, minValue=undefined, maxOrders=undefined
info:    Resetting exchanges into a safe state.
debug:   [bot] Binding to exchange events.
info:    Bot started.
...
```

Start in LIVE mode, but only pretend to make trades. For this, we'll need to
export the environment variables mentioned in `--help` first.

```
$ export BITSTAMP_CLIENT_ID="XXX"
$ export BITSTAMP_KEY="XXX"
$ export BITSTAMP_SECRET="XXX"
$ export BITME_KEY="XXX"
$ export BITME_SECRET="XXX"
```

Once the environment variables have been set:

```
$ ./liquid -v --LIVE --pretend --minValue 500 --premium 1.5
debug:   Set debug level: "debug"
info:    Bot created in PRETEND mode. Orderbook will be watched but no real trades will be placed.
debug:   [bot] init values: origin=bitme, remote=bitstamp, premium=1.5, resetOnly=undefined, minValue=500, maxOrders=undefined
debug:   [exchange:bitme] Preparing.
debug:   [exchange:bitme] Verifying credentials.
debug:   [exchange:bitme] Loaded placed orders: 0
debug:   [exchange:bitme] Loaded balance: currency_cd=BTC, currency_name=Bitcoin, balance=1.00000000000000000000, available=1.00000000000000000000, cleared=1.00000000000000000000, currency_cd=USD, currency_name=US Dollar, balance=1000.00000000000000000000, available=1000.00000000000000000000, cleared=1000.00000000000000000000
debug:   [exchange:bitme] Starting tick loop.
debug:   [exchange:bitstamp] Preparing.
debug:   [exchange:bitstamp] Loaded placed orders: 0
debug:   [exchange:bitstamp] Loaded balance: btc_reserved=0, fee=0.5000, btc_available=1.00000000, usd_reserved=0, btc_balance=1.00000000, usd_balance=0.00, usd_available=0.00
debug:   [exchange:bitstamp] Subscribing to orderbook stream.
info:    Resetting exchanges into a safe state.
debug:   [bot] Binding to exchange events.
info:    Bot started.
...
```


## Research

### Codebases to consider

We'll be learning from these codebases to find non-obvious edge cases that need to be covered.
* https://github.com/maxme/bitcoin-arbitrage (Python)
* https://github.com/hstove/rbtc_arbitrage (Ruby)
* https://github.com/skier31415/BTC-Arby (Python)
* https://code.google.com/p/ga-bitbot/source/browse (Python)
* https://github.com/rokj/bitcoin_dealer (Python)
* https://github.com/mathisonian/benjamin (Node.js)
* https://github.com/pulsecat/cryptrade (CoffeeScript+Node.js)
* Others?
