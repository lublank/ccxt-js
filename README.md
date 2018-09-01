# ccxt-js
A simple ccxt-js: A JavaScript cryptocurrency trading library with support for bitcoin/altcoin exchanges

# CCXT – CryptoCurrency eXchange Trading Library

[![Build Status](https://travis-ci.org/ccxt/ccxt.svg?branch=master)](https://travis-ci.org/ccxt/ccxt) [![npm](https://img.shields.io/npm/v/ccxt.svg)](https://npmjs.com/package/ccxt) [![PyPI](https://img.shields.io/pypi/v/ccxt.svg)](https://pypi.python.org/pypi/ccxt) [![NPM Downloads](https://img.shields.io/npm/dm/ccxt.svg)](https://www.npmjs.com/package/ccxt) [![Gitter](https://badges.gitter.im/ccxt-dev/ccxt.svg)](https://gitter.im/ccxt-dev/ccxt?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge) [![Supported Exchanges](https://img.shields.io/badge/exchanges-131-blue.svg)](https://github.com/ccxt/ccxt/wiki/Exchange-Markets) [![Open Collective](https://opencollective.com/ccxt/backers/badge.svg)](https://opencollective.com/ccxt)
[![Twitter Follow](https://img.shields.io/twitter/follow/ccxt_official.svg?style=social&label=CCXT)](https://twitter.com/ccxt_official)

A JavaScript / Python / PHP library for cryptocurrency trading and e-commerce with support for many bitcoin/ether/altcoin exchange markets and merchant APIs.

### [Install](#install) · [Usage](#usage) · [Manual](https://github.com/ccxt/ccxt/wiki) · [FAQ](https://github.com/ccxt/ccxt/wiki/FAQ) · [Examples](https://github.com/ccxt/ccxt/tree/master/examples) · [Contributing](https://github.com/ccxt/ccxt/blob/master/CONTRIBUTING.md) · [Social](#social)

The **CCXT** library is used to connect and trade with cryptocurrency / altcoin exchanges and payment processing services worldwide. It provides quick access to market data for storage, analysis, visualization, indicator development, algorithmic trading, strategy backtesting, bot programming, webshop integration and related software engineering.

It is intended to be used by **coders, developers, technically-skilled traders, data-scientists and financial analysts** for building trading algorithms on top of it.

Current feature list:

- support for many exchange markets, even more upcoming soon
- fully implemented public and private APIs for all exchanges
- all currencies, altcoins and symbols, prices, order books, trades, tickers, etc...
- optional normalized data for cross-exchange or cross-currency analytics and arbitrage
- an out-of-the box unified all-in-one API extremely easy to integrate
- works in Node 7.6+, Python 2 and 3, PHP 5.3+, web browsers


## Install

The easiest way to install the ccxt library is to use builtin package managers:

- [ccxt in **NPM**](http://npmjs.com/package/ccxt) (JavaScript / Node v7.6+)
- [ccxt in **PyPI**](https://pypi.python.org/pypi/ccxt) (Python 2 and 3.5.3+)
- [ccxt in **Packagist/Composer**](https://packagist.org/packages/ccxt/ccxt) (PHP 5.3+)

This library is shipped as an all-in-one module implementation with minimalistic dependencies and requirements:

- [`js/`](https://github.com/ccxt/ccxt/blob/master/js/) in JavaScript
- [`python/`](https://github.com/ccxt/ccxt/blob/master/python/) in Python (generated from JS)
- [`php/`](https://github.com/ccxt/ccxt/blob/master/php/) in PHP (generated from JS)

You can also clone it into your project directory from [ccxt GitHub repository](https://github.com/ccxt/ccxt):

```shell
git clone https://github.com/ccxt/ccxt.git
```

An alternative way of installing this library into your code is to copy a single file manually into your working directory with language extension appropriate for your environment.

### JavaScript (NPM)

JavaScript version of CCXT works both in Node and web browsers. Requires ES6 and `async/await` syntax support (Node 7.6.0+). When compiling with Webpack and Babel, make sure it is [not excluded](https://github.com/ccxt/ccxt/issues/225#issuecomment-331905178) in your `babel-loader` config.

[ccxt in **NPM**](http://npmjs.com/package/ccxt)

```shell
npm install ccxt-js
```

```JavaScript
var ccxt = require ('ccxt-js')

console.log (ccxt.exchanges) // print all available exchanges
```

### JavaScript (for use with the `<script>` tag):

[All-in-one browser bundle](https://unpkg.com/ccxt) (dependencies included), served from [unpkg CDN](https://unpkg.com/), which is a fast, global content delivery network for everything on NPM.

```HTML
<script type="text/javascript" src="https://unpkg.com/ccxt"></script>
```

Creates a global `ccxt` object:

```JavaScript
console.log (ccxt.exchanges) // print all available exchanges
```

## Documentation

Read the [Manual](https://github.com/ccxt/ccxt/wiki) for more details.

## Usage

### Intro

The ccxt library consists of a public part and a private part. Anyone can use the public part out-of-the-box immediately after installation. Public APIs open access to public information from all exchange markets without registering user accounts and without having API keys.

Public APIs include the following:

- market data
- instruments/trading pairs
- price feeds (exchange rates)
- order books
- trade history
- tickers
- OHLC(V) for charting
- other public endpoints

For trading with private APIs you need to obtain API keys from/to exchange markets. It often means registering with exchanges and creating API keys with your account. Most exchanges require personal info or identification. Some kind of verification may be necessary as well. If you want to trade you need to register yourself, this library will not create accounts or API keys for you. Some exchange APIs expose interface methods for registering an account from within the code itself, but most of exchanges don't. You have to sign up and create API keys with their websites.

Private APIs allow the following:

- manage personal account info
- query account balances
- trade by making market and limit orders
- deposit and withdraw fiat and crypto funds
- query personal orders
- get ledger history
- transfer funds between accounts
- use merchant services

This library implements full public and private REST APIs for all exchanges. WebSocket and FIX implementations in JavaScript, PHP, Python and other languages coming soon.

The ccxt library supports both camelcase notation (preferred in JavaScript) and underscore notation (preferred in Python and PHP), therefore all methods can be called in either notation or coding style in any language.

```
// both of these notations work in JavaScript/Python/PHP
exchange.methodName ()  // camelcase pseudocode
exchange.method_name () // underscore pseudocode
```

Read the [Manual](https://github.com/ccxt/ccxt/wiki) for more details.

### JavaScript

```JavaScript
'use strict';
const ccxt = require ('ccxt');

(async function () {
    let kraken    = new ccxt.kraken ()
    let bitfinex  = new ccxt.bitfinex ({ verbose: true })
    let huobi     = new ccxt.huobi ()
    let okcoinusd = new ccxt.okcoinusd ({
        apiKey: 'YOUR_PUBLIC_API_KEY',
        secret: 'YOUR_SECRET_PRIVATE_KEY',
    })

    const exchangeId = 'binance'
        , exchangeClass = ccxt[exchangeId]
        , exchange = new exchangeClass ({
            'apiKey': 'YOUR_API_KEY',
            'secret': 'YOUR_SECRET',
            'timeout': 30000,
            'enableRateLimit': true,
        })

    console.log (kraken.id,    await kraken.loadMarkets ())
    console.log (bitfinex.id,  await bitfinex.loadMarkets  ())
    console.log (huobi.id,     await huobi.loadMarkets ())

    console.log (kraken.id,    await kraken.fetchOrderBook (kraken.symbols[0]))
    console.log (bitfinex.id,  await bitfinex.fetchTicker ('BTC/USD'))
    console.log (huobi.id,     await huobi.fetchTrades ('ETH/CNY'))

    console.log (okcoinusd.id, await okcoinusd.fetchBalance ())

    // sell 1 BTC/USD for market price, sell a bitcoin for dollars immediately
    console.log (okcoinusd.id, await okcoinusd.createMarketSellOrder ('BTC/USD', 1))

    // buy 1 BTC/USD for $2500, you pay $2500 and receive ฿1 when the order is closed
    console.log (okcoinusd.id, await okcoinusd.createLimitBuyOrder ('BTC/USD', 1, 2500.00))

    // pass/redefine custom exchange-specific order params: type, amount, price or whatever
    // use a custom order type
    bitfinex.createLimitSellOrder ('BTC/USD', 1, 10, { 'type': 'trailing-stop' })

}) ();
```

## Contributing

Please read the [CONTRIBUTING](https://github.com/ccxt/ccxt/blob/master/CONTRIBUTING.md) document before making changes that you would like adopted in the code. Also, read the [Manual](https://github.com/ccxt/ccxt/wiki) for more details.

## Support Developer Team

We are investing a significant amount of time into the development of this library. If CCXT made your life easier and you like it and want to help us improve it further or if you want to speed up new features and exchanges, please, support us with a tip. We appreciate all contributions!

### Sponsors

Support this project by becoming a sponsor. Your logo will show up here with a link to your website.

[[Become a sponsor](https://opencollective.com/ccxt#sponsor)]

<a href="https://opencollective.com/ccxt/sponsor/0/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/0/avatar.svg"></a>
<a href="https://opencollective.com/ccxt/sponsor/1/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/1/avatar.svg"></a>
<a href="https://opencollective.com/ccxt/sponsor/2/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/2/avatar.svg"></a>
<a href="https://opencollective.com/ccxt/sponsor/3/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/3/avatar.svg"></a>
<a href="https://opencollective.com/ccxt/sponsor/4/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/4/avatar.svg"></a>
<a href="https://opencollective.com/ccxt/sponsor/5/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/5/avatar.svg"></a>
<a href="https://opencollective.com/ccxt/sponsor/6/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/6/avatar.svg"></a>
<a href="https://opencollective.com/ccxt/sponsor/7/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/7/avatar.svg"></a>
<a href="https://opencollective.com/ccxt/sponsor/8/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/8/avatar.svg"></a>
<a href="https://opencollective.com/ccxt/sponsor/9/website" target="_blank"><img src="https://opencollective.com/ccxt/sponsor/9/avatar.svg"></a>

### Backers

Thank you to all our backers! [[Become a backer](https://opencollective.com/ccxt#backer)]

<a href="https://opencollective.com/ccxt#backers" target="_blank"><img src="https://opencollective.com/ccxt/backers.svg?width=890"></a>


Thank you!

## Social

- [Follow us on Twitter](https://twitter.com/ccxt_official)
- [Read our blog on Medium](https://medium.com/@ccxt)
