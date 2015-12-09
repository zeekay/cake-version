require 'shortcake'

use require './'

option '-b', '--browser [browser]', 'browser to use for tests'
option '-g', '--grep [filter]',     'test filter'
option '-t', '--test [test]',       'specify test to run'
option '-v', '--verbose',           'enable verbose test logging'

task 'clean', 'clean project', ->
  exec 'rm -rf lib'

task 'build', 'build project', ->
  exec 'node_modules/.bin/coffee -bcm -o lib/ src/'

task 'test', 'Run tests', (opts, cb) ->
  grep    = opts.grep             ? ''
  test    = opts.test             ? 'test/'
  verbose = opts.verbose          ? ''

  grep    = "--grep #{opts.grep}" if grep
  verbose = "VERBOSE=true" if verbose

  exec "NODE_ENV=test #{verbose}
        node_modules/.bin/mocha
        --colors
        --reporter spec
        --timeout 100000
        --compilers coffee:coffee-script/register
        --require co-mocha
        --require postmortem/register
        #{grep}
        #{test}", (err) ->
    if err
      process.exit 1
    else
      process.exit 0

task 'watch', 'watch for changes and recompile project', ->
  exec 'coffee -bc -m -w -o lib/ src/'
