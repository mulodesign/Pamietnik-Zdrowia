# Instrukcja odtworzenia projektu dla AI i programisty

Cel: dowolny kompetentny wykonawca, otrzymując **całe repozytorium** i tę dokumentację, powinien umieć uruchomić **wierną wersję prototypu webowego**, a następnie rozwijać go według uzgodnionych wymagań. To nie jest deklaracja, że sam tekst zastąpi źródła.

## Materiały wejściowe
1. `index.html` — aktualne źródło prawdy i wykonywalna implementacja; nie zastępuj go opisem.
2. `README.md` i pliki `docs/*.md` — kontekst, wymagania, ograniczenia, operator, testy.
3. Historia commitów Git — jeśli potrzebna analiza zmian, nie jest niezbędna do uruchomienia bieżącej strony.
4. Potwierdzone ustawienia wdrożeniowe GitHub Pages. Bez nich lokalne uruchomienie jest możliwe, ale publikacja wymaga konfiguracji uprawnień.

## Odtworzenie obecnego prototypu 1:1
1. Sklonuj `https://github.com/mulodesign/Pamietnik-Zdrowia.git`.
2. Wybierz stan referencyjny `main` odpowiadający numerowi v0.13.0 w kodzie, albo zapisz konkretny SHA commitu przed rozpoczęciem.
3. Nie instaluj nieudokumentowanych frameworków. Obecny prototyp to jeden plik HTML z CSS i JavaScript.
4. Otwórz go przez zwykły serwer HTTP (np. `python3 -m http.server 8080` w katalogu repo) i wejdź na `http://localhost:8080/`; dla testów storage używaj zawsze tego samego origin.
5. Sprawdź Start, Wpis, Historię, Analizę, Więcej i wszystkie scenariusze z `TESTY_I_ZMIANY.md`.
6. Wygeneruj wyłącznie **fikcyjne dane** testowe; sprawdź odczyt, zapis, migrację i JSON import/export.
7. Dla identycznego publicznego URL użyj GitHub Pages tego samego repo; URL na nowym koncie będzie inny. Nie zmieniaj adresów w dokumentacji bez weryfikacji.
8. Zapisz `git rev-parse HEAD`, przeglądarki, systemy, testy i listę odstępstw. **Wierne odtworzenie** = ten sam kod i potwierdzona zgodność wyników testów. Nowa architektura mobilna to **oddzielne wdrożenie**, nie kopia HTML 1:1.

## Reguły obowiązkowe dla asystenta AI
- **Najpierw czytaj wszystkie źródła; nie wymyślaj niedostępnych plików ani integracji.**
- Dziel odpowiedź na [DZIAŁA], [PLAN], [NIEPOTWIERDZONE]. Nie ogłaszaj wdrożenia, zanim kod nie został zapisany, przetestowany i uruchomiony.
- Zmiany minimalne i zgodne z żądaniem. Nie modyfikuj niepowiązanych ekranów.
- Nie kasuj, nie nadpisuj i nie migruj danych użytkownika bez bezpiecznego scenariusza aktualizacji, testów i możliwości odzyskania.
- Po zmianie weryfikuj JavaScript, renderowanie ekranów, save/reload, migrację istniejących wpisów, funkcję wyszukiwania i analizy; testy na urządzeniu raportuj oddzielnie od symulowanych.
- Unikaj twierdzeń, że lokalny słownik synonimów to model AI lub diagnoza.
- Traktuj publiczne repo i jego Pages jako niezaufane miejsce dla danych rzeczywistych i sekretów.
- Zaktualizuj właściwe pliki dokumentacji razem z implementacją; wpisz datę, wersję i zakres zmian.
- Jeśli wykonanie zależy od Apple Developer/Google Play/urządzeń/kont, opisz wymagania i brakujące potwierdzenia zamiast dopisywać fikcyjne identyfikatory.

## Następne zadania przed produkcją
1. Spis wymagań bezpieczeństwa i prywatności, audyt zagrożeń, projekt kluczy i odzyskiwania dostępu.
2. Wybór stosu natywnego/cross-platform (Flutter to rozważana opcja), model bazy offline, niezależnego szyfrowanego backupu i migracji.
3. Lokalny scheduler powiadomień: wybór godziny, opt-out, opcjonalne pomijanie dni z wpisem; testy time-zone/DST/uprawnień.
4. Projekt zdjęć i chronologicznych porównań z limitami miejsca i ochroną metadanych.
5. Konfiguracja buildów, podpisywania, dystrybucji testowej, instalacji i aktualizacji.
6. Testy dostępności dla osób 60+, prywatności, odzyskania danych oraz długiej historii.
