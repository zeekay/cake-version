use 'sake-bundle'
use 'sake-outdated'
use 'sake-publish'
use 'sake-test'

try
  use require './'
catch err

task 'build', 'build project', ->
  bundle.write
    entry: 'src/index.coffee'
    compilers:
      coffee: version: 1

task 'clean', 'clean project', ->
  exec 'rm -rf lib'

task 'watch', 'watch for changes and recompile project', ->
  b = yield bundle
    entry:    'src/index.coffee'
    external: true

  build = (filename) ->
    console.log filename
    b.write
      invalidate: [filename]
      formats:    ['cjs', 'es']

  watch 'src/*', build
