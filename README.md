# Analyzer for Dart

fork dart analyzer-0.40.7 to fix bug https://github.com/dart-lang/sdk/issues/53681

This package provides a library that performs static analysis
of Dart code. It is useful for tool integration and embedding.

End-users should use the [dartanalyzer][] command-line tool
to analyze their Dart code.

Integrators that want to add Dart support to their editor
should use the _Dart Analysis Server_.
The [Analysis Server API Specification][serverapi] is available.
If you are adding Dart support to an editor or IDE, please let us know
by emailing our [list][].

## Configuring the analyzer

Both `dartanalyzer` and Dart Analysis Server can be configured with an
`analysis_options.yaml` file (using an `.analysis_options` file is deprecated).
This YAML file can control which files and paths are analyzed,
which lints are applied, and more.

If you are embedding the analyzer library in your project, you are responsible
for finding the analysis options file, parsing it, and configuring the analyzer.

The analysis options file should live at the root of your project (for example,
next to your `pubspec.yaml`). Different embedders of analyzer, such as
`dartanalyzer` or Dart Analysis Server, may choose to find the file in various
different ways. Consult their documentation to learn more.

Here is an example file that instructs the analyzer to ignore two files:

```yaml
analyzer:
  exclude:
    - test/_data/p4/lib/lib1.dart
    - test/_data/p5/p5.dart
    - test/_data/bad*.dart
    - test/_brokendata/**
```

Note that you can use globs, as defined by the [glob package][glob].

Here is an example file that enables two lint rules:

```yaml
linter:
  rules:
    - camel_case_types
    - empty_constructor_bodies
```

Check out all the available [Dart lint rules][lintrules].

You can combine the `analyzer` section and the `linter` section into a single
configuration. Here is an example:

```yaml
analyzer:
  exclude:
    - test/_data/p4/lib/lib1.dart
linter:
  rules:
    - camel_case_types
```

For more information, see the docs for
[customizing static analysis][custom_analysis].

## Who uses this library?

Many tools embed this library, such as:

* [dartfmt] - a formatter for Dart code
* [dartdoc] - a documentation generator for Dart code
* [Dart Analysis Server][analysis_sever] - a stateful server that supports IDEs and editors

## Support

Post issues and feature requests at https://github.com/dart-lang/sdk/issues

Questions and discussions are welcome at the
[Dart Analyzer Discussion Group][list].

## Background

The APIs in this package were originally machine generated by a translator and were
based on an earlier Java implementation. Several of the API's still look like their Java
predecessors rather than clean Dart APIs.

In addition, there is currently no clean distinction between public and internal
APIs. We plan to address this issue but doing so will, unfortunately, require a
large number of breaking changes. We will try to minimize the pain this causes for
our clients, but some pain is inevitable.

## License

See the [LICENSE] file.

[serverapi]: https://htmlpreview.github.io/?https://github.com/dart-lang/sdk/blob/master/pkg/analysis_server/doc/api.html
[dartanalyzer]: https://github.com/dart-lang/sdk/tree/master/pkg/analyzer_cli#dartanalyzer
[list]: https://groups.google.com/a/dartlang.org/forum/#!forum/analyzer-discuss
[lintrules]: https://dart-lang.github.io/linter/lints/
[glob]: https://pub.dev/packages/glob
[LICENSE]: https://github.com/dart-lang/sdk/blob/master/pkg/analyzer/LICENSE
[dartfmt]: https://github.com/dart-lang/dart_style
[dartdoc]: https://github.com/dart-lang/dartdoc
[analysis_sever]: https://github.com/dart-lang/sdk/tree/master/pkg/analysis_server
[custom_analysis]: https://dart.dev/guides/language/analysis-options
