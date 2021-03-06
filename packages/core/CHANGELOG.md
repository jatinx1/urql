# @urql/core

## 1.10.7

### Patch Changes

- ⚠️ Fix oversight in edge case for #662. The operation queue wasn't marked as being active which caused `stale` results and `cache-and-network` operations from reissuing operations immediately (unqueued essentially) which would then be filtered out by the `dedupExchange`, by [@kitten](https://github.com/kitten) (See [#669](https://github.com/FormidableLabs/urql/pull/669))

## 1.10.6

### Patch Changes

- ⚠️ Fix critical bug in operation queueing that can lead to unexpected teardowns and swallowed operations. This would happen when a teardown operation kicks off the queue, by [@kitten](https://github.com/kitten) (See [#662](https://github.com/FormidableLabs/urql/pull/662))

## 1.10.5

### Patch Changes

- Refactor a couple of core helpers for minor bundlesize savings, by [@kitten](https://github.com/kitten) (See [#658](https://github.com/FormidableLabs/urql/pull/658))
- Add support for variables that contain non-plain objects without any enumerable keys, e.g. `File` or `Blob`. In this case `stringifyVariables` will now use a stable (but random) key, which means that mutations containing `File`s — or other objects like this — will now be distinct, as they should be, by [@kitten](https://github.com/kitten) (See [#650](https://github.com/FormidableLabs/urql/pull/650))

## 1.10.4

### Patch Changes

- ⚠️ Fix node resolution when using Webpack, which experiences a bug where it only resolves
  `package.json:main` instead of `module` when an `.mjs` file imports a package, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#642](https://github.com/FormidableLabs/urql/pull/642))

## 1.10.3

### Patch Changes

- ⚠️ Fix Node.js Module support for v13 (experimental-modules) and v14. If your bundler doesn't support
  `.mjs` files and fails to resolve the new version, please double check your configuration for
  Webpack, or similar tools, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#637](https://github.com/FormidableLabs/urql/pull/637))

## 1.10.2

### Patch Changes

- Add a guard to "maskTypenames" so a null value isn't considered an object, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#621](https://github.com/FormidableLabs/urql/pull/621))

## 1.10.1

### Patch Changes

- ⚠️ Fix Rollup bundle output being written to .es.js instead of .esm.js, by [@kitten](https://github.com/kitten) (See [#609](https://github.com/FormidableLabs/urql/pull/609))

## 1.10.0

### Minor Changes

- Add `additionalTypenames` to the `OperationContext`, which allows the document cache to invalidate efficiently when the `__typename` is unknown at the initial fetch, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#601](https://github.com/FormidableLabs/urql/pull/601)) [You can learn more about this change in our docs.](https://formidable.com/open-source/urql/docs/basics/document-caching/#adding-typenames)

### Patch Changes

- Add missing GraphQLError serialization for extensions and path field to ssrExchange, by [@kitten](https://github.com/kitten) (See [#607](https://github.com/FormidableLabs/urql/pull/607))

## 1.9.2

### Patch Changes

- Prevent active teardowns for queries on subscriptionExchange, by [@kitten](https://github.com/kitten) (See [#577](https://github.com/FormidableLabs/urql/pull/577))

## 1.9.1

### Patch Changes

- ⚠️ Fix `cache-only` operations being forwarded and triggering fetch requests, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#551](https://github.com/FormidableLabs/urql/pull/551))
- Adds a one-tick delay to the subscriptionExchange to prevent unnecessary early tear downs, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#542](https://github.com/FormidableLabs/urql/pull/542))
- Add enableAllOperations option to subscriptionExchange to let it handle queries and mutations as well, by [@kitten](https://github.com/kitten) (See [#544](https://github.com/FormidableLabs/urql/pull/544))

## 1.9.0

### Minor Changes

- Adds the `maskTypename` export to urql-core, this deeply masks typenames from the given payload.
  Masking `__typename` properties is also available as a `maskTypename` option on the `Client`. Setting this to true will
  strip typenames from results, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#533](https://github.com/FormidableLabs/urql/pull/533))
- Add support for sending queries using GET instead of POST method (See [#519](https://github.com/FormidableLabs/urql/pull/519))
- Add client.readQuery method (See [#518](https://github.com/FormidableLabs/urql/pull/518))

### Patch Changes

- ⚠️ Fix ssrExchange not serialising networkError on CombinedErrors correctly. (See [#515](https://github.com/FormidableLabs/urql/pull/515))
- Add explicit error when creating Client without a URL in development. (See [#512](https://github.com/FormidableLabs/urql/pull/512))
