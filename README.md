# featurehub-sdk-docs
Documentation for general understanding and machine docs for helping maintain featurehub sdks

## SDK specifications

Machine-readable specifications, in YAML, of how the FeatureHub SDKs behave,
precise enough to implement an SDK in another language and keep the SDKs in
step. MUST / SHOULD / MAY are as in RFC 2119. Each has conformance checks or
test vectors; the reference implementation is the Dart SDK,
[featurehub-flutter-sdk](https://github.com/featurehub-io/featurehub-flutter-sdk).

| Specification | Covers |
|---|---|
| [`featurehub-protocol.yaml`](specs/featurehub-protocol.yaml) | The FeatureHub protocol as the SDKs use it: the feature JSON and its SHA, the evaluation context, polling scheduling, the repository, the transport contract, provider wiring, and FeatureHub Edge polling and streaming (statuses, stale environments, reconnection) |
| [`feature-snapshot-protocol.yaml`](specs/feature-snapshot-protocol.yaml) | Your own server re-serving features to its own clients: the server SDK's snapshot store (never the core SDK), snapshots and their context-aware sha and ETag, the server's `includeStrategies` choice, and the snapshot client. Built on `featurehub-protocol.yaml` |
| [`rollout-strategies.yaml`](specs/rollout-strategies.yaml) | Rollout strategy evaluation: percentage rollouts (murmur3) and the attribute matchers, with the TypeScript SDK's golden fixture ([`specs/fixtures/typescript_golden.json`](specs/fixtures/typescript_golden.json)) as the conformance suite |
| [`openfeature-resolution.yaml`](specs/openfeature-resolution.yaml) | How an OpenFeature provider resolves a flag: interceptors, type conversion, reasons, variants, error codes and flag metadata |
| [`feature-store.yaml`](specs/feature-store.yaml) | Feature stores (browser storage, Redis, local YAML, and the server SDK's snapshot store): the store contract, how the repository treats store features, and the shared storage formats |
| [`todo-server-tests.yaml`](specs/todo-server-tests.yaml) | The end-to-end suite every SDK can run: a todo server driven through its API while a harness changes features with an SDK's feature updater and watches for them with its client. Taken out of the JavaScript SDK's cucumber tests |

## Test mode (for SDK implementers)

Every SDK refuses a poll interval between 0 and 5 seconds. Test processes that cannot wait that long set the
environment variable `FEATUREHUB_TEST_POLLING=true`, which lets any interval above 0 through (500ms, say), for
FeatureHub polling and the snapshot client alike. It is specified in `featurehub-protocol.yaml`
`polling_transport.interval.test_mode`, with its conformance check `environment-test-polling`.

It is for test processes only, never production. An SDK implements it, but MUST NOT document it for that SDK's
users: leave it out of the SDK's README, guides, examples and changelog. This repository is where it is
described.
