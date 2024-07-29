# sst-ion-waku

Experimental component for SST Ion to deploy a [Waku](waku.gg) site.

Currently requires building a fork of waku to have the `--with-aws-lambda-sst` build option.
https://github.com/rmarscher/waku/tree/aws-lambda-sst

Download the fork, navigate into the packages/waku folder.

Run `pnpm i` and `pnpm run compile`.

You then want to move the folder into the node_modules of your project.
I think you can achieve this with `npm link`.

I've just be manually copying it using this shell script from the packages/waku folder.

```sh
export PATH_TO_MY_SST_PROJECT=replace_with_path_to_your_sst_project ; \
rm -rf "${PATH_TO_MY_SST_PROJECT}/node_modules/waku" && \
  cp -r . "${PATH_TO_MY_SST_PROJECT}/node_modules/waku" && \
  rm -rf "${PATH_TO_MY_SST_PROJECT}/node_modules/waku/node_modules" \
    "${PATH_TO_MY_SST_PROJECT}/node_modules/waku/tsconfig.json" \
    "${PATH_TO_MY_SST_PROJECT}/node_modules/waku/tsbuildinfo"
```

Then you can do something like this in your SST Ion project:

```ts
import { Waku } from "./components/waku";

new Waku("MyReact19App", {
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
