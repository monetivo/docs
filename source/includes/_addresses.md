# Adresy

Do konta merchanta przypisane są dane adresowe. Dane mogą posiadać następujący typ:

Typ | Opis |
--- | --- |
registration | adres podawany przy rejestracji |
correspondence | adres korespondencyjny |


## Lista adresów

```php
<?php

// autentykacja...

// pobieranie adresu do korespondencji

$addresses = $api->addresses()->list(\Monetivo\Api\Addresses::TYPE_CORRESPONDENCE);


```

> Przykładowy zwrócony wynik:

```php
Array
(
    [zip] => 60-586
    [city] => Poznań
    [block] => 8
    [phone] => +48123456789
    [street] => ul. Botaniczna
    [country] => POL
    [companyname] => Fundacja Polak Pomaga
    [httpCode] => 200
)
```

### Żądanie HTTP

`GET https://api.monetivo.com/v1/addresses/<TYPE>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
TYPE | - | tak | Typ adresu, patrz tabela wyżej |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

## Aktualizacja adresu

```php
<?php

// autentykacja...

// aktualizacja adresu do korespondencji - zmiana miasta

$address = $api->addresses()->update(\Monetivo\Api\Addresses::TYPE_CORRESPONDENCE, ['city' => 'Poznań']);


```

> Przykładowy zwrócony wynik:

```php
Array
(
    [zip] => 60-586
    [city] => Poznań
    [block] => 8
    [phone] => +48123456789
    [street] => ul. Botaniczna
    [country] => POL
    [companyname] => Fundacja Polak Pomaga
    [httpCode] => 200
)
```

### Żądanie HTTP

`PUT https://api.monetivo.com/v1/addresses/<TYPE>`

### Parametry URL żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
TYPE | - | tak | Typ adresu, patrz tabela wyżej |

### Nagłówki żądania

Nagłówek | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
X-API-Token | - | tak | token aplikacji
X-Auth-Token | - | tak | token użytkownika

### Parametry żądania

Parametr | Domyślnie | Wymagany | Opis |
-------- | --------- | -------- | ---  |
zip | - | tak | Kod pocztowy |
city | - | tak | Miasto |
block | - | tak | Nr mieszkania/lokalu
phone | - | tak | Telefon
street | - | tak | Ulica
country | - | tak | Państwo
companyname | - | tak | Nazwa firmy
