# Omnom

Bookmarking with website snapshots.


Access & share previously visited pages without worrying about modifications or availability.


Check out our [wiki](https://github.com/asciimoo/omnom/wiki) for more information.


## Features

 - Websites are captured as your browser renders it - saves the displayed content of heavily JS driven dynamic pages
 - Self hosted
 - Web interface with multiuser support
 - Flexible filtering - by date, free text search in content, tags, users, domains, URLs, etc..
 - Private & public bookmarks
 - Multiple snapshots of the same URL
 - [Documented API](https://github.com/asciimoo/omnom/wiki/API-documentation)


## Requirements

go >= 1.24

## Setup & run

 - Checkout the repo and execute `go get -u`
 - Copy `config.yml_sample` to `config.yml`
 - Execute `go build && ./omnom listen` or `go run omnom.go listen` in the repo root

Settings can be configured in `config.yml` config file - don't forget to restart webapp after updating.


## User handling

Omnom does not store passwords. Login requires one time login tokens or OAuth.
Login tokens can be requested via email (this requires a valid SMTP configuration in `config.yml`) through the web interface or can be generated from command line using the `./omnom create-token [username] login`.


### Command line tool

Basic management actions are available using the command line tool (`go run omnom.go` or `go build; ./omnom`)

#### Available Commands
```
  create-token         create new login/addon token for a user
  create-user          create new user
  generate-api-docs-md Generate Markdown API documentation
  help                 Help about any command
  listen               start server
  set-token            set new login/addon token for a user
  show-user            show user details
  completion           Generate the autocompletion script for the specified shell
```

### Browser addon

Omnom browser addon is available for
- [Firefox](https://addons.mozilla.org/en-US/firefox/addon/omnom/)
- [Chrome/Chromium](https://chrome.google.com/webstore/detail/omnom/nhpakcgbfdhghjnilnbgofmaeecoojei)

## Docker

Run Omnom with Docker using the following command:

```bash
docker run -p 7331:7331/tcp ghcr.io/asciimoo/omnom:latest
```

### Configuration

#### Port Mapping
The container exposes port 7331. Map it to your host port:
```bash
-p <host_port>:7331/tcp
```

#### Volumes
Persist your data using these volumes:

| Container Path        | Description                                                                 | Recommended Mount Type |
|-----------------------|-----------------------------------------------------------------------------|------------------------|
| `/omnom/config`       | Database (SQLite), ActivityPub keys, and configuration files                | Bind mount or volume   |
| `/omnom/static/data`  | Snapshot data and user-uploaded content                                     | Bind mount or volume   |

Example with volumes:
```bash
docker run -p 7331:7331/tcp \
  -v ./omnom_config:/omnom/config \
  -v ./omnom_data:/omnom/static/data \
  ghcr.io/asciimoo/omnom:latest
```

#### Custom Configuration
You can modify the default `config.yml` by mounting your own version:
```bash
-v ./custom_config.yml:/omnom/config.yml
```

### Advanced Usage

#### Custom Commands
Run any Omnom command directly:
```bash
docker run ghcr.io/asciimoo/omnom:latest /omnom/omnom --help
```

#### Environment Variables
| Variable | Description                | Default |
|----------|----------------------------|---------|
| `UID`    | User ID for Omnom process  | 1000    |
| `GID`    | Group ID for Omnom process | 1000    |

## Bugs

Bugs or suggestions? Visit the [issue tracker](https://github.com/asciimoo/omnom/issues) or join our [discord server](https://discord.gg/GAh4RCruh6)

## License

AGPLv3

## Funding

This project is funded through [NGI Zero Core](https://nlnet.nl/core), a fund established by [NLnet](https://nlnet.nl) with financial support from the European Commission's [Next Generation Internet](https://ngi.eu) program. Learn more at the [NLnet project page](https://nlnet.nl/project/Omnom-ActivityPub).

[<img src="https://nlnet.nl/logo/banner.png" alt="NLnet foundation logo" width="20%" />](https://nlnet.nl)
[<img src="https://nlnet.nl/image/logos/NGI0_tag.svg" alt="NGI Zero Logo" width="20%" />](https://nlnet.nl/core)
