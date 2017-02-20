# Rachunki bankowe

## Lista rachunków bankowych

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// pobieranie listy rachunków bankowych

$accounts = $api->bankAccounts()->listing();


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

`GET https://api.monetivo.com/v1/bank_accounts`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | Token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Odpowiedź

Klucz | Opis |
----- | ---- |
total | liczba wyników (rachunków bankowych) |
per_page | ilość wyników na stronę |
current_page | bieżąca strona z wynikami
last_page | numer ostatniej strony z wynikami
next_page_url | adres URL do pobrania następnej strony z wynikami
prev_page_url | adres URL do pobrania poprzedniej strony z wynikami
from | wyniki od
to | wyniki do
data | tablica zawierająca wyniki

## Szczegóły rachunku bankowego

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// pobieranie szczegółów rachunku bankowego 1
$identifier = '1';
$account = $api->bankAccounts()->details($identifier);

```

> Przykładowy zwrócony wynik:

```php
Array
(
    [merchant_account_id] => 1
    [account_number] => 60102010260000042270201111
    [name] => Monetivo
    [address] => Botaniczna 8
    [description] => rachunek podstawowy
    [verified_at] =>
    [created_at] =>

    [httpCode] => 200
)
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/bank_accounts/<ID>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
ID | - | tak | identyfikator rachunku bankowego |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika
