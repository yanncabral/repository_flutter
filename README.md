# Flutter Repository

[![style: very good analysis][very_good_analysis_badge]][very_good_analysis_link]
[![Powered by Mason](https://img.shields.io/endpoint?url=https%3A%2F%2Ftinyurl.com%2Fmason-badge)](https://github.com/felangel/mason)
[![License: MIT][license_badge]][license_link]

A package aimed at providing seamless integration between the repository library and Flutter, creating a communication widget between them.

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

Lets take a look at how to use RepositoryBuilder to provide a react to state changes in a Repository.

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
