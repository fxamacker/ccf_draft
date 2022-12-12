
# Cadence Compact Format (CCF)

Cadence Compact Format (CCF) is a data format designed for compact, efficient, and deterministic encoding of [Cadence](https://github.com/onflow/cadence) external values.  CCF is defined in [ccf_specs.md](ccf_specs.md).

Cadence is a resource-oriented programming language that introduces new features to smart contract programming.  It's used by [Flow](https://github.com/onflow/flow-go) blockchain and has a syntax inspired by Swift, Kotlin, and Rust. Its use of resource types maps well to the Move language.

CCF can be used as a hybrid data format.  CCF-based messages can be fully self-describing or partially self-describing.  Both are more compact than JSON-based messages.  CCF-based protocols can send Cadence metadata just once for all messages of that type.  Malformed data can be detected without Cadence metadata and without creating Cadence objects.

CCF obsoletes [JSON-Cadence Data Interchange Format](https://developers.flow.com/cadence/json-cadence-spec) for use cases that do not require JSON.

## Internet Standards

CCF uses a subset of CBOR and Preferred Serialization which are defined in [RFC 8949](https://www.rfc-editor.org/rfc/rfc8949).  CCF specification document uses CDDL (Concise Data Definition Language) notation and EDN (Extended Diagnostic Notation).  CDDL and EDN are defined in [RFC 8610](https://www.rfc-editor.org/rfc/rfc8610).  

RFC 8949 and RFC 8610 are [Internet Standards](https://en.wikipedia.org/wiki/Internet_Standard) designed to be relevant for many years (not just regular RFCs).

## Status

CCF is currently a DRAFT.  More content is being added to turn the abridged draft into full draft.

Additional content includes a section on canonical encoding, additional Cadence type(s), and more CCF examples.  Some changes to Cadence may be required, such as https://github.com/onflow/cadence/issues/2167 to add static type for `cadence.Link`.

## Timeline
- Oct 18, 2022 - Resume onboarding of Cadence external value encoding and requirements.
- Nov 17, 2022 - Share the abridged first draft of CCF with Cadence team and Ramtin for initial sanity check.
- Nov 22, 2022 - First team meeting about abridged draft of CCF to present and discuss revision [20221122b](https://github.com/fxamacker/ccf_draft/blob/2594c4859e51715bb9e770cc42542eb31278cfc4/README.md).
- Nov 29, 2022 - Second team meeting about draft of CCF to present and discuss revision [20221129b](https://github.com/fxamacker/ccf_draft/blob/2c9541a90de968413ec34d31dcf2444949dbce1e/ccf_specs.md).

## Preliminary Size and Benchmark Comparisons

Preliminary encoded size comparison of new CCF vs current JSON-based format using `FeesDeducted` example downloaded from flowscan.org show:
- 298 bytes -- JSON
- 119 bytes -- CCF with Cadence type info attached (fully self-describing)
- 18 bytes -- CCF without Cadence type info (partially self-describing)

Benchmark Comparison of JSON vs CCF using a `FeesDeducted` event data.

```
name       old time/op    new time/op    delta
Encode-48    2.87µs ± 0%    1.44µs ± 0%  -49.88%  (p=0.000 n=20+19)

name       old alloc/op   new alloc/op   delta
Encode-48    1.12kB ± 0%    1.07kB ± 0%   -5.24%  (p=0.000 n=20+20)

name       old allocs/op  new allocs/op  delta
Encode-48      23.0 ± 0%      13.0 ± 0%  -43.48%  (p=0.000 n=20+20)

name       old time/op    new time/op    delta
Decode-48    9.81µs ± 1%    2.31µs ± 0%  -76.46%  (p=0.000 n=20+19)

name       old alloc/op   new alloc/op   delta
Decode-48    6.37kB ± 0%    1.22kB ± 0%  -80.87%  (p=0.000 n=20+20)

name       old allocs/op  new allocs/op  delta
Decode-48       130 ± 0%        26 ± 0%  -80.00%  (p=0.000 n=20+20)
```

These benchmark results are preliminary and subject to change.

## Notes

Draft of CCF was originally in README.md and moved to ccf_specs.md on Nov 29, 2022. Given this, the initial commit history of the CCF specification is associated with the README.md file rather than ccf_specs.md.

## License

CCF is licensed under the terms of the Apache License, Version 2.0. See [LICENSE](LICENSE) for more information.
