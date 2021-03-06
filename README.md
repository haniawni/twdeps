# TaskWarrior Dependency Visualization

Visualizes dependencies between TaskWarrior tasks.

[![Build Status](https://secure.travis-ci.org/nerab/twdeps.png?branch=master)](http://travis-ci.org/nerab/twdeps)
[![Gem Version](https://badge.fury.io/rb/twdeps.png)](http://badge.fury.io/rb/twdeps)

## Example

Given a set of interdependent tasks described in the TaskWarrior [tutorial](http://taskwarrior.org/projects/taskwarrior/wiki/Tutorial2#DEPENDENCIES), the tasks are

1. Exported from TaskWarrior as JSON, then
1. Piped into `twdeps`, and finally
1. The output is directed to a PNG file.

Result:

![party](https://raw.github.com/nerab/twdeps/master/examples/party.png)

For the impatient: The JSON export is also available as [party.json](https://raw.github.com/nerab/twdeps/master/test/fixtures/party.json). If you download it, the command

    $ twdeps -f png party.json > party.png

will generate `party.png` in the current directory.

## Installation

    $ gem install twdeps

## Usage

    # Create a dependency graph as PNG and pipe it to a file
    # See [Limitations](Limitations) below for why we need the extra task parms
    task export rc.json.array=on rc.verbose=nothing | twdeps > deps.png

    # Same but specify output format
    task export rc.json.array=on rc.verbose=nothing | twdeps --format svg > deps.svg

    # Create a graph from a previously exported file
    task export rc.json.array=on rc.verbose=nothing > tasks.json
    cat tasks.json | twdeps > deps.png

    # Display graph in browser without creating an intermediate file
    # Requires bcat to be installed
    task export rc.json.array=on rc.verbose=nothing | twdeps --format svg | bcat

## Dependencies

The graph is generated with [ruby-graphviz](https://github.com/glejeune/Ruby-Graphviz), which in turn requires a local [Graphviz](http://graphviz.org/) installation (e.g. `brew install graphviz` on a Mac or `sudo apt-get install graphviz` on Ubuntu Linux).

[bcat](http://rtomayko.github.com/bcat/) is required for piping into a browser.

## Limitations

Due to [two](http://taskwarrior.org/issues/1017) [bugs](http://taskwarrior.org/issues/1013) in its JSON export, TaskWarrior versions before 2.1 need the additional command line options `rc.json.array=on` and `rc.verbose=nothing`.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
