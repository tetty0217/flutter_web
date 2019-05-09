[![Gitter chat](https://badges.gitter.im/flutter/flutter_web.png)](https://gitter.im/flutter/flutter_web)

Welcome to the code repository for [Flutter for web](https://flutter.dev/web).

This repository contains the source code for a fork of
[Flutter](https://flutter.dev/) that targets the web. Our goal is to add web
support as a first-tier platform in the Flutter SDK alongside iOS and Android.
The code in this repository is a stepping stone to that goal,
providing web-only packages that implement (almost) the entire Flutter API.

Web support for Flutter is not yet stable. We're designating this release as a
technical preview, designed to validate that the product
meets developers' needs, iterate on major features and get to feature complete.
Design and implementation may change significantly, and changes may be
introduced that break compatibility with existing code. As a result, the Flutter
team do not recommend using code created with Flutter for web in production
at this time.

You can find a
[short introduction to Flutter for web](https://medium.com/flutter-io/bringing-flutter-to-the-web-904de05f0df0)
on our blog.

## Important notes

### Limitations

We intend to completely support all of Flutter's API and functionality across
modern browsers. However, during this preview, there are a number of exceptions:

* `flutter_web` does not have a plugin system yet. _Temporarily_, we provide
  access to `dart:html`, `dart:js`, `dart:svg`, `dart:indexed_db` and other web
  libraries that give you access to the vast majority of browser APIs. However,
  expect that these libraries will be replaced by a different plugin API.
* Not all Flutter APIs are implemented on Flutter for web yet.
* Performance work is only just beginning. The code generated by Flutter for web
  may run slowly, or demonstrate significant UI "jank".
* At this time, desktop UI interactions are not fully complete, so a UI built
  with `flutter_web` may feel like a mobile app, even
  when running on a desktop browser.
* The development workflow is only designed to work with Chrome at the moment.

### Browser support

Flutter for web provides:

* a [production JavaScript compiler](https://webdev.dartlang.org/tools/dart2js)
  that generates optimized, minified code for deployment
* a [development JavaScript compiler](https://webdev.dartlang.org/tools/dartdevc),
  that offers incremental compilation and hot restart

When built with the *production* compiler, Flutter supports Chromium-based
browsers and Safari, both on desktop and mobile. We also aim to fully support
Firefox and Edge as targeted platforms, but our own test coverage is still low
on these browsers. Our intention is to support the current and the last two
major releases. Feedback on rendering and performance issues on all of these
browsers is appreciated.

Internet Explorer support is not planned.

The *development* compiler currently supports Chrome only.

## Testing Flutter for web

While we are far from code complete, we're ready for you to start developing
and experimenting with Flutter for web. We are building the product around a
number of target scenarios,
[as described in our blog](https://medium.com/flutter-io/bringing-flutter-to-the-web-904de05f0df0),
and we'd appreciate your feedback on feature gaps or suitability for these
scenarios, as well as other scenarios for which you find Flutter useful on the
web.

In addition, we'd love to see repros that demonstrate crashes, rendering
fidelity issues or extreme performance issues. We'd also love general feedback
on the quality of the release and the developer experience.

Of particular interest to us is testing across a variety of operating systems
used for development (Windows, Linux, Mac) and browsers used for deployment.

Since we are developing this in a separate fork to the main Flutter repo, we are
not yet ready to accept GitHub pull requests at this time. However,
[GitHub issues][issue tracker] are very welcome.

[issue tracker]: https://goo.gle/flutter_web_issue

## Samples

Check out [flutter.github.io/samples](https://flutter.github.io/samples/).

## Getting started

Flutter 1.5 and above enable support for targeting the web with Flutter,
including Dart compilation to JavaScript. To use the Flutter SDK with the
`flutter_web` preview make sure you have upgraded Flutter to at least `v1.5.4`
by running `flutter upgrade` from your machine. If you're actively developing
for Flutter for web, you may prefer to be running from one of the unstable
channels. Our wiki describes the
[Flutter channels](https://github.com/flutter/flutter/wiki/Flutter-build-release-channels)
and how to select the right one for your needs.

### Clone the flutter_web source code

Clone this repository locally.

### Install the flutter_web build tools

To install the
[`webdev` package](https://pub.dartlang.org/packages/webdev),
which provides the build tools for Flutter for web, run the following:

```console
$ flutter packages pub global activate webdev
```

Ensure that the `$HOME/.pub-cache/bin` directory
[is in your path](https://www.dartlang.org/tools/pub/cmd/pub-global#running-a-script-from-your-path),
and then you may use the `webdev` command directly from your terminal.

> Note: if you have problems configuring `webdev` to run directly, try:<br>
  `flutter packages pub global run webdev [command]`.

### Run the hello_world example

1. The example exists at `examples/hello_world` in the repository.

    ```console
    $ cd examples/hello_world/
    ```

2. Update packages.

    ```console
    $ flutter packages upgrade
    ! flutter_web 0.0.0 from path ../../flutter_web
    ! flutter_web_ui 0.0.0 from path ../../flutter_web_ui
    Running "flutter packages upgrade" in hello_world...                5.0s
    ```

    If that succeeds, you're ready to run it!

3. Build and serve the example locally.

    ```console
    $ webdev serve
    [INFO] Generating build script completed, took 331ms
    ...
    [INFO] Building new asset graph completed, took 1.4s
    ...
    [INFO] Running build completed, took 27.9s
    ...
    [INFO] Succeeded after 28.1s with 618 outputs (3233 actions)
    Serving `web` on http://localhost:8080
    ```

    Open <http://localhost:8080> in Chrome and you should see `Hello World` in
    red text in the upper-left corner.

## Tools support for Flutter web development

### Visual Studio Code

Visual Studio Code supports Flutter web development with the v3.0 release of
the [Flutter extension](https://dartcode.org/).

- [install](https://flutter.dev/docs/get-started/install) the Flutter SDK
- [set up](https://flutter.dev/docs/get-started/editor?tab=vscode) VS Code
- configure VS Code to point to your local Flutter SDK
- run the `Flutter: New Web Project` command from VS Code
- after the project is created, run your app by pressing F5 or
  "Debug -> Start Debugging"
- VS Code will use the `webdev` command-line tool to build and run your app; a
  new Chrome window should open, showing your running app

### Using from IntelliJ

- [install](https://flutter.dev/docs/get-started/install) the Flutter SDK
- [set up](https://flutter.dev/docs/get-started/editor) your copy of IntelliJ or
  Android Studio
- configure IntelliJ or Android Studio to point to your local Flutter SDK
- create a new Dart project; note, for a Flutter for web app, you want to start
  from the Dart project wizard, not the Flutter project wizard
- from the Dart project wizard, select the 'Flutter for web' option for the
  application template
- create the project; `pub get` will be run automatically
- once the project is created, hit the `run` button on the main toolbar
- IntelliJ will use the `webdev` command-line tool to build and run your app; a
  new Chrome window should open, showing your running app

## Workflow

### Use flutter_web packages from git

If you'd like to depend on the `flutter_web` packages without cloning the
repository, you can setup your pubspec as follows:

```yaml
name: my_flutter_web_app

environment:
  sdk: '>=2.2.0 <3.0.0'

dependencies:
  flutter_web: any
  flutter_web_ui: any

dev_dependencies:
  # Enables the `pub run build_runner` command
  build_runner: ^1.1.2
  # Includes the JavaScript compilers
  build_web_compilers: ^1.0.0

# flutter_web packages are not published to pub.dartlang.org
# These overrides tell the package tools to get them from GitHub
dependency_overrides:
  flutter_web:
    git:
      url: https://github.com/flutter/flutter_web
      path: packages/flutter_web
  flutter_web_ui:
    git:
      url: https://github.com/flutter/flutter_web
      path: packages/flutter_web_ui
```

### Getting (stateless) hot-reload with `webdev`

To use `webdev` with hot-reload, run the following within your project
directory:

```console
$ webdev serve --auto restart
```

You'll notice a similar output to `flutter packages pub run build_runner serve`
but now changes to your application code should cause a quick refresh of the
application on save.

> Note: the `--hot-reload` option is not perfect. If you notice unexpected
  behavior, you may want to manually refresh the page.

> Note: the `--hot-reload` option is currently "stateless". Application state
  will be lost on reload. We do hope to offer "stateful" hot-reload on the web
  – we're actively working on it!


### Building with the production JavaScript compiler

The workflow documented above (available with `build_runner` and `webdev`) uses
the [Dart Dev Compiler](https://webdev.dartlang.org/tools/dartdevc) which is
designed for fast, incremental compilation and easy debugging.

If you'd like evaluate production performance, browser compatibility and code
size, you can enable our release compiler,
[dart2js](https://webdev.dartlang.org/tools/dart2js).

To enable the release compiler, pass in the `--release` flag (or just `-r`).

```console
$ webdev serve -r
```

> Note: Builds may be slower in this configuration.

If you'd like to generate output to disk, we recommend you use `webdev`.

```console
$ webdev build
```

This will create a `build` directory with `index.html`, `main.dart.js` and the
rest of the files needed to run the application using a static HTTP server.

To optimize the output JavaScript, you can enable optimization flags using a
`build.yaml` file in the root of your project with the following contents:

```yaml
# See https://github.com/dart-lang/build/tree/master/build_web_compilers#configuration
targets:
  $default:
    builders:
      build_web_compilers|entrypoint:
        generate_for:
        - web/**.dart
        options:
          dart2js_args:
            - --no-source-maps
            - -O4
```

> Note: the `-O4` option enables a number of advanced optimizations that may
  cause runtime errors in code that has not been thoroughly tested.

## Migrating existing code

If you'd like to migrate existing Flutter code to run on the web preview, read
[the migration guide](https://github.com/flutter/flutter_web/blob/master/docs/migration_guide.md).
# flutter_web_sample
