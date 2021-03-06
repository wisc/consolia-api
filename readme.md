# Consolia API in Go w/ MySQL

Back-office API for [Consolia](https://consolia-comic.com/), a webcomic. Back-office, as in only used by the admin panel and not by the website itself.

It's a simple REST API written in Go, backed by MySQL. It primarily uses:

- [Negroni](https://github.com/urfave/negroni) - HTTP middleware
- [Gorm](https://github.com/jinzhu/gorm) - ORM library
- [Osin](https://github.com/RangelReale/osin) - Oauth2 server library
- [Migrate](https://github.com/mattes/migrate/) - DB migrations
- [Godep](https://github.com/tools/godep) - Dependency manager

It is unit tested and can validate API output against the JSON schemas.


## Getting Started

1) The API uses environment variables to inject environment-specific stuff. Just add these environment variables to your `~/.profile`:

```
export consolia_db_host=127.0.0.1
export consolia_db_port=3306
export consolia_db_name=consolia
export consolia_db_username=consolia
export consolia_db_password=supersecretyouwillneverguessthishahaha
export consolia_port=3000
export consolia_env=dev
```

2) Provision the DB. Run the migrations:

```console
$ make migrate_up
```

3) The tool uses `godep` to manage the dependencies. Install it:
```console
$ go get github.com/tools/godep
```

4) Build the API:
```console
$ make build
```

5) Test:
```console
$ make test
```

6) Run:
```console
$ make run
```


## Features

Features of this API:

- Administer comics (basic CRUD)
- Notify on any updates in social media platforms, e.g. new upvotes in reddit, more likes on facebook.
- All-time social media scoreboard - the most popular comics on the most popular platforms
- Expose awesome statistics, like how long it's been running, how many square pixels have been drawn, etc.
- Notifications - put the comics through a validator, and expose any quirks the comics have.


The internal processes that update the database are *not in this repo*, processes like:

- Publishing comics on a set date
- Tracking likes/upvotes on social media platforms (supporting reddit, 9gag, cheezburger, tumblr, twitter, facebook)
- Tracking Google Analytics data
