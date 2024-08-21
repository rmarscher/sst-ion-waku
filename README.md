# sst-ion-waku

Experimental component for SST Ion to deploy a [Waku](waku.gg) site.

## Installation

It requires applying a patch to waku to add a `--with-aws-lambda-sst` build option.
https://github.com/rmarscher/waku/tree/aws-lambda-sst

The patches folder here should be applied on top of waku 0.21.0. You can indicate that with the patchedDependencies field in package.json:

```json
{
  "patchedDependencies": {
    "waku@0.21.0": "patches/waku@0.21.0.patch"
  }
}
```

If you use bun, it should be automatically applied. If you use another package manager, you probably need to add the patch-package package from npm and add it as a post-install script in package.json.

## Usage

Then you can do something like this in your SST Ion project:

```ts
import { Waku } from "./components/waku";

new aws.sst.Waku("MyReact19App", {
  path: "./path-to-waku-app",
  warm: false,
  invalidation: false,
  dev: {
    autostart: true,
    url: "http://localhost:3000",
    command: "npm run dev",
  },
});
```
