# POS

POS to punkt sprzedaży, np. Twój sklep internetowy. Możesz posiadać wiele POS-ów, które są przypisane do Twojego konta merchanta. Każdy POS posiada szereg ustawień, w tym adres URL na który będą przychodzić powiadomienia o zmianie statusu transakcji
POS posiada swój identyfikator, który jest niezbędny do stworzenia transakcji.

## Tworzenie POS

```php
<?php

// autentykacja...

// pobieranie listy POS
$params = ['name' => 'My shop', 'url' => 'https://myshop.example.com', 'contact_id' => 1];
$transactions = $api->pos()->create($params);

// Przykładowy zwrócony wynik:
Array
(
    [pos_id] => 1
    [name] => Monetivo
    [url] => https://monetivo.com
    [contact_user] => Array
        (
            [name] => John
            [email] => hello@monetivo.com
            [phone] => +48123456789
            [title] => Mr
            [surname] => Doe
        )

    [enabled] => 1
    [parameters] => Array
        (
            [url_notify] => https://monetivo.com/notify
        )

    [created_at] => 2016-12-09T12:24:15+0000
    [updated_at] => 2016-12-09T12:24:15+0000
    [httpCode] => 200
)
```

```shell
curl -X "POST" "https://api.monetivo.com/v1/pos" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
     --data-urlencode "name=My Shop" \
     --data-urlencode "url=https://myshop.example.com" \
     --data-urlencode "contact_id=1"
```

### Żądanie HTTP

`POST https://api.monetivo.com/v1/pos`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Parametry żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
name | - | tak | nazwa POS (unikalna)
url | - | tak | adres URL POS
contact_id | - | tak | ID osoby kontaktowej

### Odpowiedź

Klucz | Opis |
----- | ---- |
pos_id | identyfikator POS |
name | nazwa POS |
url | adres URL POS
contact_user[name] | imię osoby kontaktowej
contact_user[surname] | nazwisko osoby kontaktowej
contact_user[email] | adres email osoby kontaktowej
contact_user[phone] | telefon osoby kontaktowej
contact_user[title] | tytuł służbowy osoby kontaktowej
enabled | POS aktywny
parameters[url_notify] | adres URL do wysyłania powiadomień o zmianie statusu transakcji
created_at | data utworzenia
updated_at | data ostatniej edycji

## Lista POS

```php
<?php

// autentykacja...

// pobieranie listy POS

$transactions = $api->pos()->listing();

// Przykładowy zwrócony wynik:
Array
(
    [total] => 1
    [per_page] => 15
    [current_page] => 1
    [last_page] => 1
    [next_page_url] =>
    [prev_page_url] =>
    [from] => 1
    [to] => 1
    [data] => Array
        (
            [0] => Array
                (
                    [pos_id] => 1
                    [name] => Monetivo
                    [url] => https://monetivo.com
                    [contact_user] => Array
                        (
                            [name] => John
                            [email] => hello@monetivo.com
                            [phone] => +48123456789
                            [title] => Mr
                            [surname] => Doe
                        )

                    [enabled] => 1
                    [parameters] => Array
                        (
                            [url_notify] => https://monetivo.com/notify
                        )

                    [created_at] => 2016-12-09T12:24:15+0000
                    [updated_at] => 2016-12-09T12:24:15+0000
                )

        )

    [httpCode] => 200
)
```

```shell
curl "https://api.monetivo.com/v1/pos" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/pos`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Parametry żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
sort | asc | nie | kolejność sortowania: asc (od najstarszego), desc (od najnowszego)
orderby | - | nie | kolumna sortowania, patrz niżej
per_page | - | nie | ilość wyników na stronę

### Kolumny sortowania

Kolumna | Opis |
------- | ----  |
updated_at | data zmiany statusu
created_at | data utworzenia
pos_id | sortowanie po identyfikatorze POS

### Odpowiedź

Klucz | Opis |
----- | ---- |
total | liczba wyników (POS) |
per_page | ilość wyników na stronę |
current_page | bieżąca strona z wynikami
last_page | numer ostatniej strony z wynikami
next_page_url | adres URL do pobrania następnej strony z wynikami
prev_page_url | adres URL do pobrania poprzedniej strony z wynikami
from | wyniki od
to | wyniki do
data | tablica zawierająca wyniki

### POS

Klucz | Opis |
----- | ---- |
pos_id | identyfikator POS |
name | nazwa POS |
url | adres URL POS
contact_user[name] | imię osoby kontaktowej
contact_user[surname] | nazwisko osoby kontaktowej
contact_user[email] | adres email osoby kontaktowej
contact_user[phone] | telefon osoby kontaktowej
contact_user[title] | tytuł służbowy osoby kontaktowej
enabled | POS aktywny
parameters[url_notify] | adres URL do wysyłania powiadomień o zmianie statusu transakcji
created_at | data utworzenia
updated_at | data ostatniej edycji


## Szczegóły POS

```php
<?php

// autentykacja...

// pobieranie szczegółów POS o identyfikatorze 1
$identifier = '1';
$transaction = $api->pos()->details($identifier);

// Przykładowy zwrócony wynik:

Array
(
    [pos_id] => 1
    [name] => Monetivo
    [url] => https://monetivo.com
    [contact_user] => Array
        (
            [name] => John
            [email] => hello@monetivo.com
            [phone] => +48123456789
            [title] => Mr
            [surname] => Doe
        )

    [enabled] => 1
    [parameters] => Array
        (
            [url_notify] => https://monetivo.com/notify
        )

    [created_at] => 2016-12-09T12:24:15+0000
    [updated_at] => 2016-12-09T12:24:15+0000
)
```

```shell
curl "https://api.monetivo.com/v1/pos/1" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/pos/<POS_ID>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
POS_ID | - | tak | identyfikator POS |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### POS

Klucz | Opis |
----- | ---- |
pos_id | identyfikator POS |
name | nazwa POS |
url | adres URL POS
contact_user[name] | imię osoby kontaktowej
contact_user[surname] | nazwisko osoby kontaktowej
contact_user[email] | adres email osoby kontaktowej
contact_user[phone] | telefon osoby kontaktowej
contact_user[title] | tytuł służbowy osoby kontaktowej
enabled | POS aktywny
parameters[url_notify] | adres URL do wysyłania powiadomień o zmianie statusu transakcji
created_at | data utworzenia
updated_at | data ostatniej edycji

## Listowanie rachunków przypisanych do POS

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// pobieranie rachunków przypisanych do POS o identyfikatorze 1
$identifier = '1';
$transaction = $api->pos()->accounts($identifier);

// Przykładowy zwrócony wynik:

Array
(
    [total] => 1
    [per_page] => 15
    [current_page] => 1
    [last_page] => 1
    [next_page_url] =>
    [prev_page_url] =>
    [from] => 1
    [to] => 1
    [data] => Array
        (
            [0] => Array
                (
                    [account_id] => 1
                    [pos_id] => 1
                    [currency] => PLN
                    [created_at] => 2016-12-09T13:24:15+0100
                )

        )

    [httpCode] => 200
)
```

```shell
curl "https://api.monetivo.com/v1/pos/1/accounts" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/pos/<POS_ID>/accounts`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
POS_ID | - | tak | identyfikator POS |

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

## Przypisanie rachunku do POS

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

<aside class="notice">
Do POS można przypisać nie więcej niż jeden rachunek z daną walutą
</aside>

```php
<?php

// autentykacja...

// przypisanie rachunku o identyfikatorze 4 do POS o identyfikatorze 1
$pos_identifier = '1';
$account_identifier = '4';
$transaction = $api->pos()->bindAccount($pos_identifier, $account_identifier);

// Przykładowy zwrócony wynik:

Array
(
    [total] => 1
    [per_page] => 15
    [current_page] => 1
    [last_page] => 1
    [next_page_url] =>
    [prev_page_url] =>
    [from] => 1
    [to] => 1
    [data] => Array
        (
            [0] => Array
                (
                    [account_id] => 4
                    [pos_id] => 1
                    [currency] => PLN
                    [created_at] => 2016-12-09T13:24:15+0100
                )

        )

    [httpCode] => 200
)
```

```shell
curl -X "POST" "https://api.monetivo.com/v1/pos/1/accounts/4" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`POST https://api.monetivo.com/v1/pos/<POS_ID>/accounts/<ACCOUNT_ID>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
POS_ID | - | tak | identyfikator POS |
ACCOUNT_ID | - | tak | identyfikator rachunku |

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

## Usunięcie przypisania rachunku do POS

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// przypisanie rachunku o identyfikatorze 4 do POS o identyfikatorze 1
$pos_identifier = '1';
$account_identifier = '4';
$transaction = $api->pos()->unbindAccount($pos_identifier, $account_identifier);

// Przykładowy zwrócony wynik:

Array
(
    [total] => 1
    [per_page] => 15
    [current_page] => 1
    [last_page] => 1
    [next_page_url] =>
    [prev_page_url] =>
    [from] => 1
    [to] => 1
    [data] => Array
        (
            [0] => Array
                (
                    [account_id] => 4
                    [pos_id] => 1
                    [currency] => PLN
                    [created_at] => 2016-12-09T13:24:15+0100
                )

        )

    [httpCode] => 200
)
```

```shell
curl -X "DELETE" "https://api.monetivo.com/v1/pos/1/accounts/4" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`DELETE https://api.monetivo.com/v1/pos/<POS_ID>/accounts/<ACCOUNT_ID>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
POS_ID | - | tak | identyfikator POS |
ACCOUNT_ID | - | tak | identyfikator rachunku |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika
