# Building:

Testing on Ubuntu 20.04. Note, snap package for ruby doesn't work. Instead, I'm using the ruby install from [https://rvm.io/](https://rvm.io/), and using the fishshell integration [https://rvm.io/integration/fish](https://rvm.io/integration/fish)

```
~> rvm use 2.7
Using /home/jtuckey/.rvm/gems/ruby-2.7.0
~> ruby --version
ruby 2.7.0p0 (2019-12-25 revision 647ee6f091) [x86_64-linux]
~/g/darwinmakers-site[7]> bundle update jekyll
Fetching gem metadata from https://rubygems.org/...........
Fetching gem metadata from https://rubygems.org/.
Resolving dependencies...
Fetching public_suffix 4.0.5 (was 4.0.3)
Installing public_suffix 4.0.5 (was 4.0.3)
Fetching addressable 2.7.0
Installing addressable 2.7.0
Using bundler 2.1.4
Fetching colorator 1.1.0
Installing colorator 1.1.0
Fetching concurrent-ruby 1.1.6 (was 1.1.5)
Installing concurrent-ruby 1.1.6 (was 1.1.5)
Fetching eventmachine 1.2.7
Installing eventmachine 1.2.7 with native extensions
Fetching http_parser.rb 0.6.0
Installing http_parser.rb 0.6.0 with native extensions
Fetching em-websocket 0.5.1
Installing em-websocket 0.5.1
Fetching ffi 1.12.2 (was 1.11.3)
Installing ffi 1.12.2 (was 1.11.3) with native extensions
Fetching forwardable-extended 2.6.0
Installing forwardable-extended 2.6.0
Fetching i18n 1.8.2 (was 1.7.0)
Installing i18n 1.8.2 (was 1.7.0)
Fetching sassc 2.3.0 (was 2.2.1)
Installing sassc 2.3.0 (was 2.2.1) with native extensions
Fetching jekyll-sass-converter 2.1.0 (was 2.0.1)
Installing jekyll-sass-converter 2.1.0 (was 2.0.1)
Fetching rb-fsevent 0.10.4 (was 0.10.3)
Installing rb-fsevent 0.10.4 (was 0.10.3)
Fetching rb-inotify 0.10.1
Installing rb-inotify 0.10.1
Fetching listen 3.2.1
Installing listen 3.2.1
Fetching jekyll-watch 2.2.1
Installing jekyll-watch 2.2.1
Fetching rexml 3.2.4
Installing rexml 3.2.4
Fetching kramdown 2.2.1 (was 2.1.0)
Installing kramdown 2.2.1 (was 2.1.0)
Fetching kramdown-parser-gfm 1.1.0
Installing kramdown-parser-gfm 1.1.0
Fetching liquid 4.0.3
Installing liquid 4.0.3
Fetching mercenary 0.3.6
Installing mercenary 0.3.6
Fetching pathutil 0.16.2
Installing pathutil 0.16.2
Fetching rouge 3.19.0 (was 3.14.0)
Installing rouge 3.19.0 (was 3.14.0)
Fetching safe_yaml 1.0.5
Installing safe_yaml 1.0.5
Fetching unicode-display_width 1.7.0 (was 1.6.0)
Installing unicode-display_width 1.7.0 (was 1.6.0)
Fetching terminal-table 1.8.0
Installing terminal-table 1.8.0
Fetching jekyll 4.0.1 (was 4.0.0)
Installing jekyll 4.0.1 (was 4.0.0)
Fetching jekyll-feed 0.13.0
Installing jekyll-feed 0.13.0
Fetching jekyll-seo-tag 2.6.1
Installing jekyll-seo-tag 2.6.1
Fetching minima 2.5.1
Installing minima 2.5.1
Bundle updated!
Post-install message from i18n:

HEADS UP! i18n 1.1 changed fallbacks to exclude default locale.
But that may break your application.

If you are upgrading your Rails application from an older version of Rails:

Please check your Rails app for 'config.i18n.fallbacks = true'.
If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
'config.i18n.fallbacks = [I18n.default_locale]'.
If not, fallbacks will be broken in your app by I18n 1.1.x.

If you are starting a NEW Rails application, you can ignore this notice.

For more info see:
https://github.com/svenfuchs/i18n/releases/tag/v1.1.0

Post-install message from jekyll:
-------------------------------------------------------------------------------------
Jekyll 4.0 comes with some major changes, notably:

  * Our `link` tag now comes with the `relative_url` filter incorporated into it.
    You should no longer prepend `{{ site.baseurl }}` to `{% link foo.md %}`
    For further details: https://github.com/jekyll/jekyll/pull/6727

  * Our `post_url` tag now comes with the `relative_url` filter incorporated into it.
    You shouldn't prepend `{{ site.baseurl }}` to `{% post_url 2019-03-27-hello %}`
    For further details: https://github.com/jekyll/jekyll/pull/7589

  * Support for deprecated configuration options has been removed. We will no longer
    output a warning and gracefully assign their values to the newer counterparts
    internally.
-------------------------------------------------------------------------------------
~/g/darwinmakers-site>
```
Now you should be able to run:
```
~/g/darwinmakers-site> jekyll serve
Warning: the running version of Bundler (2.1.2) is older than the version that created the lockfile (2.1.4). We suggest you to upgrade to the version that created the lockfile by running `gem install bundler:2.1.4`.
Configuration file: /home/jtuckey/g/darwinmakers-site/_config.yml
            Source: /home/jtuckey/g/darwinmakers-site
       Destination: /home/jtuckey/g/darwinmakers-site/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 0.128 seconds.
 Auto-regeneration: enabled for '/home/jtuckey/g/darwinmakers-site'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
[2020-05-16 10:27:43] ERROR `/favicon.ico' not found.
```

# Adding upcoming events
Upcoming events are created in the \_events directory. Past events will only be excluded when the site is rebuilt but an empty commit should be sufficent to trigger this process.
