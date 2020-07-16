# heroku-buildpack-artanis
A Heroku buildpack to run Guile's [Artanis](https://web-artanis.com/), web-application framework, on Heroku.

This buildpack is dependent on my [Guile buildpack](https://github.com/WammKD/heroku-buildpack-guile-scheme).

There is also a [DBI/DBD buildpack](https://github.com/WammKD/heroku-buildpack-guile-dbi-and-dbd), if you want to use Artanis with a database (currently, the buildpack only supports MySQL), and a [GnuTLS buildpack](https://github.com/WammKD/heroku-buildpack-gnutls-with-guile-bindings), if you want to make https calls with Guile.

The Guile buildpack should be added first, so that it runs first, though I believe the other two can go in any which order so long as they're after the Guile and before the Artanis buildpacks (though I've only tested them in Guile, GnuTLS, DBD/DBI, and then Artanis order).

## Notes
This buildpack is setup to run a standard Artanis project so it will check that an `ENTRY` file exists to deploy successfully and will run `art work -p $PORT` for you (so there's no need to provide a Procfile to your project to properly run your app. on Heroku).

Also, make sure that your `artanis.conf` file has set `host.addr` from 127.0.0.1 to 0.0.0.0 or Artanis will not properly bind to `$PORT`.
