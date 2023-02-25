## Generate pubspec.yaml in Dart code

**Idea:** to implement a simple way to get data from `pubspec.yaml`, as simple as importing `package.json`

### Setup

**Shell:**

To run the script from the repository, install curl, but it is usually there by default.

```shell
$ curl -s https://raw.githubusercontent.com/MineEjo/pub-shell-scripts/master/gen_pubspec_dart/gen_pubspec_dart.sh | bash /dev/stdin ./pubspec.yaml ./lib/pubspec.dart
```

**Shell local:**

This will run the script if you write the command in the directory with the script, but if you update in the repository, you will have to update it manually.

```shell
$ bash gen_pubspec_dart.sh ./pubspec.yaml ./lib/pubspec.dart
```

**Workflow:** `.github/workflows/publish.yml`
<br>Before publishing it will generate a file in package/lib - pubspeck.dart.
<br>If you have questions about customized publishing, go to the [beginning of the repository](../README.md).

```yaml
  publish:
    steps:
      # Add this as a must before you publish it.
      - run: curl -s https://raw.githubusercontent.com/MineEjo/pub-shell-scripts/master/gen_pubspec_dart/gen_pubspec_dart.sh | bash /dev/stdin ./pubspec.yaml ./lib/pubspec.dart
      - name: Publish
        run: dart pub publish --force
```
