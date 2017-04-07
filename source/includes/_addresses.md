# Adresy

Do konta merchanta przypisane są dane adresowe. Dane mogą posiadać następujący typ:

Typ | Opis |
--- | --- |
registration | adres podawany przy rejestracji |
correspondence | adres korespondencyjny |


## Lista adresów

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// pobieranie adresu do korespondencji

$addresses = $api->addresses()->listing(\Monetivo\Api\Addresses::TYPE_CORRESPONDENCE);

// Przykładowy zwrócony wynik:

Array
(
    [zip] => 60-586
    [city] => Poznań
    [block] => 8
    [phone] => +48123456789
    [street] => ul. Botaniczna
    [country] => POL
    [companyname] => Monetivo
    [httpCode] => 200
)
```

```shell
curl "https://api.monetivo.com/v1/addresses/correspondence" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8"
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

<aside class="notice">
Minimalny poziom uprawnień: <code>użytkownik administracyjny</code>
</aside>

```php
<?php

// autentykacja...

// aktualizacja adresu do korespondencji - zmiana miasta

$address = $api->addresses()->update(\Monetivo\Api\Addresses::TYPE_CORRESPONDENCE, ['city' => 'Poznań']);

// Przykładowy zwrócony wynik:

Array
(
    [zip] => 60-586
    [city] => Poznań
    [block] => 8
    [phone] => +48123456789
    [street] => ul. Botaniczna
    [country] => POL
    [companyname] => Monetivo
    [httpCode] => 200
)
```

```shell
curl -X "PUT" "https://api.monetivo.com/v1/addresses/correspondence" \
     -H "X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6Im5pY2UgdHJ5IDspIiwiaWF0IjoxNDkxNTQ5ODE0LCJleHAiOjE0OTE1NTM1NzUsImp0aSI6IjhiNmQwYmQyLWE0ZGEtNDVjYi05MTU5LWZmZTc2NmFjMmU5MyJ9.iQj7wi5eLkqX_mGhuTP89xpw2cjM-qx6T1gvDpUGljI" \
     -H "X-API-Token: prod_3cd89e58-xxxx-xxxx-xxxx-ee804b8a2ecf" \
     -H "Content-Type: application/x-www-form-urlencoded; charset=utf-8" \
     --data-urlencode "city=Poznan" \
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
country | - | tak | Państwo (w formacie ISO 3166-1 alpha-2)
companyname | - | tak | Nazwa firmy
