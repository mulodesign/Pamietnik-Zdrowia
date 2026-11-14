# Instrukcja operatora — Pamiętnik Zdrowia

**Wersja testowa v0.13.0.** Dokument przeznaczony dla osoby zarządzającej prototypem, również bez programowania. Pracuj tylko na fikcyjnych danych.

## Dostęp i lokalizacja
- Repozytorium: https://github.com/mulodesign/Pamietnik-Zdrowia
- Aplikacja: https://mulodesign.github.io/Pamietnik-Zdrowia/
- Konto/repozytorium: `mulodesign / Pamietnik-Zdrowia`.
- Główna gałąź: `main`; edytowany obecnie plik: `index.html`.
- GitHub Pages: otwórz repo → **Settings → Pages**, sprawdź rzeczywisty adres publikacji, gałąź i folder źródłowy. Dotychczasowe publikowanie działa przez aktualizację pliku na `main`, ale zmiany konfiguracji wymagają ponownego sprawdzenia.
- Do kopiowania projektu przez Git: `git clone https://github.com/mulodesign/Pamietnik-Zdrowia.git`.

## Przeglądanie na iPhonie — ważne
1. Otwórz Safari, wybierz **zwykłe karty** („Wszystkie karty”), NIE „Prywatne”.
2. Otwórz adres aplikacji. Odnośnik z parametrem `?v=0130` może pomóc odświeżyć cache strony, **nie przenosi danych między przeglądarkami**.
3. Przed testami zapisz identyfikator pamięci `PZ-...` z zakładki Historia; sprawdź liczbę wpisów.
4. Po utworzeniu **fikcyjnego** wpisu zamknij Safari, otwórz ponownie w tym samym trybie i sprawdź liczbę wpisów.
5. Nie przypisuj zniknięcia wpisów automatycznie do błędu kodu. Najpierw ustal przeglądarkę, tryb, grupę kart i identyfikator pamięci.
6. **Nie wnioskuj**, że zmiana identyfikatora jednoznacznie oznacza skasowanie danych — może świadczyć o innym kontekście przechowywania.

## Codzienny eksport kopii testowej
1. Otwórz aplikację w zwykłym Safari.
2. Wybierz **Historia → Pobierz kopię wszystkich wpisów** albo **Więcej → Pobierz kopię JSON**.
3. Potwierdź ostrzeżenie o nieszyfrowanym eksporcie.
4. Zapisz plik JSON w miejscu, które kontrolujesz; dla danych testowych najlepiej w katalogu przeznaczonym wyłącznie do testów.
5. Aby odtworzyć: **Więcej → Przywróć kopię** → wskaż właściwy JSON → potwierdź. Import dołącza brakujące identyfikatory; nie nadpisuje już istniejących rekordów o tym samym `id`.
6. Nie wysyłaj kopii z prawdziwą historią zdrowotną przez publiczne repozytorium.

## Aktualizowanie strony
1. Otwórz `index.html` na GitHubie, wybierz edycję tylko jeśli wiesz, co zmieniasz; alternatywnie commit przez Git.
2. Przed zmianą pobierz bieżący kod i testową kopię JSON. Dokumentację aktualizuj razem z kodem.
3. W nagłówku `header()` i w sekcji `more()` zmień **ten sam numer wersji**.
4. Sprawdź składnię JavaScript oraz scenariusze w [TESTY_I_ZMIANY.md](TESTY_I_ZMIANY.md).
5. Zapisz commit na `main`, sprawdź wynik pod adresem GitHub Pages i odczyt istniejącej historii. Nie zakładaj, że publikacja zakończyła się natychmiast.
6. W razie awarii znajdź ostatni sprawny commit w historii GitHub, wykonaj **jawny rollback kodu** i przetestuj dane. Nie wymazuj pamięci przeglądarki w ramach diagnozy.

## Diagnostyka
- **Historia pusta:** upewnij się, czy w Safari otwarto zwykły, a nie prywatny tryb. Sprawdź identyfikator pamięci i liczbę wpisów. Przejdź do „Więcej” i sprawdź IndexedDB. Nie czyść danych witryny.
- **Brak zapisu:** nie opuszczaj edycji, skopiuj fikcyjny tekst do bezpiecznej notatki i odnotuj komunikat. Sprawdź uprawnienia/zasoby pamięci urządzenia.
- **Stara wersja interfejsu:** odśwież stronę, sprawdź numer w nagłówku; ewentualnie dodaj parametr wersji do URL.
- **Brak dyktowania:** używaj mikrofonu na klawiaturze systemowej; to nie jest wbudowany rejestrator audio.
- **Błędy po aktualizacji:** sprawdź zachowanie na nowej fikcyjnej historii i w historii już istniejącej; nie usuwaj wpisów diagnostycznych bez kopii.

## Rejestr środowisk — do uzupełniania po potwierdzeniu
| Element | Stan | Co trzeba potwierdzić |
|---|---|---|
| GitHub | Konto `mulodesign`, publiczne repo, `main` | Operatorzy, uprawnienia i 2FA — bez zapisywania tajnych danych |
| Hosting | GitHub Pages pod wskazanym URL | Bieżące Settings → Pages i ewentualna domena niestandardowa |
| iPhone | Testy odbywały się w Safari na iOS | Model, dokładny iOS, tryb i data testu |
| Android | Docelowo planowany | Model, system, przeglądarka i wyniki testów |
| Backend / chmura na dane zdrowia | Nie ma w aktualnym kodzie | Projektować dopiero z zasadami bezpieczeństwa |
| Push/notyfikacje | Niewdrożone | Uprawnienia, harmonogram, działanie po restarcie |
| Integracje, konta i sekrety | Brak listy potwierdzonej w repo | Zweryfikować z operatorem i zapisać jedynie procedurę konfiguracji |

**Nigdy nie dołączaj do dokumentacji haseł, kluczy API, tokenów, kodów odzyskiwania ani realnych danych zdrowotnych.**
