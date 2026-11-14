# Architektura i dane — stan faktyczny v0.13.0

## Infrastruktura [ZWERYFIKOWANE]
- Repozytorium GitHub: `mulodesign/Pamietnik-Zdrowia`; dostęp publiczny; gałąź domyślna `main`.
- Aplikacja uruchamia się pod `https://mulodesign.github.io/Pamietnik-Zdrowia/` (adres projektu).
- Źródło: pojedynczy plik `index.html` w katalogu głównym. HTML, CSS i zwykły JavaScript; bez zewnętrznego frameworka, bundlera, backendu i konfiguracji CI widocznej w pliku.
- Hostowanie przez GitHub Pages. Szczegóły aktywnego ustawienia publikacji należy skontrolować w GitHub → Settings → Pages.
- Żadne urządzenie nie jest „podłączone do repo” przez mechanizm aplikacji. Rzeczywistych urządzeń testowych i ich dokładnych wersji OS nie da się wiarygodnie odczytać z kodu; wpisywać tylko po sprawdzeniu.

## Przepływ danych [ZWERYFIKOWANE]
1. `initializeDiary()` uruchamia się na starcie i otwiera IndexedDB.
2. Wstępny odczyt następuje z `localStorage` (klucz `pz_demo_01`). Starsze wpisy są normalizowane.
3. IndexedDB: baza `PamietnikZdrowia`, wersja `1`, magazyn `snapshots`, klucz rekordu `current`. Jeśli jest snapshot z tablicą `records`, staje się źródłem danych. W przeciwnym razie istniejące dane z localStorage są migracją zapisywane w IndexedDB.
4. `save(candidate)` najpierw zapisuje snapshot do IndexedDB (gdy działa), następnie próbuje zapisać `localStorage`, po czym aktualizuje tablicę w pamięci. Gdy IndexedDB nie działa, może zapisać wyłącznie do localStorage.
5. `pz_install_id_01` w localStorage zawiera identyfikator diagnostyczny `PZ-...`; **to nie jest identyfikator konta ani metoda identyfikacji użytkownika**.
6. Safari zwykłe i prywatne oraz różne przeglądarki mogą używać różnych magazynów. Oba lokalne mechanizmy mogą zostać wyczyszczone przez system/przeglądarkę. **To nie jest zabezpieczenie przed utratą telefonu ani niezależna kopia.**
7. Eksport `exportDemo()` tworzy niezabezpieczony plik `Pamietnik_Zdrowia_TEST_kopia_YYYY-MM-DD.json`. Import `importDemo()` dołącza wpisy z pliku, unikając tych samych identyfikatorów. Nie ma kryptografii ani weryfikacji integralności kopii.

## Model wpisu [ZWERYFIKOWANE — przykład syntetyczny]
```json
{
  "id": "unikalny-identyfikator-tekstu",
  "date": "2026-11-14",
  "topic": "Po spacerze",
  "mood": 5,
  "sleepScore": 6,
  "energyScore": 5,
  "stressScore": 2,
  "text": "Przykładowa, fikcyjna notatka.",
  "originalText": "Przykładowa, fikcyjna notatka.",
  "mode": "literal",
  "tags": []
}
```
- `id`: string, obecnie generowany z `Date.now()` i `Math.random()` (nie UUID).
- `date`: lokalny dzień `YYYY-MM-DD`; `topic` opcjonalny.
- `mood`: 1–7 obowiązkowe; `sleepScore`, `energyScore`, `stressScore`: opcjonalne 1–7 lub `null`.
- `text`, `originalText`: string. Aktualny zapis 1:1; starsze wpisy mogą mieć różnice.
- `mode`: `literal`, `tags`: tablica (pozostałość zgodności starszych wersji).
- Nie ma wersji schematu per wpis, ograniczeń długości tekstu, relacji ani załączników. Są to zaległości techniczne.

## Logika
- Ekrany: `home()`, `write()`, `history()`, `detail()`, `analysis()`, `more()`, przełączane przez `openView()` i `render()`.
- Wyszukiwanie: `normalizeSearch()`, `searchMatches()`, `RELATED_TERMS`, `historyResults()`; lokalne dopasowanie i ręczny słownik, **bez AI, bez rozpoznawania negacji**.
- Wyróżnienia: `searchExplanation()`, `markSearchMatches()`, `searchSnippet()`; tekst jest escapowany przez `esc()`.
- Wykresy: statystyki `metricStats()` i renderowanie słupków `metricPlot()`. Brakujące oceny nie liczą się do średniej. Żadnych zewnętrznych zapytań o zdrowie.

## Bezpieczeństwo i luki [PILNE PRZED PUBLIKACJĄ]
- Brak szyfrowania danych i kopii JSON, brak PIN/Face ID/Touch ID, brak kont/synchronizacji/serwera.
- Publiczny kod HTML jest dostępny każdemu; nie należy dodawać sekretów ani danych rzeczywistych.
- Zdjęcia, powiadomienia, backup zaszyfrowany i kompletne testy automatyczne — niezaimplementowane.
- IndexedDB snapshot jest źródłem przy starcie nawet gdy localStorage ma inną zawartość; przed rozwijaniem synchronizacji konieczny protokół konfliktów i wersji danych.
- Brak izolowanej strategii rollbacku/zapobiegania utracie przez równoległe karty, brak kontroli transakcji wielourządzeniowej.
- Zewnętrzny silnik dyktowania w iOS może korzystać z sieci; zależy od konfiguracji telefonu.
