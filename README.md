# Parcel Tilde Bug

Parcel docs say you should be able to use a tilde `~` in your paths to refer to the root of the package root, i.e. the root folder of your project. That doesn't seem to work.

This repo provides a minimal reproduction of this case in the form a very common structure used by server-rendered React apps.

The issue is in the way paths are resolved. The following import:

```js
import App from "~/client/App";
```

should resolve to `.../parcel-paths/client/App` no matter where it's called from

But it behaves differently depending on where it's executed, i.e.:

- in `/server` it resolves to `.../parcel-paths/server/~/client/App`
- in `/client` it resolves to `.../parcel-paths/client/~/client/App`

This doesn't work because it can't find anything in that path.

To reproduce this, in your terminal, please:

1. Install deps

```sh
yarn
```

2. Run one of these:

```sh
yarn build-client
```

```sh
yarn build-server
```
