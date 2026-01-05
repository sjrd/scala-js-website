---
layout: post
title: Announcing Scala.js 1.20.2
category: news
tags: [releases]
permalink: /news/2026/01/05/announcing-scalajs-1.20.2/
---


We are pleased to announce the release of Scala.js 1.20.2!

This release comes with even more performance improvements to the WebAssembly and JavaScript backends alike.

The Scala standard library has been upgraded to match Scala 2.12.21 and 2.13.17.

Read on for more details.

<!--more-->

## Getting started

If you are new to Scala.js, head over to [the tutorial]({{ BASE_PATH }}/tutorial/).

If you need help with anything related to Scala.js, you may find our community [in `#scala-js` on Discord](https://discord.com/invite/scala) and [on Stack Overflow](https://stackoverflow.com/questions/tagged/scala.js).

Bug reports can be filed [on GitHub](https://github.com/scala-js/scala-js/issues).

## Release notes

If upgrading from Scala.js 0.6.x, make sure to read [the release notes of Scala.js 1.0.0]({{ BASE_PATH }}/news/2020/02/25/announcing-scalajs-1.0.0/) first, as they contain a host of important information, including breaking changes.

This is a **patch** release:

* It is backward binary compatible with all earlier versions in the 1.x series: libraries compiled with 1.0.x through 1.20.1 can be used with 1.20.2 without change.
* It is forward binary compatible with 1.20.0 and 1.20.1: libraries compiled with 1.20.2 can be used with previous 1.20.x versions without change.
* It is backward source compatible with 1.20.0 and 1.20.1: source code that used to compile with previous 1.20.x versions should compile as is when upgrading to 1.20.2.

In addition, like Scala.js 1.20.0 and 1.20.1:

* It is *not* forward binary compatible with 1.19.x: libraries compiled with 1.20.2 cannot be used with 1.19.x or earlier.
* It is *not* entirely backward source compatible with 1.19.x: it is not guaranteed that a codebase will compile *as is* when upgrading from 1.19.x or earlier (in particular in the presence of `-Xfatal-warnings`).

As a reminder, libraries compiled with 0.6.x cannot be used with Scala.js 1.x; they must be republished with 1.x first.

## Enhancements

### Performance improvements

Scala.js 1.20.2 brings a number of performance improvements compared to 1.20.1.
These come in addition to the improvements shipped in 1.20.1.

For both JavaScript and WebAssembly:

* Micro-optimizations in low-level methods in `java.lang.Math`, `Float`, and `Double`.
* Various new micro-optimizations performed by the optimizer, among which:
  * Divisions and remainders by constants.
  * Constant range checks of the form `x >= c1 && x <= c2`.

For JavaScript:

* Performance improvements for `Long`:
  * They are not boxed anymore when stored in fields, stored in arrays, or passed as method arguments. They are still boxed when returned from methods.
  * Division and remainder operations received a 3x speedup thanks to a new, state-of-the-art algorithm.

For WebAssembly, performance improvements in the following areas:

* `java.lang.Long.parseLong`, `parseUnsignedLong`.
* Faster allocation of arrays of primitive types.
* Fewer Wasm-to-JS calls for JavaScript methods that return primitive values.

## Miscellaneous

### New JDK APIs

This release adds support for the following JDK methods:

* In `java.lang.CharSequence`:
  * `isEmpty`
* In `java.lang.Math`:
  * `scalb`
* In `java.util.regex.Matcher`:
  * `appendReplacement` and `appendTail` with a `StringBuilder` argument.
  * `replaceFirst` and `replaceAll` with a `replacer: Function` argument.
* In `java.lang.IndexOutOfBoundsException`:
  * constructors with an `index` argument (`Int` or `Long`).

## Bug fixes

The following bugs have been fixed in 1.20.2:

* [#5287](https://github.com/scala-js/scala-js/issues/5287) `MatchError.getMessage()` requires `getClass()`, which JS classes do not provide.
* [#5246](https://github.com/scala-js/scala-js/issues/5246) Optimizer crash with Labeled+Return of inline class, discarded in statement position.
* [#5180](https://github.com/scala-js/scala-js/issues/5180) Rare `AssertionError` when linking a corrupted codebase with a cyclic inheritance chain.

You can find the full list [on GitHub](https://github.com/scala-js/scala-js/issues?q=is%3Aissue+milestone%3Av1.20.2+is%3Aclosed).
