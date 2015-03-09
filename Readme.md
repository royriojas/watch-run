**Important**
This is a fork from `watch-run` that uses `spawn` instead of `exec` internally for the following reasons:

- spawn does not have a buffer limit for stdout
- spawn does not loses colored output when terminal allows it

Everything else is the same as the origina watch-run

# watch-spawn(1)

> Re-execute a given command everytime something changes in a specific directory. Build upon [gaze](https://github.com/shama/gaze).

## Installation

	$ npm install -g watch-spawn

## Usage

Via `--help`:

```
Usage: watch-spawn <cmd>

Options:

  -h, --help               output usage information
  -p, --pattern <pattern>  glob pattern. More info: https://github.com/isaacs/minimatch
  -i  --initial            run <cmd> on initial startup
  -d  --delay <n>          delay execution of <cmd> for a number of milliseconds
  -s  --stop-on-error     stop watching and exit when errors occur in <cmd>

Examples:

  # watch dir and execute cmd
  $ watch-spawn -p 'lib/**' cat package.json
```

## Example

	$ watch-spawn -p 'js/modules/**/*.js' browserify main.js -o public/build.js

## License

MIT
