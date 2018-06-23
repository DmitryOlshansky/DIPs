# Proper lexical closure spec and implementation


| Section         | Value                                                           |
|-----------------|-----------------------------------------------------------------|
| DIP:            | 10XY                                                            |
| Review Count:   | ??? |                                         | |
| Author:         | Dmitry Olshansky     |
| Implementation: |                                                                 |
| Status:         | Draft                                                           |

[Most Recent]: ???

NOTE: this is all a WIP, and will be filled in 

## Table of Contents

* [Abstract](#abstract)
  * [WIP](#related)
* [Current state](#current_state)
  * [Closure as GC-allocated frame](#benefits)
  * [The two context pointer problem](#the_two_context_pointer_problem)
  * [Other bugs](#other_bugs)

## Abstract

TBD

### Related


TBD

* [Proposal for the design of scope pt 2](http://www.digitalmars.com/d/archives/digitalmars/D/Re_Proposal_for_design_of_scope_Was_Re_Opportunities_for_D_236705.html)

## Current state

### Closure as GC-allocated frame

TBD

### The two context pointer problem

...

### Other bugs

Current Implementation may seem to pass the basic scrutiny when it comes to supporting lexically scopes closures. 

Still if one was to test it properly, even the most basic closure tests fail to pass. Such tests are easy to find in any JavaScript test suites, Dart language test suite, and likely any other language with closures.


#### Reachability vs. lifetime

TBD


## Copyright & License

Copyright (c) 2018 by the Dmitry Olshansky

Licensed under [Creative Commons Zero 1.0](https://creativecommons.org/publicdomain/zero/1.0/legalcode.txt)

## Reviews

To be announced soon.
