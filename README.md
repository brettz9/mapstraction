# mapstraction

Browserify plugin to extract sourcemaps.

[![Build Status](https://travis-ci.org/jiborobot/mapstraction.svg?branch=master)](https://travis-ci.org/jiborobot/mapstraction)

This plugin was created to solve two problems: extract sourcemaps similar to [exorcist](https://www.npmjs.com/package/exorcist) but that would work without having to pipe results. 

## Usage

Include `mapstraction` as a Browserify plugin on the commandline. The name of the default file is the output name, (e.g., "bundle.js.map").

```bash
browserify main.js -o bundle.js -p mapstraction --debug
```

### Path Output

Pass in an optional argument with the path of the map file.

```bash
browserify main.js -o bundle.js -p [ mapstraction "custom.js.map" ] --debug
```

### Options

Options can be supplied in the following manner:

```bash
browserify main.js -o bundle.js -p [ mapstraction "custom.js.map" --sourcesBase "basePath/" ] --debug
```

The following options are available:

- `sourceRoot` - Sets the `sourceRoot` on the extracted map
- `sourcesBase` - Adjusts the `sources` files obtained from the source map to be relative to the given base path.
- `sourcesMap` - If no `sourcesBase` is present, this map function will be used for adjusting the `sources` files obtained from the source map. Should return the adjusted result.

If neither `sourcesBase` nor `sourceMap` is present, the `sources` files will
instead be mapped to be relative to the based of the supplied map path
(defaults to the output file plus `".map"`) and with backslashes replaced
(to avoid comparisons being Windows-format-dependent such as with
[this issue](https://github.com/thlorenz/combine-source-map/pull/23)).
