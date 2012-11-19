## Bootstarp Build Template Example

This is an example build environment for bootstrap. Bootstrap itself is a git submodule in src/lib/bootstrap, with src/lib/bootstrap/less added to the less
compile path after src/less.

#### Requirements

This project requires ruby and rubygems, with bundler installed.

#### Installation

  * git clone the repo
  * git submodule init; git submodule update (to download the bootstrap submodule)
  * bundle install (to install the ruby libraries)

#### Usage

To build the project

    $ rake build

To watch the src directory for js and less changes

    $ rake watch
