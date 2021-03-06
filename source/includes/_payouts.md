# Wypłaty

Funkcjonalność wypłat pozwala na transfer środków z konta Merchanta w systemie Monetivo na konto bankowe.

<aside class="notice">
Do Twojego konta musi być przypisane konto bankowe. Konto to wymaga weryfikacji.
</aside>

## Zlecenie wypłaty

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

<aside class="notice">
Zlecenie wypłaty możliwe jest jedynie w przypadku pozytywnej weryfikacji konta
</aside>

```php
<?php

// autentykacja...

// tworzenie zlecenia wypłaty środków

$account_id = '1';
$payout = $api->payouts()->create($account_id);

// Przykładowy zwrócony wynik:

Array
(
    [identifier] => 1
    [account_number] => 60102010260000042270201111
    [account_name] => Default PLN
    [account_address] => Botaniczna 8, Poznan
    [amount] => 1000.00
    [status] => 1
    [status_history] => Array (

      )
    [account_id] => 1
    [currency] => PLN
    [committed_at] =>

    [httpCode] => 200
)
```

```shell
curl -X "POST" "https://api.monetivo.com/v1/accounts/1/payouts" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
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

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// pobieranie listy wypłat

$payouts = $api->payouts()->listing();

// Przykładowy zwrócony wynik:
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

```shell
curl "https://api.monetivo.com/v1/payouts" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/payouts`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

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

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// pobieranie szczegółów wypłaty o identyfikatorze M12345
$identifier = 'P12345';
$payout = $api->payouts()->details($identifier);

// Przykładowy zwrócony wynik:

Array
(
    [identifier] => 12345
    [account_number] => 60102010260000042270201111
    [account_name] => Default PLN
    [account_address] => Botaniczna 8, Poznan
    [amount] => 1000.00
    [status] => 2
    [status_history] => Array (

      )
    [account_id] => 1
    [currency] => PLN
    [committed_at] =>

    [httpCode] => 200
)
```

```shell
curl "https://api.monetivo.com/v1/payouts/P12345" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
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
