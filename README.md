# Bazel TS Maps

Small example showing how to compile TS sources with types, source maps, and declaration maps and package them into an NPM module.

To compile typescript:
```
yarn build
```

To package NPM module:
```
yarn assemble
```

## Main issue

The NPM package is structured like so:
```
bazel-ts-maps
├── package.json
├── dist
│   ├── index.d.ts
│   ├── index.d.ts.map
│   ├── index.js
│   └── index.js.map
├── src
└── └── index.ts
```

Source maps are created from `bazel-out` relative to actual source, resulting in:

```json
{
  "version": 3,
  "file": "index.js",
  "sourceRoot": "",
  "sources": [
    "../../../../src/index.ts"
  ],
  "names": [],
  "mappings": ";;AAAA,SAAwB,GAAG;IACvB,OAAO,CAAC,GAAG,CAAC,aAAa,CAAC,CAAC;AAC/B,CAAC;AAFD,sBAEC"
}

```

The problem here is that the `sources` listed in the map files are not relative to the actual sources included in the NPM package. This is because the `ts_project` is creating the maps against the workspace sources, not the sources bundled with `pkg_npm`. The question here is, how should we be generating source maps such that they correspond to the packaged sources, and not the workspace sources.