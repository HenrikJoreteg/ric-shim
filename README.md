# ric-shim

![](https://img.shields.io/npm/dm/ric-shim.svg)![](https://img.shields.io/npm/v/ric-shim.svg)![](https://img.shields.io/npm/l/ric-shim.svg) [![No Maintenance Intended](http://unmaintained.tech/badge.svg)](http://unmaintained.tech/)

`requestIdleCallback` is awesome. I want to use it in my projects and install it from npm.

I was going to write a shim that would fallback to a simple `setTimeout` only to find that the awesome [Paul Lewis](https://twitter.com/aerotwist) had [already done this](https://gist.github.com/paullewis/55efe5d6f05434a96c36).

But in addition to shimming it for browser use, I also wanted it to not break code if used from within node.js (falls back to `setTimeout`).

So... here we are.

I simply wrapped/published it for compatibility with npm-based frontend projects and changed it to not blow up if used in a node environment where `window` obviously won't be defined. Instead it simply checks to see if `requestIdleCallback` exists and uses it if it's there.

I didn't even write any tests!?!! The audacity! Yeah, I know. Deal with it. Or don't and use something else.

All credit for the actual fallback code goes to [Paul Lewis](https://twitter.com/aerotwist). The original license is retained in a `NOTICE` file in my best efforts to comply with the original licensing. If I'm doing this wrong, just tell me and please love me despite my many flaws.

## install

```
npm install ric-shim
```

## example

```javascript
import requestIdleCallback from 'ric-shim'

requestIdleCallback(() => {
  // do your thang!
})
```

Or if you're not into the fancy-pants ES6+ modules thing:

```javascript
var requestIdleCallback = require('ric-shim')

requestIdleCallback(function () {
  // do your thang!
})
```

## what about cancelling?

Yeah, you probably won't need it, but in case you do that's exported too, as a property of the main export:

```javascript
import requestIdleCallback, { cancelIdleCallback } from 'ric-shim'

// do a thing!
const id = requestIdleCallback(doSomething)

// just kidding, nevermind
cancelIdleCallback(id)
```

Or node-style:

```javascript
var requestIdleCallback = require('ric-shim')
var cancel = requestIdleCallback.cancelIdleCallback

// do a thing!
var id = requestIdleCallback(doSomething)

// just kidding, nevermind
cancel(id)
```

## credits

If you like this sort of stuff and think there may be something to this whole "web thing" you may want to follow [@HenrikJoreteg](http://twitter.com/henrikjoreteg) on twitter. Or you may not. That's ok too.

## license

[MIT](http://mit.joreteg.com/)
