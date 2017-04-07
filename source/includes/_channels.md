# Kanały płatności

## Lista dostępnych kanałów płatności

```php
<?php

// autentykacja...

// pobieranie listy dostępnych kanałów płatności dla waluty PLN

$accounts = $api->paymentChannels()->listing('PLN');


```

> Przykładowy zwrócony wynik:

```php
Array
(
    [0] => stdClass Object
        (
            [channel_id] => 1
            [name] => Blik
            [currency] => PLN
            [type] => 6
            [order_by] => 1
            [img] => https://secure.monetivo.com/assets/img/banks/1.png
        )

    [1] => stdClass Object
        (
            [channel_id] => 2
            [name] => mTransfer
            [currency] => PLN
            [type] => 1
            [order_by] => 2
            [img] => https://secure.monetivo.com/assets/img/banks/2.png
        )

    [2] => stdClass Object
        (
            [channel_id] => 3
            [name] => Płać z ING
            [currency] => PLN
            [type] => 1
            [order_by] => 3
            [img] => https://secure.monetivo.com/assets/img/banks/3.png
        )

    [3] => stdClass Object
        (
            [channel_id] => 4
            [name] => Pekao24Przelew
            [currency] => PLN
            [type] => 1
            [order_by] => 4
            [img] => https://secure.monetivo.com/assets/img/banks/4.png
        )

    [4] => stdClass Object
        (
            [channel_id] => 5
            [name] => Przelew24 BZWBK
            [currency] => PLN
            [type] => 1
            [order_by] => 5
            [img] => https://secure.monetivo.com/assets/img/banks/5.png
        )

    [5] => stdClass Object
        (
            [channel_id] => 6
            [name] => Płacę z Alior Bankiem
            [currency] => PLN
            [type] => 1
            [order_by] => 6
            [img] => https://secure.monetivo.com/assets/img/banks/6.png
        )

    [6] => stdClass Object
        (
            [channel_id] => 7
            [name] => Płacę z IPKO
            [currency] => PLN
            [type] => 1
            [order_by] => 7
            [img] => https://secure.monetivo.com/assets/img/banks/7.png
        )

    [7] => stdClass Object
        (
            [channel_id] => 8
            [name] => Płacę z Inteligo
            [currency] => PLN
            [type] => 1
            [order_by] => 8
            [img] => https://secure.monetivo.com/assets/img/banks/8.png
        )

    [8] => stdClass Object
        (
            [channel_id] => 9
            [name] => Millennium Bank PBL
            [currency] => PLN
            [type] => 1
            [order_by] => 9
            [img] => https://secure.monetivo.com/assets/img/banks/9.png
        )

    [9] => stdClass Object
        (
            [channel_id] => 10
            [name] => CA przelew online
            [currency] => PLN
            [type] => 1
            [order_by] => 10
            [img] => https://secure.monetivo.com/assets/img/banks/10.png
        )

    [10] => stdClass Object
        (
            [channel_id] => 11
            [name] => T-Mobile Usługi Bankowe
            [currency] => PLN
            [type] => 1
            [order_by] => 11
            [img] => https://secure.monetivo.com/assets/img/banks/11.png
        )

    [11] => stdClass Object
        (
            [channel_id] => 12
            [name] => Deutsche Bank
            [currency] => PLN
            [type] => 1
            [order_by] => 12
            [img] => https://secure.monetivo.com/assets/img/banks/12.png
        )

    [12] => stdClass Object
        (
            [channel_id] => 13
            [name] => BPH Przelew
            [currency] => PLN
            [type] => 1
            [order_by] => 13
            [img] => https://secure.monetivo.com/assets/img/banks/13.png
        )

    [13] => stdClass Object
        (
            [channel_id] => 14
            [name] => BGŻ BNP Paribas
            [currency] => PLN
            [type] => 1
            [order_by] => 14
            [img] => https://secure.monetivo.com/assets/img/banks/14.png
        )

    [14] => stdClass Object
        (
            [channel_id] => 15
            [name] => Eurobank - płatność online
            [currency] => PLN
            [type] => 1
            [order_by] => 15
            [img] => https://secure.monetivo.com/assets/img/banks/15.png
        )

    [15] => stdClass Object
        (
            [channel_id] => 16
            [name] => PBS PBL
            [currency] => PLN
            [type] => 1
            [order_by] => 16
            [img] => https://secure.monetivo.com/assets/img/banks/16.png
        )

    [16] => stdClass Object
        (
            [channel_id] => 17
            [name] => r-Przelew
            [currency] => PLN
            [type] => 1
            [order_by] => 17
            [img] => https://secure.monetivo.com/assets/img/banks/17.png
        )

    [17] => stdClass Object
        (
            [channel_id] => 18
            [name] => Toyota Bank Pay Way
            [currency] => PLN
            [type] => 1
            [order_by] => 18
            [img] => https://secure.monetivo.com/assets/img/banks/18.png
        )

    [18] => stdClass Object
        (
            [channel_id] => 19
            [name] => BSWSCHOWA PBL
            [currency] => PLN
            [type] => 1
            [order_by] => 19
            [img] => https://secure.monetivo.com/assets/img/banks/19.png
        )

    [19] => stdClass Object
        (
            [channel_id] => 20
            [name] => Płać z BOŚ Bank
            [currency] => PLN
            [type] => 1
            [order_by] => 20
            [img] => https://secure.monetivo.com/assets/img/banks/20.png
        )

    [20] => stdClass Object
        (
            [channel_id] => 21
            [name] => Getin Bank
            [currency] => PLN
            [type] => 1
            [order_by] => 21
            [img] => https://secure.monetivo.com/assets/img/banks/21.png
        )

    [21] => stdClass Object
        (
            [channel_id] => 22
            [name] => Płacę z Orange
            [currency] => PLN
            [type] => 1
            [order_by] => 22
            [img] => https://secure.monetivo.com/assets/img/banks/22.png
        )

    [22] => stdClass Object
        (
            [channel_id] => 23
            [name] => Płacę z Citi Handlowy
            [currency] => PLN
            [type] => 1
            [order_by] => 23
            [img] => https://secure.monetivo.com/assets/img/banks/23.png
        )

    [23] => stdClass Object
        (
            [channel_id] => 24
            [name] => e-transfer Pocztowy24
            [currency] => PLN
            [type] => 1
            [order_by] => 24
            [img] => https://secure.monetivo.com/assets/img/banks/24.png
        )

    [24] => stdClass Object
        (
            [channel_id] => 25
            [name] => Płacę z PLUS BANK
            [currency] => PLN
            [type] => 1
            [order_by] => 25
            [img] => https://secure.monetivo.com/assets/img/banks/25.png
        )

    [25] => stdClass Object
        (
            [channel_id] => 26
            [name] => Noble Bank
            [currency] => PLN
            [type] => 1
            [order_by] => 26
            [img] => https://secure.monetivo.com/assets/img/banks/26.png
        )

)
```

```shell
curl "https://api.monetivo.com/v1/channels" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/channels`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
currency | - | tak | waluta wykorzystywana w kanałach płatności |
type | - | nie | typy kanałów płatności rozdzielane przecinkiem, z listy poniżej

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Typy kanałów płatności

Typ | Wartość | Opis |
------ | ---- | ---- |
TYPE_ETRANSFER | 1 | kanały szybkich płatności typu eTransfer
TYPE_BLIK | 2 | kanały płatności systemu BLIK
TYPE_MO_APP | 4 | kanały aplikacji mobilnych (oferta w przygotowaniu)
TYPE_MANUAL | 8 | kanały dla płatności wykonywanych manualnie, np. druk płatności
TYPE_CARD | 16 | kanały płatności kartą kredytową
TYPE_OTHER | 32 | pozostałe kanały

<aside class="notice">
Wartość <code>channel_id</code> kanałów zwracanych w odpowiedzi możesz wykorzystać do predefiniowania kanału płatności. Zobacz <a href="https://docs.monetivo.com/#tworzenie-transakcji">Tworzenie transakcji</a>
</aside>
