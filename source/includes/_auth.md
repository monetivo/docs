# Autentykacja

Dostęp do API wymaga autentykacji (zalogowania). Do autentykacji potrzebne są:

- login (podawany podczas rejestracji),
- hasło (podawane podczas rejestracji),
- token aplikacji (uzyskiwany po rejestracji).

Po pomyślnej autentykacji zostanie zwrócony token, który jest niezbędny do wykonywania zapytań do API. Nasza biblioteka automatycznie dołączy token do każdego zapytania w postaci nagłówka. Każdy błąd, zarówno po stronie klienta API jak i systemu Monetivo, sygnalizowany jest wyrzuceniem wyjątku `MonetivoException`. Instancja wyjątku w większości przypadków zawiera także dodatkowe przydatne informacje.

<aside class="notice">
Zwróć uwagę, że token aplikacji zawiera prefix <code>test_</code> dla środowiska testowego albo <code>prod_</code> dla środowiska produkcyjnego. Prefiksy te pozwolą Ci łatwo odróżnić do jakiego środowiska został przypisany zestaw danych (login, hasło, token aplikacji). Zestaw danych dla środowiska testowego nie może być użyty w środowisku produkcyjnym i odwrotnie. Nasze oficjalne biblioteki oraz wtyczki integracji automatycznie ustawiają docelowe środowisko na podstawie wprowadzonego tokenu.
</aside>

<aside class="notice">
Dane dostępowe do API dostępne są po zalogowaniu do <a href="https://merchant.monetivo.com">Panelu Merchanta</a> w systemie Monetivo
</aside>

<aside class="notice">
Dane dostępowe są przypisane do użytkownika specjalnie utworzonego na potrzeby integracji. Użytkownik ten posiada zmniejszoną ilość uprawnień co ogranicza dostęp do Panelu Merchanta. Większy zakres uprawnień przypisany jest do Użytkownika administracyjnego. Dokumentacja szczegółowo opisuje przypadki, gdy uprawnienia użytkownika integracji są niewystarczające i operacji należy dokonać jako użytkownik administracyjny. Sposób logowania użytkownika administracynego jest identyczny jak w przypadku użytkownika integracji.
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
    // zmienna `$token` zawiera token autoryzacyjny. Jego ważność to 15 minut.
    $token = $api->auth($login, $password);

    // następne zapytania do API
}
catch(Monetivo\Exceptions\MonetivoException $e) {
  echo $e->getHttpCode(); // wyświetla kod odpowiedzi serwera;
  echo $e->getResponse(); // zawiera odpowiedź serwera
}
```

```shell
curl -X "POST" "https://api.monetivo.com/v1/auth/login \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8" \
     --data-urlencode "login=1GE" \
     --data-urlencode "password=37855xb46d9x478fexxx"
```

> Pamiętaj, że autentykację wywołujesz jednokrotnie, a przy kolejnych zapytaniach do API posługujesz się odebranym tokenem
