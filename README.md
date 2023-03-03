## List

* [Generate pubspec.yaml in Dart code](./gen_pubspec_dart)
* [Testing Dart code: browser support](./test_dart_code)
* [Automatic code formatting](./format_dart_code)


## Introduction

**Useful** ideas and concepts for [pub.dev](https://pub.dev/) or `pubspec` files implemented with shell scripts.

* The scripts do not have to be downloaded or added locally, you can run them via `curl`, see the script
  instructions for more details.
* The individual scripts are sorted into folders and have their own launch instructions, github actions, etc.

### Pub.dev workflow

[Pub.dev] allows you to [automatically publish] a package when it is released, so scripts generate something before publishing the package. The following is a standard example which currently works for custom publishing.

[Pub.dev]: https://pub.dev/
[automatically publish]: https://dart.dev/tools/pub/automated-publishing

```yaml
name: Publish to pub.dev

on:
  push:
    tags:
      # The tag format can be changed.
      - '[0-9]+.[0-9]+.[0-9]+*'

jobs:
  publish:
    permissions:
      id-token: write # This is required for authentication using OIDC
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: dart-lang/setup-dart@v1
      - name: Install dependencies
        run: dart pub get
      # Here you can insert custom steps you need
      # - run: script
      - name: Publish
        run: dart pub publish --force
```

## Contribution
Please make sure to read the [Contributing Guide](.github/CONTRIBUTING.md) before making a pull request.

## License

[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2022-present, MineEjo
