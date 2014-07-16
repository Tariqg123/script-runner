# Script Runner

This package will run various script files inside of Atom. It currently supports JavaScript, CoffeeScript, Ruby, Python, Bash, Go and anything with a shebang line.

![Example](https://github.com/ioquatix/script-runner/raw/master/resources/screenshot-1.png)

This package is a fork of the popular `atom-runner` but with many PRs merged and other issues fixed. It includes support for shebang lines (`#!`) and proper (currently non-interactive) terminal emulation. Many thanks to Loren Segal and all the contributing developers.

## Usage

N.B. these keyboard shortcuts are currently being reviewed, [input is welcome](https://github.com/ioquatix/script-runner/issues/1).

| Command              | Mac OS X               | Linux/Windows           |
|----------------------|------------------------|-------------------------|
| Run: Script          | <kbd>cmd-shift-x</kbd> | <kbd>ctrl-shift-x</kbd> |
| Run: Terminate       | <kbd>cmd-shift-z</kbd> | <kbd>ctrl-shift-z</kbd> |

Scripts which have been saved run in their directory, unsaved scripts run in the workspace root directory.

### Pseudo TTY Emulation

Most interpreters output to `stdout` and `stderr`, however the buffering mechanisms are often different when the process is not running on a PTY. For example, Ruby buffers `stdout` when not attached to a terminal which causes incorrect order of output when writing to both `stdout` and `stderr`. Additionally, most programs won't output control codes used for colouring the output when not running on a terminal. `script-runner` uses the `script` command to emulate a terminal and generally gives the best output.

### Shebang Lines

In a typical UNIX environment, the shebang line specifies the interpreter to use for the script:

```ruby
#!/usr/bin/env ruby
puts "Hello World"
```

The shebang line is the preferred way to specify how to run something as it naturally supports all the intricacies of your underlying setup, e.g. Ruby's `rvm`, Python's `virtualenv`.

Even for unsaved files without an associated grammar, as long as you have the correct shebang line it will be executed correctly.

### Environment Variables

The default Atom process takes environment variables from the shell it was launched from. This might be an issue if launching Atom directly from the desktop environment when using, say, RVM. This is a particularly insideous problem on Mac OS X.

To ensure everything works as expected, when a script is run, the environment variables are extracted from the login shell (what you usually get when you open a terminal) and used when you run your script. This should ensure that you get the same behaviour from both Atom and a terminal.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License

Released under the MIT license. Please see `LICENSE.md` for the full license.
