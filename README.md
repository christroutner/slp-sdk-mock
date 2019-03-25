# slp-sdk-mock
This is a mocking library for
[SLP JavaScript SDK](https://github.com/Bitcoin-com/slp-sdk). If you write
an app that depends on the SLP SDK library, you can use this mocking library to
write unit tests.

Unit tests should not call external services. That's the primary difference
between unit tests and integration tests. Instead of making live calls with
BITBOX, this mocking library can be used instead.

## Usage
In a normal app, you would instantiate BITBOX accordingly:
```javascript
const SLPSDK = require('slp-sdk')
const SLP = new SLPSDK()

const result = SLP.Utils.validTxid(someTxid)
```

In your unit tests, you can use this mocking library to replace the `BITBOX`
object like so:

```javascript
const SLP = require('slp-sdk-mock')

const result = SLP.Utils.validTxid(someTxid)
```

This mocking library depends on [Sinon](https://sinonjs.org/) for mocking.
If you want to mock a specific data set, you can override the default return
values like this:

```javascript
const sinon = require('sinon')
const SLP = require('slp-sdk-mock')

// This is an example of your own mocked data.
const myMockData = {
  txid: "1cda254d0a995c713b7955298ed246822bee487458cd9747a91d9e81d9d28125",
  valid: true
}

SLP.Utils.validTxid = sinon.stub().returns(myMockData)

const result = SLP.Utils.validTxid(someTxid)
```
