# Flutter Repository

[![style: very good analysis][very_good_analysis_badge]][very_good_analysis_link]
[![Powered by Mason](https://img.shields.io/endpoint?url=https%3A%2F%2Ftinyurl.com%2Fmason-badge)](https://github.com/felangel/mason)
[![License: MIT][license_badge]][license_link]

A package aimed at providing seamless integration between the [Repository][repository_package_link] library and Flutter, creating a communication widget between them.

## Installation 💻

**❗ In order to start using Repository Builder you must have the [Flutter SDK][flutter_install_link] installed on your machine.**

Add `repository_flutter` to your `pubspec.yaml`:

```yaml
dependencies:
  repository_flutter:
```

Install it:

```sh
flutter packages get
```

---

## Usage

Lets take a look at how to use RepositoryBuilder to provide a react to state changes in a [Repository][repository_package_link].

### currencies_repository.dart

```dart
class CurrenciesRepository extends CustomHttpRepository<Currencies> {
  @override
  Iterable<Currency> fromJson(json) {
    return RemoteCurrenciesModel.from(
      raw: jsonDecode(json),
    );
  }

  @override
  Uri get endpoint => "https://localhost:8080/api/v1/currency/supported";
}
```

### currencies_page.dart

```dart
class CurrenciesPage extends StatelessWidget {
  const CurrenciesPage();

  final _repository = CurrenciesRepository();

  Widget build(BuildContext context) {
    return Scaffold(
      body: RepositoryBuilder(
        repository: _repository,
        builder: (context, currencies) {
          if (currencies == null) {
            return const Center(
              child: SizedBox(
                child: CircularProgressIndicator(),
              ),
            );
          } else {
            return ListView(
              children: [
                for (currency in currencies)
                  CurrencyListTile(currency: currency)
              ]
            );
          }
        }
      ),
    );
  }
}
```

[dart_install_link]: https://dart.dev/get-dart
[repository_package_link]: https://pub.dev/packages/repository
[flutter_install_link]: https://dart.dev/get-dart
[github_actions_link]: https://docs.github.com/en/actions/learn-github-actions
[license_badge]: https://img.shields.io/badge/license-MIT-blue.svg
[license_link]: https://opensource.org/licenses/MIT
[logo_black]: https://raw.githubusercontent.com/VGVentures/very_good_brand/main/styles/README/vgv_logo_black.png#gh-light-mode-only
[logo_white]: https://raw.githubusercontent.com/VGVentures/very_good_brand/main/styles/README/vgv_logo_white.png#gh-dark-mode-only
[mason_link]: https://github.com/felangel/mason
[very_good_analysis_badge]: https://img.shields.io/badge/style-very_good_analysis-B22C89.svg
[very_good_analysis_link]: https://pub.dev/packages/very_good_analysis
[very_good_coverage_link]: https://github.com/marketplace/actions/very-good-coverage
[very_good_ventures_link]: https://verygood.ventures
[very_good_ventures_link_light]: https://verygood.ventures#gh-light-mode-only
[very_good_ventures_link_dark]: https://verygood.ventures#gh-dark-mode-only
[very_good_workflows_link]: https://github.com/VeryGoodOpenSource/very_good_workflows
