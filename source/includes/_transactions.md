# Transakcje

## Tworzenie transakcji

```php
<?php

// autentykacja...

 $params = array(
             'order_data' => [
                 'description' => 'Christmas gifts',
                 'order_id' => '12345'
                 ],
             'buyer' => [
                 'name' => 'John Smith',
                 'email' =>  'js@example.com'
                 ],
             'language' => 'pl',
             'currency' => 'PLN',
             'amount' => '150.00',
             'return_url' => 'https://example.com/thanks'
         );
 $transaction = $api->transactions()->create($params);

// Przykładowy zwrócony wynik
Array
(
    [pos_id] => 1
    [amount] => 17.50
    [language] => pl
    [currency] => PLN
    [buyer] => Array
        (
            [name] => John Smith
            [email] => john@example.com
        )

    [order_data] => Array
        (
            [description] => Opis testowy
            [order_id] => 403a6047-4798-4f1e-a93c-xxxxxxxxxxxx
        )

    [return_url] => http://example.com
    [status_history] => Array
        (
        )

    [updated_at] => 2016-12-22T11:00:22+0000
    [created_at] => 2016-12-22T11:00:22+0000
    [identifier] => XXXXXXX
    [sign] => daa31f723b855af6cc4ff274fe0dxxxxxxxxxxxx
    [redirect_url] => https://secure.monetivo.com/pay/XXXXXXX/daa31f723b855af6cc4ff274fe0dxxxxxxxxxxxx
    [httpCode] => 200
)
```

```shell
curl -X "POST" "https://api.monetivo.com/v1/transactions" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8" \
     --data-urlencode "amount=120.00" \
     --data-urlencode "return_url=https://example.com/thankyou" \
     --data-urlencode "order_data[description]=Testowy opis zamówienia" \
     --data-urlencode "buyer[email]=jkowalski@example.com" \
     --data-urlencode "language=PL" \
     --data-urlencode "currency=PLN" \
     --data-urlencode "order_data[order_id]=MYSHOP-12345" \
     --data-urlencode "buyer[name]=Jan Kowalski"
```

### Żądanie HTTP

`POST https://api.monetivo.com/v1/transactions`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | --- |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Parametry żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
order_data[description] | - | tak | Opis zamówienia |
order_data[order_id] | - | tak | Dodatkowy identyfikator zamówienia (dowolna treść zdefiniowana przez merchanta) |
buyer[name] | - | tak | nazwa kupującego|
buyer[email] | - | tak | email kupującego|
language | - | tak | język, którym posługuje się Kupujący
currency | - | tak | waluta, dowolna spośród: PLN
amount | - | tak | kwota zamówienia
channel_id | - | nie | identyfikator kanału płatności, zdefiniowanie powoduje wymuszenie dokonania płatności poprzez wskazany kanał bez uprzedniej możliwości wyboru przez Kupującego
accept_terms | - | tak, jeśli channel_id jest zdefiniowany | informacja, że Kupujący zaakceptował regulamin płatności systemu Monetivo; dozwolona wartość: 1
return_url | - | tak | adres powrotny (URL) do przekierowania
notify_url | taki jak dla POS | nie | adres URL po stronie Merchanta na który zostanie wysłane powiadomienie o zmianie statusu transakcji w systemie Monetivo

<aside class="notice">
Dostępne wartości dla parametru <code>language</code> to: <code>pl</code>, <code>en</code>. Wybór języka determinuje pewne zachowania systemu, np. przy wyborze języka <code>en</code>
Kupujący otrzyma wiadomość email w języku angielskim
</aside>

<aside class="notice">
Adres powrotny <code>return_url</code> to adres podstrony Twojej witryny, na który zostanie przekierowany Kupujący po dokonaniu płatności.
</aside>

<aside class="notice">
Zdefiniowanie adresu <code>notify_url</code> nie powoduje nadpisania adresu zdefiniowanego w ramach wybranego POS. Adres <code>notify_url</code> zdefiniowany przy tworzeniu transakcji będzie wykorzystywany tylko dla tej transakcji.
</aside>

### Odpowiedź

Klucz | Opis |
----- | ---- |
pos_id | identyfikator POS
amount | kwota zamówienia
language | język, którym posługuje się Kupujący
currency | waluta, dowolna spośród: PLN
buyer[name] | nazwa kupującego|
buyer[email] | email kupującego|
order_data[description] | opis zamówienia
order_data[order_id] | dodatkowy identyfikator zamówienia (dowolna treść zdefiniowana przez merchanta)
return_url | adres powrotny do przekierowania
status_history | historia zmian statusu
notify_url | adres URL do powiadomienia
partial_refunds | zwroty częściowe z transakcji (puste dla nowej transakcji)
updated_at | data ostatniej zmiany statusu transakcji
created_at | data utworzenia transakcji
identifier | identyfikator transakcji
sign | podpis transakcji
redirect_url | adres URL, który umożliwia dokonanie płatności

## Lista transakcji

```php
<?php

// autentykacja...

// pobieranie listy zapłaconych transakcji od dnia 2016-12-01

$transactions = $api->transactions()->listing(['date_from' => '2016-12-01', 'status' => \Monetivo\Api\Transactions::TRAN_STATUS_PAID]);

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
    [to] => 3
    [data] => Array
        (
            [0] => Array
                (
                    [pos_id] => 1
                    [identifier] => MXXXXXX
                    [currency] => PLN
                    [amount] => 2.00
                    [status] => 1
                    [language] => pl
                    [order_data] => Array
                        (
                            [order_id] => f011185b-fa2a-4b70-xxxx-xxxxxxxxxxxx
                            [description] => Zakup testowy 1
                        )

                    [buyer] => Array
                        (
                            [name] => John Smith
                            [email] => john@example.com
                        )

                    [status_history] => Array
                        (
                        )

                    [return_url] => https://example.com/thanks
                    [account_id] =>
                    [created_at] => 2016-12-09T12:38:04+0000
                    [updated_at] => 2016-12-09T12:38:04+0000
                    [channel_id] =>
                    [committed_at] =>
                    [accounted_at] =>
                    [partial_refunds] => Array()
                )

            [1] => Array
                (
                    [pos_id] => 1
                    [identifier] => M1XXXXX
                    [currency] => PLN
                    [amount] => 100.00
                    [status] => 1
                    [language] => pl
                    [order_data] => Array
                        (
                            [order_id] => d047f63d-7cdf-XXXX-9655-XXXXXXXXXXXX
                            [description] => Christmas gifts
                        )

                    [buyer] => Array
                        (
                            [name] => Anna Doe
                            [email] => ann@example.com
                        )

                    [status_history] => Array
                        (
                        )

                    [return_url] => https://example.com/thanks
                    [account_id] =>
                    [created_at] => 2016-12-09T12:41:58+0000
                    [updated_at] => 2016-12-09T12:41:58+0000
                    [channel_id] =>
                    [committed_at] =>
                    [accounted_at] =>
                    [partial_refunds] =>
                )

        )

    [httpCode] => 200
)
```

```shell
curl "https://api.monetivo.com/v1/transactions" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/transactions`

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | --- |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Parametry żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
date_from | - | nie | data od |
date_to | - | nie | data do |
sort | asc | nie | kolejność sortowania: asc (od najstarszej), desc (od najnowszej)
orderby | - | nie | kolumna sortowania, patrz niżej
per_page | - | nie | ilość wyników na stronę
page | - | nie | numer strony z wynikami
email | - | nie | ograniczenie wyszukania po wskazanym adresie email
amount_from | - | nie | kwota transakcji od
amount_to | - | nie | kwota transakcji do (włącznie)
status | - | nie | ograniczenie wyszukania do wskazanego statusu (wartość z tabeli Statusy transakcji)

### Kolumny sortowania

Kolumna | Opis |
------- | ----  |
updated_at | data zmiany statusu
created_at | data utworzenia
amount | kwota
committed_at | data zaksięgowania

### Statusy transakcji

Status | Wartość |
------ | ---- |
Nowa | 1 |
Zapłacona | 2 |
Zaakceptowana | 4 |
Zwrócona | 16 |
Odrzucona | 32 |

### Odpowiedź

Klucz | Opis |
----- | ---- |
total | liczba wyników (transakcji) |
per_page | ilość wyników na stronę |
current_page | bieżąca strona z wynikami
last_page | numer ostatniej strony z wynikami
next_page_url | adres URL do pobrania następnej strony z wynikami
prev_page_url | adres URL do pobrania poprzedniej strony z wynikami
from | wyniki od
to | wyniki do
data | tablica zawierająca wyniki

## Szczegóły transakcji

```php
<?php

// autentykacja...

// pobieranie szczegółów transakcji MO12345
$identifier = 'MO12345';
$transaction = $api->transactions()->details($identifier);

// Przykładowa odpowiedź - transakcja zaakceptowana wraz z dwoma zwrotami częściowymi
Array
(
    [pos_id] => 1
    [identifier] => MXXXXXX
    [currency] => PLN
    [amount] => 15.50
    [status] => 4
    [language] => pl
    [order_data] => Array
        (
            [order_id] => d6681448-f850-4c7c-bc28-XXXXXXXXXXXX
            [description] => Opis testowy
        )

    [buyer] => Array
        (
            [name] => John Doe
            [email] => john@example.com
        )

    [status_history] => Array
        (
        )

    [return_url] => https://example.com
    [notify_url] =>
    [account_id] =>
    [partial_refunds] => Array
        (
            [0] => Array
                (
                    [amount] => 1.00
                    [committed_at] => 2017-01-04T10:10:36+0100
                    [refund_identifier] => MRX8XXXX1
                )

            [1] => Array
                (
                    [amount] => 1.00
                    [committed_at] => 2017-01-04T10:12:26+0100
                    [refund_identifier] => MRX8XXXX2
                )

        )
    [channel_id] => 25
    [created_at] => 2016-12-13T10:18:06+0000
    [updated_at] => 2016-12-13T10:18:06+0000
    [committed_at] => 2016-12-13T10:18:08+0000
    [httpCode] => 200
)
```

```shell
curl "https://api.monetivo.com/v1/transactions/MRX8XXXX2" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"

```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/transactions/<ID>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
ID | - | tak | identyfikator transakcji |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Odpowiedź

Klucz | Opis |
----- | ---- |
pos_id | identyfikator POS
identifier | identyfikator transakcji
currency | waluta transakcji
amount | kwota transakcji
status | status transakcji
language | język, którym posługuje się Kupujący
order_data[description] | opis zamówienia
order_data[order_id] | dodatkowy identyfikator zamówienia (dowolna treść zdefiniowana przez merchanta)
buyer[name] | nazwa kupującego|
buyer[email] | email kupującego|
status_history | historia zmian statusu
return_url | adres powrotny URL do przekierowania
notify_url | adres URL do wysłania powiadomienia
account_id | identyfikator rachunku
partial_refunds | zwroty częściowe transakcji
channel_id | identyfikator kanału płatności użytego do dokonania płatności przez Kupującego
created_at | data utworzenia transakcji
updated_at | data ostatniej zmiany statusu transakcji
committed_at | data zaksięgowania transakcji na koncie Merchanta

## Obsługa powiadomień o statusie

Zmiana statusu transakcji powoduje  wysłanie przez system Monetivo powiadomienia na adres URL podany przez Merchanta.

<aside class="notice">
Adres <code>notify_url</code> zazwyczaj jest zdefiniowany przy POS. Istnieje możliwość nadpisania tego adresu przy tworzeniu transakcji tylko i wyłącznie na potrzeby tej transakcji.
</aside>

<aside class="notice">
Przy odbiorze powiadomienia Twój serwer powinien zwrócić kod HTTP 200 OK. Jeżeli biblioteka się nie autoryzuje lub wystąpi inny błąd np. po stronie realizacji zamówienia, aplikacja musi zwrócić błąd http (np. 400) jeżeli chce otrzymać następne powiadomienie. W takim przypadku serwer Monetivo będzie ponawiać wysyłkę powiadomień co jakiś czas do momentu, gdy zwrócony zostanie status 200 OK.
</aside>

Po odebraniu powiadomienia, w przypadku gdy transakcja jest poprawna (opłacona, a następnie zaakceptowana), możesz przystąpić do dalszych czynności związanych z realizacją płatności po Twojej stronie.


```php
<?php

// autentykacja...

// odbiór powiadomienia
$transaction = $api->handleCallback();

// sprawdzenie czy transakcja została
if($transaction === false) {
  exit('Transakcja nie została zaakceptowana');
}
else {
  // transakcja została opłacona i zaakceptowana,
  // zmienna $transaction obejmuje szczegóły transakcji,
  // Twój kod - dalsza część logiki, np. oznaczenie płatności w systemie jako wykonanej, wysłanie maila, etc.
}
```

### Parametry żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
identifier | - | tak | identyfikator transakcji |

## Akceptacja transakcji

```php
<?php

// autentykacja...

// akceptowanie transakcji MO12345
$identifier = 'MO12345';
$transaction = $api->transactions()->accept($identifier);

// Poprawna odpowiedź serwera jest taka sama jak w przypadku tworzenia transakcji
// W przypadku wystąpienia błędu zwrócony zostanie odpowiedni komunikat

// Przykład: próba zaakceptowania transakcji oczekującej - serwer zwraca komunikat o błędzie z informacją, że nie można zaakceptować oczekującej, nieopłaconej transakcji
Array
(
    [errors] => Array
        (
            [code] => 1
            [message] => "Cannot accept transaction - incorrect status"
        )
)
```

```shell
curl -X "PUT" "https://api.monetivo.com/v1/transactions/MO12345/accept" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`PUT https://api.monetivo.com/v1/transactions/<ID>/accept`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
ID | - | tak | identyfikator transakcji |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

<aside>
Akceptacja transakcji nie jest wymagana, jeśli włączono auto-akceptację (domyślnie włączona)
</aside>

## Odrzucenie transakcji

```php
<?php

// autentykacja...

// odrzucenie transakcji MO12345
$identifier = 'MO12345';
$transaction = $api->transactions()->decline($identifier);

```

```shell
curl -X "PUT" "https://api.monetivo.com/v1/transactions/MO12345/decline" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```
> Odpowiedź serwera jest taka sama jak w przypadku tworzenia transakcji

### Żądanie HTTP

`PUT https://api.monetivo.com/v1/transactions/<ID>/decline`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
ID | - | tak | identyfikator transakcji |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

## Zwrot transakcji

```php
<?php

// autentykacja...

// pobieranie szczegółów transakcji MO12345
$identifier = 'MO12345';
$transaction = $api->transactions()->refund($identifier);

// Przykładowy zwrócony wynik:

Array
(
    [name] => John Smith
    [email] => john@example.com
    [amount] => 1.00
    [transaction_identifier] => MO12345
    [currency] => PLN
    [description] => christmas gifts
    [reason] => 4
    [partial] => 0
    [status_history] => Array
        (
            [0] => Array
                (
                    [status] => 1
                    [date] => 2017-01-04T09:07:38+0000
                )
        )
    [status] => 1
    [updated_at] => 2017-01-04T09:07:38+0100
    [created_at] => 2017-01-04T09:07:38+0100
    [identifier] => MRX8ER10X
    [account_id] => 1
    [committed_at] => 2017-01-04T10:07:37+0100
)
```

```shell
curl -X "POST" "https://api.monetivo.com/v1/transactions/MRX8ER10X/refund" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`POST https://api.monetivo.com/v1/transactions/<ID>/refund`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
ID | - | tak | identyfikator transakcji |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Odpowiedź

Klucz | Opis |
----- | ---- |
name | nazwa kupującego
email | email kupującego
amount | kwota zwrotu
transaction_identifier | identyfikator transakcji
currency | waluta
description | opis zwrotu
reason | przyczyna zwrotu (patrz niżej)
partial | czy zwrot częściowy. Wartość ```true``` jeśli kwota zwrotu jest niższa od kwoty transakcji
status_history | historia zmian statusu
status | status zwrotu
updated_at | data aktualizacji zwrotu
created_at | data utworzenia zwrotu
identifier | identyfikator zwrotu
account_id | identyfikator rachunku
committed_at | data księgowania

### Przyczyny zwrotu

Wartość | Opis |
------- | ---- |
1 | transakcja nie została zaakceptowana
2 | transakcja nie została odnaleziona w systemie
4 | zwrot nastąpił na żądanie merchanta
8 | zwrot nastąpił z powodu błędu w przetwarzaniu transakcji

### Statusy zwrotu

Wartość | Opis |
------- | ---- |
1 | oczekiwanie na uzupełnienie danych bankowych
2 | oczekiwanie na przesłanie danych do banku
8 | dane bankowe przesłane do wypłaty
