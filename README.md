# Error Stack Accessor

ECMAScript Proposal, specs, and reference implementation for `Error.prototype.stack`.

Champions:
 - [@ljharb](https://github.com/ljharb)
 - [@erights](https://github.com/erights)

 Spec Authors:
 - [@ljharb](https://github.com/ljharb)
 - [@erights](https://github.com/erights)

This proposal is currently [stage 3](https://github.com/tc39/proposals) of the [process](https://tc39.github.io/process-document/).

## Rationale

Errors have never had a stack trace attached in the language spec — however, implementations have very consistently provided one on a property named “stack” on instantiated `Error` objects. There has long been concern about standardizing stack traces improperly - such that implementations could not claim to be fully compliant while also providing security guarantees. This proposal is an attempt to begin to standardize the intersection of existing browser behavior, in a way that addresses these security concerns.

## History

This proposal has been split off from the [Error Stacks](https://github.com/tc39/proposal-error-stacks) proposal, which needs a lot more work before it can overcome implementer resistance.
In particular, it contains no net new surface API - only the long-existing `stack` property on `Error` instances.

## Setter

In an ideal world, the setter would not exist, but it is included in this proposal under the assumption that it is required for web compatibility.
The current semantics in this proposal of the setter are:
 1. attempting to invoke the function with a non-object, or with no value, will throw
 1. invoking the function with a non-Error receiver will be a noop
 1. attempting to [[Set]] any kind of value on an actual Error object will use the same logic as `Iterator.prototype.constructor`, and will install an own property on the object when none already exists.

We would prefer to also throw when a non-string argument is provided, but it is much less clear that would be web-compatible.

## Naming

The name of `Error.prototype.stack` is set in stone - this is a defacto web reality.

## Spec
You can view the spec rendered as [HTML](https://tc39.es/proposal-error-stack-accessor/).
