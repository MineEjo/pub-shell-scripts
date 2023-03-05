## Generate pubspec.yaml in Dart code

**Idea:** to implement a simple way to get data from `pubspec.yaml`, as simple as importing `package.json`

### Example

Let's take some of the data from the config as an example.

```yaml
name: package
description: Hello world! # Example of no formatting and no commentary.
environment:
  sdk: '>=2.17.6 <3.0.0'
# Example of commentary and strange formatting.

platforms:
  web:

# Example commentary.

dev_dependencies:
  dep1: ^1.2.3
  dep2: ^2.3.4
```

After running the script, you will get a generated class with data.

```dart
/// Don't change this file or class, it's generated! Contains data from pubspec.yaml.
/// * The usual fields are the name from the config and the [String] type.
/// * Arrays and the like are maps with a [String] key and a [dynamic] value.
/// * All keys try to have a [String] value, the exception is a key without a value, it will have a [bool] value.
class PackagePubspec {
  static const String description = 'Hello world!';
  static const Map<String, dynamic> environment = {'sdk': '>=2.17.6 <3.0.0'};
  static const Map<String, dynamic> platforms = {'web:': true};
  static const Map<String, dynamic> devDependencies = {
    'dep1': '^1.2.3',
    'dep2': '^2.3.4'
  };
}
```

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
<br>Before publishing it will generate a file in package/lib - pubspec.dart.
<br>If you have questions about customized publishing, go to the [beginning of the repository](../README.md).

```yaml
  publish:
    steps:
      # Add this as a must before you publish it.
      - run: curl -s https://raw.githubusercontent.com/MineEjo/pub-shell-scripts/master/gen_pubspec_dart/gen_pubspec_dart.sh | bash /dev/stdin ./pubspec.yaml ./lib/pubspec.dart
      - name: Publish
        run: dart pub publish --force
```
