**Important**
This is a fork from `watch-run` that uses `spawn` instead of `exec` internally for the following reasons:

- spawn does not have a buffer limit for stdout
- spawn does not loses colored output when terminal allows it
- add option to specify several patterns passing several times the `-p, --pattern` option all the options will be
  aggregated into a single array to pass to Gaze.
- add option to react only on certain events: `added`, `changed`, `deleted` or `renamed`.
- add verbose info, use `-q, --quiet`  to reduce the noise. (the info about when the command is run and when it finish will always be printed regardless the value of `--quiet`)
- add option to skip executing the command if the command is already running `-k, --skip-if-running`.

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

  -h, --help                     output usage information
  -p, --pattern [pattern]        glob pattern. More info: https://github.com/isaacs/minimatch
  -i, --initial                  run <cmd> on initial startup
  -d, --delay <n>                delay execution of <cmd> for a number of milliseconds
  -s, --stop-on-error            stop watching and exit when errors occur in <cmd>
  -f, --fire-on-events <events>  fire only on the events provided: `added`, `changed` or `deleted`
  -q, --quiet                    be as quiet as possible
  -k, --skip-if-running          skip if currently executing the <cmd>


Examples:

  # watch dir and execute cmd
  $ watch-spawn -p 'lib/**' cat package.json

```

## Examples

```bash
# listen to changes on js/modules/**/*.js and execute browserify
watch-spawn -p 'js/modules/**/*.js' browserify main.js -o public/build.js

# listen only to `added`, `deleted` events and execute browserify
watch-spawn -f 'added, deleted' -p 'js/modules/**/*.js' browserify main.js -o public/build.js

# all of previous but execute the command first and then wait to see if execute in again on any change
watch-spawn -f 'added, deleted' -p 'js/modules/**/*.js' -i browserify main.js -o public/build.js

# all of previous but wait 4 seconds before executing the command (except the first time)
watch-spawn -f 'added, deleted' -p 'js/modules/**/*.js' -i -d 4000 browserify main.js -o public/build.js

# all of previous and quiet
watch-spawn -q -f 'added, deleted' -p 'js/modules/**/*.js' -i -d 4000 browserify main.js -o public/build.js

# all of previous and skip if the command is already running
watch-spawn -k -q -f 'added, deleted' -p 'js/modules/**/*.js' -i -d 4000 browserify main.js -o public/build.js
```

## License

MIT
