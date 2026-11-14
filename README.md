# Pamiętnik Zdrowia — dokumentacja projektu

**Stan dokumentacji:** 2026-11-14 · **Wersja prototypu:** v0.13.0 · **Status:** działający prototyp webowy, **nie** gotowa aplikacja medyczna ani produkcyjna.

## Najważniejsze odnośniki
- **Kod:** https://github.com/mulodesign/Pamietnik-Zdrowia
- **Testowa strona:** https://mulodesign.github.io/Pamietnik-Zdrowia/
- **Kod wykonywalny:** [index.html](index.html) — pojedynczy plik HTML z CSS i JavaScript.
- **Gałąź podstawowa:** `main`; repozytorium jest **publiczne**.
- **Publikacja:** GitHub Pages (publiczny adres powyżej; konfigurację Pages należy zweryfikować w Settings → Pages przed zmianą sposobu publikowania).

## Dokumenty projektu
1. [SPECYFIKACJA.md](docs/SPECYFIKACJA.md) — wymagania, ekrany, zasady i dalszy rozwój.
2. [ARCHITEKTURA.md](docs/ARCHITEKTURA.md) — faktyczna technologia, przepływ danych, model wpisu, ograniczenia.
3. [OPERATOR.md](docs/OPERATOR.md) — instrukcja dla właściciela/operatora: uruchamianie, publikowanie, backup, diagnoza.
4. [ODTWORZENIE_AI.md](docs/ODTWORZENIE_AI.md) — instrukcja dla programisty/asystenta AI wraz z kryteriami zgodności.
5. [TESTY_I_ZMIANY.md](docs/TESTY_I_ZMIANY.md) — testy regresyjne, decyzje i wykaz braków.

## Ważne dla wszystkich wykonawców
**Nie przechowuj prawdziwych danych o zdrowiu w aktualnym prototypie.** Dane testowe są zapisywane lokalnie w przeglądarce i nie są szyfrowane. Prywatne karty Safari mają oddzielny magazyn danych; wyczyszczenie danych witryny może skasować oba magazyny. Kopia JSON jest **niezaszyfrowana**. Nigdy nie zapisuj haseł, tokenów, sekretów ani danych użytkowników w tym publicznym repozytorium.

## Zasady utrzymania
- `index.html` jest źródłem prawdy o **aktualnie działającej** aplikacji; dokumenty odróżniają stan wdrożony od planu.
- Po każdej zmianie kodu aktualizuj numer wersji widoczny w nagłówku oraz w „Więcej”, dokumentację i scenariusze testów.
- Nie zmieniaj modelu danych ani storage bez migracji, kopii i testów odczytu istniejącej historii.
- Dokumentacja + kompletny kod + jawnie wskazane wymagania środowiska mają pozwolić odtworzyć aplikację; sama dokumentacja nie zastąpi plików źródłowych.
- Każda niezweryfikowana informacja o urządzeniu, koncie lub konfiguracji musi być opisana jako **do potwierdzenia**, nie jako fakt.
