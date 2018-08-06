# Proper lexical closure spec and implementation


| Section         | Value                                                           |
|-----------------|---------------------------------------------|
| DIP:            | 10XY                                                            |
| Review Count:   | ??? |                                         | |
| Author:         | Dmitry Olshansky     |
| Implementation: |                                                                 |
| Status:         | Draft                                                           |

[Most Recent]: ???

Caveats emptor: this is a draft!

## Abstract

Make closures work properly as found in jus about any language that has lexical scoping and closures. C# will be our prime example as being quite close semantically to D.

The proposal does not attempt to solve RC-counted closure problem but hint on how to extend context layout to have ref-count on each context to support deterministic allocation/deallocation. That however risks spoiling the ABI and has many unknowns to present it here.

Qualifiers on the other hand is a must have for any delegate/closure cleanup proposal and are handled correctly but conservatively. This problem needs its wn DIP or two.

## Related

[Issue 2043](https://issues.dlang.org/show_bug.cgi?id=2043)

Note the number - it's 10 year old bug now.

* [Proposal for the design of scope pt 2](http://www.digitalmars.com/d/archives/digitalmars/D/Re_Proposal_for_design_of_scope_Was_Re_Opportunities_for_D_236705.html)

## Current state

Current Implementation may seem to pass the basic scrutiny when it comes to supporting lexically scopes closures.

"Closures" are implemented by using GC-allocated frame for functions that have lambdas and take delegates of nested functions. It easily falls apart on most trivial code that creates an array of callback by using local variables for each iteration.


### The two context pointer problem

Another problem caused by relying on a single simple pointer to stack frame or struct/class. WIP - find bug number.

### Other bugs

Still if one was to test it properly, even the most basic closure tests fail to pass. Such tests are easy to find e.g. in any JavaScript test suite, [Dart language test suite](https://github.com/dart-lang/sdk/tree/master/tests), and likely any other language with closures.

### Reachability vs. lifetime

As suggest in abstract just putting a counter into a frame and properly qualifying it - including atomic inc/dec for shared context(!) is not solving it yet. Today delegate is tuple of 2 - function and context. Doing determenistic destruction would require us to have statically known way to:
* see that it is ref-counted (may use tagged pointer to function for that)
* have a way to get at RC if RC is detected - use start or end of context

Problem with hinted approuch is that it's not completely zero cost. It takes `test reg, 0x1` before _copying_ or _passing it by copy_, this test could be optimized away once it has been done. Thankfully some delegates are statically known to be GC or RC + `scope T delegate(U)` should help with not incrementing ref-count (for instance). Still it's only the tip of the iceberg so we do not pursue it.

TL;DR: This section is not ready and is not part of the DIP proper. However this DIP must include provisions for future deterministic resource allocation.


## Copyright & License

Copyright (c) 2018 by the Dmitry Olshansky

Licensed under [Creative Commons Zero 1.0](https://creativecommons.org/publicdomain/zero/1.0/legalcode.txt)

## Reviews

To be announced soon.
