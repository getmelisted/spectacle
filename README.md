# SwiqSpectacle

SwiqSpectacle is OpenAPI 2.0 docs generator for SweetIQ projects that need branded documentation. See what they look like [here](http://locs-stag.swiq3.com/docs/).

This repo is a fork of [Spectacle](https://sourcey.com/spectacle):

>Spectacle generates beautiful static HTML5 documentation from [OpenAPI](https://openapis.org)/[Swagger](http://swagger.io) 2.0 API specifications. The goal of Spectacle is help you "save time and look good" by providing an extensible platform for auto generating your REST API docs. The default layout is a three column single page, similar to those employed by [Stripe](https://stripe.com/docs/api) and [Intercom](https://developers.intercom.com/reference).

## Features

* **OpenAPI/Swagger 2.0 support**: Support for the latest OpenAPI/Swagger specification.
* **Markdown support**: Render markdown written in any of your API descriptions.
* **Custom Guides/Topics**: Write custom guides for your users to explain the complicated stuff. See `test/fixtures/swiq/topics` for examples. All in markdown. Wooh!
* **Remote file references**: Support for swagger specs split across multiple files.
* **Clean responsive design**: Responsive HTML5 and CSS3 layout built with [Foundation 6](http://foundation.zurb.com/sites.html) that looks great on all devices and screen sizes.
* **Embed into your existing website**: An embedded option so that generate partial docs without a HTML `<body>` for convenient integration into your existing website.
* **Live preview developer mode**: Development mode that starts a local HTTP server with a file watcher and live reload so you can preview live changes in your browser as you update your spec.

## Usage

Add **SwiqSpectacle** to your `package.json`:

```json
"spectacle-docs": "git+ssh://git@github.com:getmelisted/spectacle.git#master"
```

Next pass your `api.json` or `api.yaml` document to the CLI to generate your documentation.

```bash
spectacle -d your_sweetiq_api.json
```

Your generated documentation will be located in the `public` directory by default. You can either copy the generated HTML to your web server, or view your docs by pointing your browser to [http://localhost:4400/](http://localhost:4400/).

### Docker

[Docker](https://hub.docker.com/r/sourcey/spectacle/) images are included that allow Spectacle to be run from the inside. It's useful, for instance, in a Gitlab CI pipeline. Thanks @alexeiaguiar.

How to use it: `docker run -it sourcey/spectacle /bin/sh`

## Configuration Options

The basic CLI options are detailed below:

```bash
$ spectacle -h

  Usage: spectacle [options] <specfile>

  Options:

    -h, --help                   output usage information
    -V, --version                output the version number
    -C, --disable-css            omit CSS generation (default: false)
    -J, --disable-js             omit JavaScript generation (default: false)
    -e, --embeddable             omit the HTML <body/> and generate the documentation content only (default: false)
    -d, --development-mode       start HTTP server with the file watcher (default: false)
    -D, --development-mode-live  start HTTP server with the file watcher and live reload (default: false)
    -s, --start-server           start the HTTP server without any development features
    -p, --port <port>            the port number for the HTTP server to listen on (default: 4400)
    -P, --port-live <port>       the port number for the live reload to listen on (default: 4401)
    -t, --target-dir <dir>       the target build directory (default: public)
    -f, --target-file <file>     the target build HTML file (default: index.html)
    -a, --app-dir <dir>          the application source directory (default: app)
    -l, --logo-file <file>       specify a custom logo file (default: null)
    -c, --config-file <file>     specify a custom configuration file (default: app/lib/config.js)
```

Most options are self explanatory, but the following options warrant some further explanation:

* **--development-mode** `-d`: This option starts a development server with a file watcher, and will automatically regenerate your docs when any of your spec or app files change.

* **--development-mode-live** `-D`: This option starts a development server with a file watcher and live reload, and will automatically regenerate your docs when any of your spec or app files change.

* **--start-server** `-s`: This option starts a production server without any development options enabled that serves the contents of your `--target-dir`.

* **--embeddable** `-e`: This option lets you build a minimal version of the documentation without the HTML `<body>` tags, so you can embed Spectacle into your own website template. More info on [custom builds](#custom-builds) here.

* **--app-dir** `-a`: This option overrides the default directory which contains all the Handlebars templates, SCSS, and JavaScript source files. This option is useful for development because you can copy the contents of `app` to a remote location or a separate repo for custom builds.

* **--target-dir** `-t`: This option specifies where the generated documentation HTML files will be output.

## Development
You can find a demo setup in `test/fixtures/swiq`. Run: 
```bash
node bin/spectacle -D test/fixtures/swiq/location-loader-api-docs.yaml --logo-file test/fixtures/swiq/sweetiq_small.png
```
It will build the docs and serve them on `localhost:4400` with hot reload. Now you can modify the source and see your changes live in your browser.

- To modify styles, go to `app/stylesheets`.
- To modify template, go to `app/views`

### Testing

Testing is powered by [Mocha](https://mochajs.org/)/[Chai](http://chaijs.com/), and automated testing is run via [CircleCI](https://circleci.com/).

At this stage, unit tests have not been written for all parts of the codebase.  However, new code should be tested, and unit tests for the existing code will be added in the future.

Run `npm test` on the repository to start the automated tests.
Some parts of testing can be configured using environment variables.

- `OFFLINE=true`
  Some tests use HTTP connections to test giving Spectacle remote API specifications.
  Use `OFFLINE=true` to skip tests that require an internet connection.

Include environment variables before calling `npm test`.  For example, `OFFLINE` mode can be enabled via `OFFLINE=true npm test`.

## More Information

If you are running into problems, slack to Anthony S. or report an issue into this repo's issue tracker

All contributions are welcome.

Good luck and enjoy **SwiqSpectacle**!
