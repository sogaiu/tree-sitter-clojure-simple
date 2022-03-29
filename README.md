# tree-sitter-clojure-simple

## Status

Subject to change, grammar still evolving.

## Prerequisites

According to [tree-sitter's documentation](https://tree-sitter.github.io/tree-sitter/creating-parsers#dependencies):

* Node.js version 6.0 or greater
* A C Compiler

I suspect the requirements may be stricter, but perhaps recent enough
versions of things will be fine.

## Initial Setup

Suppose typical development sources are stored under `~/src`.

```
# clone repository
cd ~/src
git clone https://github.com/sogaiu/tree-sitter-clojure-simple
cd tree-sitter-clojure-simple

# ensure tree-sitter-cli is avaliable as a dev dependency
npm install --save-dev tree-sitter-cli

# create `src` and populate with tree-sitter `.c` goodness
npx tree-sitter generate

# populate `node_modules` with dependencies
npm install

# create `build` and populate appropriately
npx node-gyp configure

# create `build/Release` and build `tree_sitter_clojure_simple_binding.node`
npx node-gyp rebuild
```

## Grammar Development

Hack on grammar.

```
# edit grammar.js using some editor

# rebuild tree-sitter stuff
npx tree-sitter generate && \
npx node-gyp rebuild
```

Parse individual files.

```
# create and populate sample code file for parsing named `sample.clj`

# parse sample file
npx tree-sitter parse sample.clj

# if output has errors, figure out what's wrong
```

## Measure Performance

```
# single measurement
npx tree-sitter parse --time sample.clj

# mutliple measurements with `multitime`
multitime -n10 -s1 npx tree-sitter parse --time --quiet sample.clj
```

