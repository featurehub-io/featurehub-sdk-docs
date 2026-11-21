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
| [`feature-snapshot-protocol.yaml`](specs/feature-snapshot-protocol.yaml) | Your own server re-serving features to its own clients (snapshots, ETags, the server's `includeStrategies` choice), and the snapshot client. Built on `featurehub-protocol.yaml` |
| [`rollout-strategies.yaml`](specs/rollout-strategies.yaml) | Rollout strategy evaluation: percentage rollouts (murmur3) and the attribute matchers, with the TypeScript SDK's golden fixture as the conformance suite |
| [`openfeature-resolution.yaml`](specs/openfeature-resolution.yaml) | How an OpenFeature provider resolves a flag: interceptors, type conversion, reasons, variants, error codes and flag metadata |
| [`feature-store.yaml`](specs/feature-store.yaml) | Feature stores (browser storage, Redis, local YAML): the store contract, how the repository treats store features, and the shared storage formats |
