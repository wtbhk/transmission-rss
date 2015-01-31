transmission-rss
================

transmission-rss is basically a workaround for transmission's lack of the
ability to monitor RSS feeds and automatically add enclosed torrent links.

It works with transmission-daemon and transmission-gtk (if the web frontend
is enabled in the settings dialog). Sites like showrss.karmorra.info and
ezrss.it or self-hosted seriesly instances are suited well as feed sources.

A tool called transmission-add-file is also included for mass adding of
torrent files.

As it's done with poems, I devote this very artful and romantic piece of
code to the single most delightful human being: Ann.

The minimum supported Ruby version is 1.9.3.

Installation
------------

### Latest stable version from rubygems.org

    gem install transmission-rss

### From source

    git clone git://git.orgizm.net/transmission-rss.git
    cd transmission-rss
    gem build transmission-rss.gemspec
    gem install transmission-rss-*.gem

Configuration
-------------

A yaml formatted config file is expected at `/etc/transmission-rss.conf`.

### Minimal example

It should at least contain a list of feeds:

    feeds:
      - url: http://example.com/feed1
      - url: http://example.com/feed2

Feed item titles can be filtered by a regular expression:

    feeds:
      - url: http://example.com/feed1:
        regexp: foo
      - url: http://example.com/feed2:
        regexp: (foo|bar)

Feeds can also be configured to download files to specific directory:

    feeds:
      - url: http://example.com/feed1:
        download_dir: /home/user/Downloads

### All available options

The following configuration file example contains every existing option
(although `update_interval`, `add_paused`, `server`, `fork`, and `pid_file` are
default values and could be omitted). The default `log_target` is STDERR.
`privileges` is not defined by default, so the script runs as current
user/group. `login` is also not defined by default. It has to be defined, if
transmission is configured for HTTP basic authentication.

    feeds:
      - url: http://example.com/feed1
      - url: http://example.com/feed2
      - url: http://example.com/feed3
        regexp: match1
      - url: http://example.com/feed4
        regexp: (match1|match2)
      - url: http://example.com/feed4
        download_dir: /home/user/Downloads

    update_interval: 600

    add_paused: false

    server:
      host: localhost
      port: 9091

	login:
	  username: transmission
	  password: transmission

    log_target: /var/log/transmissiond-rss.log

    privileges:
      user: nobody
      group: nobody

    fork: false

    pid_file: false

TODO
----

* Option to stop seeding after full download.
* Configurable log level.
