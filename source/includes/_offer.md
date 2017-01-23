# Oferta

Oferta obejmuje informacje o prowizjach pobieranych przez Monetivo. Obecnie wyróżniamy dwa typy oferty:

Typ oferty | Opis |
--- | --- |
payments | oferta dotycząca płatności (prowizje za płatność w kanale) |
services | oferta dotycząca usług (prowizje za poszczególne usługi udostępniane przez Monetivo merchantowi) |


## Lista ofert

```php
<?php

// autentykacja...

// pobieranie listy ofert dla udostępnionych usług

$offers = $api->offer()->listing(\Monetivo\Api\Offer::TYPE_PAYMENTS);


```

> Przykładowy zwrócony wynik:

```php
Array
(
    [0] => Array
        (
            [channel_id] => 1
            [channel_name] => Blik
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [1] => Array
        (
            [channel_id] => 2
            [channel_name] => mTransfer
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [2] => Array
        (
            [channel_id] => 3
            [channel_name] => Płać z ING
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [3] => Array
        (
            [channel_id] => 4
            [channel_name] => Pekao24Przelew
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [4] => Array
        (
            [channel_id] => 5
            [channel_name] => Przelew24 BZWBK
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [5] => Array
        (
            [channel_id] => 6
            [channel_name] => Płacę z Alior Bankiem
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [6] => Array
        (
            [channel_id] => 7
            [channel_name] => Płacę z IPKO
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [7] => Array
        (
            [channel_id] => 8
            [channel_name] => Płacę z Inteligo
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [8] => Array
        (
            [channel_id] => 9
            [channel_name] => Millennium Bank PBL
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [9] => Array
        (
            [channel_id] => 10
            [channel_name] => CA przelew online
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [10] => Array
        (
            [channel_id] => 11
            [channel_name] => T-Mobile Usługi Bankowe
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [11] => Array
        (
            [channel_id] => 12
            [channel_name] => Deutsche Bank
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [12] => Array
        (
            [channel_id] => 13
            [channel_name] => BPH Przelew
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [13] => Array
        (
            [channel_id] => 14
            [channel_name] => BGŻ BNP Paribas
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [14] => Array
        (
            [channel_id] => 15
            [channel_name] => Eurobank - płatność online
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [15] => Array
        (
            [channel_id] => 16
            [channel_name] => PBS PBL
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [16] => Array
        (
            [channel_id] => 17
            [channel_name] => r-Przelew
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [17] => Array
        (
            [channel_id] => 18
            [channel_name] => Toyota Bank Pay Way
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [18] => Array
        (
            [channel_id] => 19
            [channel_name] => BSWSCHOWA PBL
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [19] => Array
        (
            [channel_id] => 20
            [channel_name] => Płać z BOŚ Bank
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [20] => Array
        (
            [channel_id] => 21
            [channel_name] => Getin Bank
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [21] => Array
        (
            [channel_id] => 22
            [channel_name] => Płacę z Orange
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [22] => Array
        (
            [channel_id] => 23
            [channel_name] => Płacę z Citi Handlowy
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [23] => Array
        (
            [channel_id] => 24
            [channel_name] => e-transfer Pocztowy24
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [24] => Array
        (
            [channel_id] => 25
            [channel_name] => Płacę z PLUS BANK
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [25] => Array
        (
            [channel_id] => 26
            [channel_name] => Noble Bank
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [26] => Array
        (
            [channel_id] => 27
            [channel_name] => Inny bank
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [27] => Array
        (
            [channel_id] => 28
            [channel_name] => Karty SixPay
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [28] => Array
        (
            [channel_id] => 29
            [channel_name] => Sofort
            [commission_rate] => 1.90
            [commission_const] => 0.00
        )

    [httpCode] => 200
)
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/offer/<TYPE>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
TYPE | - | tak | typ oferty, patrz tabela wyżej |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

## Szczegóły oferty

```php
<?php

// autentykacja...

// pobranie szczegółów oferty dotyczącej usługi o identyfikatorze 18

$offer = $api->offer()->details(\Monetivo\Api\Offer::TYPE_SERVICES, 18);


```

> Przykładowy zwrócony wynik:

```php
Array
(
    [0] => Array
        (
            [service_id] => 18
            [service_name] => account_locked_operation
            [commission_rate] => 0.00
            [commission_const] => 0.00
        )

    [httpCode] => 200
)
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/offer/<TYPE>/<ID>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
TYPE | - | tak | typ adresu, patrz tabela wyżej |
ID | - | tak | identyfikator oferty |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Odpowiedź

Klucz |  Opis |
----- | ----- |
service_id | identyfikator usługi
service_name | nazwa usługi
commision_rate | stawka prowizji
commission_const | prowizja w postaci stałej opłaty
