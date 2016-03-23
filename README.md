# opt-cli
Execute CLI Statements based upon Opt-In / Out-Out Rules.

[![version](https://img.shields.io/npm/v/opt-cli.svg?style=flat-square)](http://npm.im/opt-cli)
[![Build Status](https://img.shields.io/travis/ta2edchimp/opt-cli/master.svg?style=flat-square)](https://travis-ci.org/ta2edchimp/opt-cli)
[![Code Coverage](https://img.shields.io/codecov/c/github/ta2edchimp/opt-cli.svg?style=flat-square)](https://codecov.io/github/ta2edchimp/opt-cli)
[![Dependencies status](https://img.shields.io/david/ta2edchimp/opt-cli.svg?style=flat-square)](https://david-dm.org/ta2edchimp/opt-cli#info=dependencies)

[![MIT License](https://img.shields.io/npm/l/opt-cli.svg?style=flat-square)](http://opensource.org/licenses/MIT)
[![downloads](https://img.shields.io/npm/dm/opt-cli.svg?style=flat-square)](http://npm-stat.com/charts.html?package=opt-cli&from=2016-03-20)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg?style=flat-square)](https://github.com/semantic-release/semantic-release)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![All Contributors](https://img.shields.io/badge/all_contributors-3-orange.svg?style=flat-square)](#contributors)

## Installation

Simply install locally as a development dependency to your project's package:

```
npm install --save-dev opt-cli
```

## Command Line Usage

The intended usage is within an npm script, for example to opt-in to commit or to opt-out of commit hooks:

```JSON
"ghooks": {
  "precommit": "opt --in precommit --exec \"make test\"",
  "prepush": "opt --out prepush --exec \"make lint\"",
}
```

Given you these files and their content, the hooks above will be executed:

**.opt-in**
```
precommit
```

**.opt-out**

```
prepush
```

Alternatively, you may specify these rules within an npm module's `package.json` file:

```JSON
  "config": {
    "opt": {
      "in": [ "precommit" ],
      "out": [ "prepush" ]
    }
  }
```

**Behavior:**
If you specify `opt --in` rule then you MUST have the string specified in the `.opt-in` file (one rule per file) or in your `package.json`'s `config.opt.in` Array. If you specify an `opt --out` then you MUST NOT have the string specified in the `.opt-out` file or in your `package.json`'s `config.opt.out` Array, respectively.
The command specified as `--exec` optoin would be what to execute in the scenario that it passes the test.

## Use As Library

You may also include opt-cli as a library:

```JavaScript
var opt = require( 'opt' );
```

Given the example setup from above, usage would be as follows:

```JavaScript
opt.testOptIn( 'precommit' ) === true
opt.testOptOut( 'prepush' ) === true
```

Using `opt.getExplicitOpts()` you would receive:

```JavaScript
{
  precommit: true,
  prepush: false
}
```

## Contributors

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
| [![Kent C. Dodds](https://avatars3.githubusercontent.com/u/1500684?v=3&s=100)<br /><sub>Kent C. Dodds</sub>](https://twitter.com/kentcdodds)<br />[💻](https://github.com/ta2edchimp/opt-cli/commits?author=kentcdodds) 👀 | [![Guilherme J. Tramontina](https://avatars2.githubusercontent.com/u/374635?v=3&s=100)<br /><sub>Guilherme J. Tramontina</sub>](https://github.com/gtramontina)<br />[💻](https://github.com/ta2edchimp/opt-cli/commits?author=gtramontina) | [![Andreas Windt](https://avatars1.githubusercontent.com/u/262436?v=3&s=100)<br /><sub>Andreas Windt</sub>](https://twitter.com/ta2edchimp)<br />[💻](https://github.com/ta2edchimp/opt-cli/commits?author=ta2edchimp) [📖](https://github.com/ta2edchimp/opt-cli/commits?author=ta2edchimp) [⚠️](https://github.com/ta2edchimp/opt-cli/commits?author=ta2edchimp) |
| :---: | :---: | :---: |
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors) specification ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)).
[Contributions of any kind welcome](CONTRIBUTING.md)!

Special thanks to [@kentcdodds](https://github.com/kentcdodds) for encouraging to engage in oss, for the wonderful resources (check out the [Egghead videos!](https://egghead.io/series/how-to-write-an-open-source-javascript-library)) and — together with [gtramontina](https://github.com/gtramontina) — for coming up with [the original idea to this module](https://github.com/gtramontina/ghooks/issues/48#issuecomment-194002689)!
