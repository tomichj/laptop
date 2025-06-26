Laptop
======

Laptop is a script to configure my OS X laptop for ruby development.

Much of this script comes from thoughtbot/laptop, thanks guys!

You can safely run this multiple times on the same laptop.


Install
-------

Download and review the script, or execute the script right from github like so:

```sh
bash <(curl -s https://raw.githubusercontent.com/tomichj/laptop/master/mac)
```


What it sets up
---------------

A mac with a minimal configuration for Ruby and Rails development. 


macOS package management:

[Homebrew]: http://brew.sh/

Unix command line utilities:
* [bash] the Bourne Again SHell
* [bash-completion] command line completion for bash 
* [openssl] for SSL and TLS
* [gnutls] GNU Transport Layer Security (TLS) Library
* [tree] Display directories as trees
* [coreutils] GNU File, Shell, and Text utilities
* [findutils] Collection of GNU find, xargs, and locate
* [grc] Colorize logfiles and command output
* [spark] Sparklines for the shell
* [imagemagick] Tools and libraries to manipulate images in many formats
* [libyaml] YAML Parser
* [the_silver_searcher] Code-search similar to ack

[bash]: https://www.gnu.org/software/bash/
[bash-completion]: https://davidalger.com/posts/bash-completion-on-os-x-with-brew/
[openssl]: https://www.openssl.org/
[gnutls]: https://gnutls.org/
[tree]: http://mama.indstate.edu/users/ice/tree/
[coreutils]: https://www.gnu.org/software/coreutils
[findutils]: https://www.gnu.org/software/findutils/
[grc]: https://korpus.juls.savba.sk/~garabik/software/grc.html
[spark]: https://zachholman.com/spark/
[imagemagick]: https://www.imagemagick.org/
[libyaml]: https://github.com/yaml/libyaml
[the_silver_searcher]: https://github.com/ggreer/the_silver_searcher

Git tools:
* [git] the git distributed revision control system
* [hub] add GitHub support to git on the command-line
* [sourcetree] a visual git client
* [github desktop] github's visual git client
* [diffmerge] visually compare and merge files 

[git]: https://git-scm.com
[hub]: https://hub.github.com/
[sourcetree]: https://www.sourcetreeapp.com/
[github desktop]: https://desktop.github.com/
[diffmerge]: https://www.sourcegear.com/diffmerge/

Ruby dev environment:
* [rbenv] Ruby version manager
* [ruby-build] Install various Ruby versions and implementations
* [puma-dev] A tool to manage rack apps in development with puma
* [heroku/brew/heroku] Everything you need to get started with Heroku
* [ngrok] Public URLs for exposing your local resources (web servers, etc)

[rbenv]: https://github.com/rbenv/rbenv#readme
[ruby-build]: https://github.com/rbenv/ruby-build
[puma-dev]: https://github.com/puma/puma-dev
[heroku/brew/heroku]: https://cli.heroku.com
[ngrok]: https://ngrok.com/

Browsers:
* Google's (chrome)[google-chrome] browser
* The [firefox] browser

[google-chrome]: https://www.google.com/chrome/
[firefox]: https://www.mozilla.org/firefox/

Databases and tools:
* [postgres] a full-featured PostgreSQL installation packaged as a standard Mac app.
* [redis-app] a redis installation packages as a standard Mac app.
* [postico] a Postgres client 

[postgres]: https://postgresapp.com/
[redis-app]: https://jpadilla.github.io/redisapp/
[postico]: https://eggerapps.at/postico/


Latest ruby:
* rbenv and ruby-build are used to install the latest version of Ruby
* rbenv is configured to use this version of ruby
* Bundler is then installed and configured in the just-installed ruby

Bash:
* The latest version of bash is installed and added to /etc/shells
* Your shell is switched to bash


Customize in `~/.laptop.local`
------------------------------

Your `~/.laptop.local` is run at the end of the Laptop script.
Put your customizations there.
For example:

```sh
#!/bin/sh

brew bundle --file=- <<EOF
brew "Caskroom/cask/dockertoolbox"
brew "go"
brew "ngrok"
brew "watch"
EOF

default_docker_machine() {
  docker-machine ls | grep -Fq "default"
}

if ! default_docker_machine; then
  docker-machine create --driver virtualbox default
fi

default_docker_machine_running() {
  default_docker_machine | grep -Fq "Running"
}

if ! default_docker_machine_running; then
  docker-machine start default
fi

fancy_echo "Cleaning up old Homebrew formulae ..."
brew cleanup
brew cask cleanup

if [ -r "$HOME/.rcrc" ]; then
  fancy_echo "Updating dotfiles ..."
  rcup
fi
```

Write your customizations such that they can be run safely more than once.
See the `mac` script for examples.

Laptop functions such as `fancy_echo` and
`gem_install_or_update`
can be used in your `~/.laptop.local`.

See the [wiki](https://github.com/thoughtbot/laptop/wiki)
for more customization examples.


License
-------
© 2016-2019 Justin Tomich
© 2011-2015 thoughtbot, inc.

It is free software, 
and may be redistributed under the terms specified in the [LICENSE] file.

[LICENSE]: LICENSE

