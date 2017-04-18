# Wstęp

## Informacje ogólne

Monetivo API umożliwia integrację własnego oprogramowania merchanta (np. sklepu) z systemem płatności Monetivo.
Udostępniamy biblioteki, które pozwalają na m.in. wygenerowanie transakcji płatniczej oraz obsługa powiadomień o dokonaniu płatności.
Bilbioteka umożliwia również wykonanie innych operacji na koncie merchanta systemu Monetivo takich jak:

- generowanie listy transakcji,
- zarządzanie rachunkami merchanta,
- zarządzanie kontaktami merchanta.

Możesz korzystać z Monetivo API nie używając bibliotek. W takim przypadku samodzielnie wysyłasz zapytania HTTP do naszego REST API.

System Monetivo składa się z dwóch odizolowanych od siebie środowisk:

- testowego, dostępnego pod adresem `https://api.monetivo.io`,
- produkcyjnego, dostępnego pod adresem `https://api.monetivo.com`.

## Dostęp do API

Możesz uzyskać dostęp do Monetivo API po wykonaniu nastepujących kroków:

1. Zarejestruj albo zaloguj się w [Panelu Merchanta](https://merchant.monetivo.com),
2. Kliknij Dodaj sklep i podaj szczegółowe informacje o Twoim sklepie.

Po utworzeniu sklepu w systemie Monetivo otrzymasz dostęp do środowiska testowego w postaci tokenu aplikacji, loginu oraz hasła. Dane te są przypisane do specjalnego użytkownika, tzw. użytkownika integracji, który posiada zmniejszony poziom uprawnień. Logując się jako użytkownik integracji możesz wykonać podstawowe czynności, takie jak utworzenie transakcji czy zwrot transakcji. Część zapytań do naszego API może być wykonywana tylko przez użytkownika administracyjnego.

Jeśli Twoja integracja przebiegnie pomyślnie, po uprzednim uzupełnieniu niezbędnych danych będziesz mieć możliwość migracji na środowisko produkcyjne. Niektóre akcje, takie jak wypłata środków na Twój rachunek bankowy, możliwe są do wykonania jedynie w środowisku produkcyjnym.

## Elementy systemu Monetivo

Z punktu widzenia Merchanta, system Monetivo obejmuje kilka elementów:

1. rachunek wewnętrzny na którym księgowane są środki w systemie Monetivo (Account),
2. punkt sprzedaży (POS), odpowiadający np. sklepowi Merchanta,
3. rachunek do wypłat (Bank account), wykorzystywany do wypłat środków z rachunku wewnętrznego na zewnętrzny rachunek bankowy Merchanta.

Każdy z tych elementów jest w pełni konfigurowalny z poziomu naszego API.
Dążąc do uproszczenia integracji, wprowadziliśmy koncepcję Sklepu. Sklep w systemie Monetivo stanowi połączenie rachunku oraz POS.
Dodając sklep w Panelu Merchanta Monetivo, nasz system automatycznie skonfiguruje dla Ciebie POS oraz rachunek wewnętrzny. Korzystając z API nadal masz możliwość dodatkowej konfiguracji obu tych elementów z osobna.
