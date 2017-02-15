# Biblioteki

## PHP

Biblioteka `MerchantAPI PHP` umożliwia integrację oprogramowania napisanego w języku PHP z systemem Monetivo.

<aside class="notice">
Nie musisz wykorzystywać udostępnianych przez nas bibliotek. Jest to jedynie ułatwienie. Możesz samodzielnie wysyłać zapytania HTTP do API.
</aside>

### Wymagania systemowe

- PHP w wersji 5.5 lub wyższej,
- zainstalowane rozszerzenie PHP cURL

### Instalacja

1. Standardowa - przy użyciu Composer:

`composer require monetivo/monetivo-php`
jeśli Composer nie został zainstalowany globalnie:

`php composer.phar require monetivo/monetivo-php`

2. Niestandardowa - przy użyciu archiwum z biblioteką:
  - rozpakowanie archiwum do dowolnego folderu,
  - dołączenie pliku autoload.php z zachowaniem odpowiedniej ścieżki:

    `require '<ścieżka do pliku autoload.php>';`

<aside class="notice">
Zobacz sekcję <a href="https://getcomposer.org/doc/00-intro.md">Getting Started</a> w dokumentacji Composer by poznać szczegóły korzystania z tego narzędzia
</aside>
