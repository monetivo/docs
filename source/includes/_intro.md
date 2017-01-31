# Wstęp

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

Przy rejestracji otrzymujesz dostęp do środowiska testowego. Jeśli Twoja integracja przebiegnie pomyślnie, po uprzednim uzupełnieniu niezbędnych danych będziesz mieć możliwość migracji na środowisko produkcyjne.
