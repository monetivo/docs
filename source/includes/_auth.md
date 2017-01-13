# Autentykacja

Dostęp do API wymaga autentykacji (zalogowania). Do autentykacji potrzebne są:

- login (podawany podczas rejestracji),
- hasło (podawane podczas rejestracji),
- token aplikacji (uzyskiwany po rejestracji).

Po pomyślnej autentykacji zostanie zwrócony token, który jest niezbędny do wykonywania zapytań do API. Nasza biblioteka automatycznie dołączy token do każdego zapytania w postaci nagłówka.

Każdy błąd, zarówno po stronie klienta API jak i systemu Monetivo, sygnalizowany jest wyrzuceniem wyjątku `MonetivoException`
Instancja wyjątku w większości przypadków zawiera także dodatkowe przydatne informacje.

<aside class="notice">
Dane dostępowe do API dostępne są po zalogowaniu do <a href="https://getcomposer.org/doc/00-intro.md">Panelu Merchanta</a> w systemie Monetivo
</aside>

### Żądanie HTTP

`POST https://api.monetivo.com/v1/auth/login`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji

### Parametry żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
login | - | tak | login merchanta |
password | - | tak | hasło merchanta |

### Odpowiedź

Klucz | Opis |
----- | ---- |
token | token użytkownika, do wykorzystania w nagłówku X-Auth-Token |

> Przykładowa autentykacja:

```php
<?php

// ładowanie biblioteki za pośrednictwem Composer
require __DIR__.'/vendor/autoload.php';

try {
    // token aplikacji
    $app_token = 'tokenaplikacji';

    // login merchanta
    $login = 'merchant_test_12345';

    // hasło merchanta
    $password = 'very_strong_password';

    // inicjalizacja biblioteki
    $api = new \Monetivo\MerchantApi($app_token);

    // autentykacja; jeśli wystąpi błąd to zostanie wyrzucony wyjątek MonetivoException
    $token = $api->auth($login, $password);

    // następne zapytania do API
}
catch(Monetivo\Exceptions\MonetivoException $e) {
  echo $e->getHttpCode(); // wyświetla kod odpowiedzi serwera;
  echo $e->getResponse(); // zawiera odpowiedź serwera
}
```

> Zmienna `$token` zawiera token autoryzacyjny. Jego ważność to 15 minut.

> Pamiętaj, że autentykację wywołujesz jednokrotnie
