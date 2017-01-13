# Wypłaty

Funkcjonalność wypłat pozwala na transfer środków z konta Merchanta w systemie Monetivo na konto bankowe.

<aside class="notice">
Do Twojego konta musi być przypisane konto bankowe. Konto to wymaga weryfikacji.
</aside>

## Zlecenie wypłaty

```php
<?php

// autentykacja...

// tworzenie zlecenia wypłaty środków

$account_id = 'M12345';
$payout = $api->payouts()->create($account_id);


```

> Przykładowy zwrócony wynik:

```php
Array
(
    [identifier] => 1
    [account_number] => 60102010260000042270201111
    [account_name] => Default PLN
    [account_address] => Botaniczna 8, Poznan
    [amount] => 1000.00
    [status] => 60102010260000042270201111
    [status_history] => Array (

      )
    [account_id] => 1
    [currency] => PLN
    [committed_at] =>

    [httpCode] => 200
)
```

### Żądanie HTTP

`POST https://api.monetivo.com/v1/accounts/<ACCOUNT_ID>/payouts`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
ACCOUNT_ID | - | tak | identyfikator rachunku w systemie Monetivo |

### Odpowiedź

Klucz | Opis |
----- | ---- |
identifier | identyfikator wypłaty |
account_number | numer rachunku bankowego na który zlecono wypłatę |
account_name | nazwa odbiorcy płatności
account_address | adres odbiorcy płatności
amount | kwota
status | status, patrz niżej
status_history | historia zmiana statusu
account_id | identyfikator rachunku w systemie Monetivo
currency | waluta
committed_at | data wykonania

### Statusy wypłaty

Wartość | Opis |
----- | ---- |
1 | nowa wypłata, status początkowy
4 | zlecenie wypłaty przekazane do banku

<aside class="notice">
Kwota wypłaty <code>amount</code> jest równa kwocie środków na rachunku w systemie Monetivo pomniejszonej o prowizje.
</aside>

## Lista wypłat

```php
<?php

// autentykacja...

// pobieranie listy wypłat

$payouts = $api->payouts()->list();


```

> Przykładowy zwrócony wynik:

```php
Array
(
    [total] => 0
    [per_page] => 15
    [current_page] => 1
    [last_page] => 0
    [next_page_url] =>
    [prev_page_url] =>
    [from] =>
    [to] =>
    [data] => Array
        (
        )

    [httpCode] => 200
)
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/payouts`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
ACCOUNT_ID | - | tak | identyfikator rachunku w systemie Monetivo |

### Odpowiedź

Klucz | Opis |
----- | ---- |
total | liczba wyników (wypłat) |
per_page | ilość wyników na stronę |
current_page | bieżąca strona z wynikami
last_page | numer ostatniej strony z wynikami
next_page_url | adres URL do pobrania następnej strony z wynikami
prev_page_url | adres URL do pobrania poprzedniej strony z wynikami
from | wyniki od
to | wyniki do
data | tablica zawierająca wyniki

## Szczegóły wypłaty

```php
<?php

// autentykacja...

// pobieranie szczegółów wypłaty o identyfikatorze M12345
$identifier = 'M12345';
$payout = $api->payouts()->details($identifier);

```

> Przykładowy zwrócony wynik:

```php
Array
(
    [identifier] => 1
    [account_number] => 60102010260000042270201111
    [account_name] => Default PLN
    [account_address] => Botaniczna 8, Poznan
    [amount] => 1000.00
    [status] => 60102010260000042270201111
    [status_history] => Array (

      )
    [account_id] => 1
    [currency] => PLN
    [committed_at] =>

    [httpCode] => 200
)
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/payouts/<PAYOUT_ID>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
PAYOUT_ID | - | tak | identyfikator wypłaty |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Odpowiedź

Klucz | Opis |
----- | ---- |
identifier | identyfikator wypłaty |
account_number | numer rachunku bankowego na który zlecono wypłatę |
account_name | nazwa odbiorcy płatności
account_address | adres odbiorcy płatności
amount | kwota
status | status, patrz niżej
status_history | historia zmiana statusu
account_id | identyfikator rachunku w systemie Monetivo
currency | waluta
committed_at | data wykonania
