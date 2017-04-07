# Rachunki

## Tworzenie rachunku

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

 $params = array(
             'currency' => 'PLN',
             'name' => 'Rachunek testowy'
         );
 $transaction = $api->accounts()->create($params);

//Przykładowy zwrócony wynik:

Array
(
    [account_id] => 2
    [currency] => PLN
    [balance] => 0.00
    [name] => Rachunek testowy
    [created_at] => 2016-12-09T12:24:15+0000
    [updated_at] => 2017-01-03T15:18:41+0000
    [httpCode] => 200
)
```

```shell
curl -X "POST" "https://api.monetivo.com/v1/accounts" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8" \
     --data-urlencode "currency=EUR" \
     --data-urlencode "name=Rachunek EUR"
```

### Żądanie HTTP

`POST https://api.monetivo.com/v1/accounts`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | --- |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Parametry żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
currency | - | tak | waluta rachunku
name | - | nie | nazwa rachunku

### Odpowiedź

Klucz | Opis |
----- | ---- |
account_id | identyfikator rachunku |
currency | waluta |
balance | saldo na rachunku
name | nazwa rachunku
created_at | data utworzenia rachunku
updated_at | data aktualizacji rachunku

## Lista rachunków

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// pobieranie listy rachunków

$accounts = $api->accounts()->listing();

// Przykładowy zwrócony wynik:

Array
(
    [total] => 2
    [per_page] => 15
    [current_page] => 1
    [last_page] => 1
    [next_page_url] =>
    [prev_page_url] =>
    [from] => 1
    [to] => 2
    [data] => Array
        (
            [0] => Array
                (
                    [account_id] => 2
                    [currency] => PLN
                    [balance] => 0.00
                    [name] => second PLN
                    [created_at] => 2016-12-15T15:15:00+0000
                    [updated_at] => 2016-12-15T15:15:00+0000
                )

            [1] => Array
                (
                    [account_id] => 1
                    [currency] => PLN
                    [balance] => 6337.54
                    [name] => Default PLN
                    [created_at] => 2016-12-09T12:24:15+0000
                    [updated_at] => 2017-01-03T15:18:41+0000
                )

        )

    [httpCode] => 200
)
```

```shell
curl "https://api.monetivo.com/v1/accounts" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QxLCJhbGciOiJIUzI1NiJ9.eyJpcCI6IjE3Mi4yMC4wLjEiLCJpc3MxOiJDUk9XRENPTU1VTklUWSIsIxV4cCI6MTQ5MTQ3ODxxMCwiZ2VuIjoxNDkxNDc4MDAwLCJ1c2VyX2lkIjoxfQ.QG8CU-4oZYueaDxnvWOGOYFa2DLD9mJ5zKMS7tcAeJ8" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/accounts`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Odpowiedź

Klucz | Opis |
----- | ---- |
total | liczba wyników (rachunków) |
per_page | ilość wyników na stronę |
current_page | bieżąca strona z wynikami
last_page | numer ostatniej strony z wynikami
next_page_url | adres URL do pobrania następnej strony z wynikami
prev_page_url | adres URL do pobrania poprzedniej strony z wynikami
from | wyniki od
to | wyniki do
data | tablica zawierająca wyniki

## Szczegóły rachunku

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// pobieranie szczegółów rachunku 1
$identifier = '1';
$account = $api->accounts()->details($identifier);

// Przykładowy zwrócony wynik:

Array
(
    [account_id] => 1
    [currency] => PLN
    [balance] => 6337.54
    [name] => Default PLN
    [created_at] => 2016-12-09T12:24:15+0000
    [updated_at] => 2017-01-03T15:18:41+0000
    [httpCode] => 200
)
```

```shell
curl "https://api.monetivo.com/v1/accounts/1" \
     -H "X-Auth-Token: exJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpcCI6IxE3Mi4yMC4wLjEiLCJpc3MiOiJDUkxXRENPTU1VTklUWSIsImV4cCI6MTQ5MTQ4MDUwNixiZ2VuIjoxNDkxNDc5NjA2LCJ1c2VyX2lkIjoxfQ.wznV8luouhZXWOPLAyxXfsFrgo4N9mrq0Rz81hm48Pc" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/accounts/<ID>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
ID | - | tak | identyfikator rachunku |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Odpowiedź

Klucz | Opis |
----- | ---- |
account_id | identyfikator rachunku |
currency | waluta |
balance | saldo na rachunku
name | nazwa rachunku
created_at | data utworzenia rachunku
updated_at | data aktualizacji rachunku

## Raport rachunku

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// pobieranie raportu z listą transakcji z rachunku 1 od dnia 2016-12-01

$report = $api->accounts()->report(1, \Monetivo\Api\Accounts::REPORT_TRANSACTIONS, ['date_from' => '2016-12-01']);

// Przykładowy zwrócony wynik:

Array
(
    [total] => 10
    [per_page] => 5
    [current_page] => 1
    [last_page] => 2
    [next_page_url] => https://api.monetivo.com/v1/accounts/1/report?page=2
    [prev_page_url] =>
    [from] => 1
    [to] => 15
    [data] => Array
        (
            [0] => Array
                (
                    [object_type] => 2
                    [amount] => 33.00
                    [currency] => PLN
                    [balance] => 6085.71
                    [operation_type] => 12
                    [operation_data] => Array
                        (
                            [name] => Jan Kowalski
                            [email] => jk@example.com
                            [order_id] => 7a085d21-xxxx-xxxx-xxxx-f5d8cef86636
                        )

                    [offer] => Array
                        (
                            [commission] => 0.36
                            [commission_rate] => 1.10
                            [commission_const] => 0.00
                        )

                    [identifier] => M8MXXXX
                    [created_at] => 2017-01-02T08:16:53+0000
                )

            [1] => Array
                (
                    [object_type] => 2
                    [amount] => -0.36
                    [currency] => PLN
                    [balance] => 6085.35
                    [operation_type] => 10
                    [operation_data] =>
                    [offer] =>
                    [identifier] => M8MXXXX
                    [created_at] => 2017-01-02T08:16:53+0000
                )

            [2] => Array
                (
                    [object_type] => 2
                    [amount] => 1.00
                    [currency] => PLN
                    [balance] => 6086.35
                    [operation_type] => 12
                    [operation_data] => Array
                        (
                            [name] => Anna Nowak
                            [email] => an@example.com
                            [order_id] => 2b20c8b7-xxxx-xxxx-xxxx-21fb52710f79
                        )

                    [offer] => Array
                        (
                            [commission] => 0.01
                            [commission_rate] => 1.10
                            [commission_const] => 0.00
                        )

                    [identifier] => M0LXXXX
                    [created_at] => 2017-01-02T15:00:49+0000
                )

            [3] => Array
                (
                    [object_type] => 2
                    [amount] => -0.01
                    [currency] => PLN
                    [balance] => 6086.34
                    [operation_type] => 10
                    [operation_data] =>
                    [offer] =>
                    [identifier] => M0LXXXX
                    [created_at] => 2017-01-02T15:00:49+0000
                )

            [4] => Array
                (
                    [object_type] => 2
                    [amount] => 1.00
                    [currency] => PLN
                    [balance] => 6087.34
                    [operation_type] => 12
                    [operation_data] => Array
                        (
                            [name] => J. Sobechuck
                            [email] => sopel2k@example.com
                            [order_id] => c900a485-xxxx-xxxx-xxxx-6112598fa0d9
                        )

                    [offer] => Array
                        (
                            [commission] => 0.01
                            [commission_rate] => 1.10
                            [commission_const] => 0.00
                        )

                    [identifier] => M0WXXXX
                    [created_at] => 2017-01-02T16:13:42+0000
                )

            [5] => Array
                (
                    [object_type] => 2
                    [amount] => -0.01
                    [currency] => PLN
                    [balance] => 6087.33
                    [operation_type] => 10
                    [operation_data] =>
                    [offer] =>
                    [identifier] => M0WXXXX
                    [created_at] => 2017-01-02T16:13:42+0000
                )
        )

    [httpCode] => 200
)
```

```shell
curl "https://api.monetivo.com/v1/accounts/3/report?type=2" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpcCI6IjE3Mi4yMC4wLjEiLCJpc3MiOiJDUk9XRENPTU1VTklUWSIsImV4cCI6MTQ5MTQ4MDUwNiwiZ2VuIjoxNDkxNDc5NjA2LCJ1c2VyX2lkIjoxfQ.wznV8luouhZXWOPLAypXfsFrgo4N9mrq0Rz81hm48Pc" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

> Wyniki posortowane są po identyfikatorze operacji

### Żądanie HTTP

`GET https://api.monetivo.com/v1/accounts/<ID>/report?type=<TYPE>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
ID | - | tak | identyfikator rachunku |
TYPE | - | tak | typ raportu (patrz poniżej); można określić wiele typów poprzez rozdzielenie przecinkiem |
date_from | - | nie | data od |
date_to | - | nie | data do |
order | asc | nie | kolejność sortowania: asc (od najstarszej), desc (od najnowszej)
offset | - | nie | pomiń x wyników
limit | - | nie | limit ilości zwracanych wyników

### Obsługiwane typy raportów:

Typ  | Opis |
-------- | ---  |
1 | wypłaty |  
2 | transakcje |  
4 | zwroty |   
32 | obciążenia |  

### Pozycja raportu
Klucz | Opis
----- | ---- |
object_type | typ operacji
amount | kwota operacji
currency | waluta
balance | saldo po operacji
operation_data | szczegóły operacji
offer | szczegóły zastosowanej oferty
identifier | identyfikator powiązanego obiektu
created_at  | data utworzenia pozycji

<aside class="notice">
Typy obiektów wyszczególnione w raporcie <code>object_type</code> są tożsame z typem raportu.
</aside>
