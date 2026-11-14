# Specyfikacja funkcjonalna — Pamiętnik Zdrowia

Stan: 2026-11-14. **[DZIAŁA]** oznacza funkcję stwierdzoną w `index.html`. **[PLAN]** to uzgodniony kierunek, jeszcze niewdrożony.

## Cel i odbiorcy
Jeden prosty pamiętnik samopoczucia dla wszystkich grup wiekowych, także 60+. Duże przyciski, czytelne napisy, ciepła kremowo-zielona estetyka, mało działań potrzebnych do wpisu. Bez diagnoz, obietnic medycznych i automatycznego przypisywania przyczyn dolegliwości.

## Ekrany [DZIAŁA]
- **Start:** ocena buźką 1–7, nowy wpis, skróty do historii/analizy/ustawień, ostatnie wpisy.
- **Wpis:** lokalna data, opcjonalny temat, obowiązkowe samopoczucie 1–7, notatka tekstowa, dyktowanie przez mikrofon systemowej klawiatury (aplikacja nie nagrywa samodzielnie), rozwijane opcjonalne oceny: **sen 1–7**, **energia 1–7**, **stres 1–7**. Wybór liczby można cofnąć. Zapis **dosłowny 1:1** względem tekstu dostarczonego do pola; aplikacja nie koryguje tekstu. **Uwaga:** systemowe rozpoznawanie mowy samo może zmieniać interpunkcję i używać usług sieciowych. Tekst wpisu jest wymagany do zapisu.
- **Historia:** wszystkie wpisy i filtrowanie po słowach/temacie; zakres dat: wszystkie / 7 / 30 / 90 dni / od–do. Można włączyć lokalne wyszukiwanie podobnych określeń z ręcznie utrzymywanym słownikiem. Znalezione fragmenty są wyróżniane; wynik opisuje przyczynę dopasowania. Brak rozumienia kontekstu i zaprzeczeń, dlatego możliwe są błędne dopasowania.
- **Szczegóły wpisu:** data, temat, oceny, treść; edycja i usunięcie pojedynczego wpisu po potwierdzeniu.
- **Analiza:** prosty i rozszerzony widok, okresy 7/30/90 dni, średnie czterech ocen, wykresy dzienne, tematy i wpisy z okresu. Brakujące opcjonalne oceny nie są zerami. **W skali stresu 7 oznacza większy stres**, a nie lepszy stan.
- **Więcej:** diagnostyka lokalnego storage, eksport/import pliku JSON, fikcyjne wpisy demonstracyjne, ostrzeżenia bezpieczeństwa. Zbiorcze kasowanie jest wyłączone.

## Przypomnienia [PLAN — wersja natywna]
- Użytkownik w menu włącza/wyłącza **codzienne przypomnienie o dokonaniu wpisu** i wybiera godzinę.
- Urządzenie pokazuje lokalne powiadomienie, którego naciśnięcie otwiera formularz nowego wpisu.
- Opcja „Nie przypominaj, gdy jest już dzisiejszy wpis” — preferowana, konfigurowalna.
- Należy zaprojektować poprawne działanie po zmianie strefy czasowej, zmianie czasu letniego/zimowego, restarcie i odmowie uprawnień.
- Bez wysyłania treści zdrowotnych do zewnętrznego serwera. Tekst powiadomienia neutralny.
- **Nie jest wdrożone w prototypie GitHub Pages.** Brak gwarancji przypomnień przy zamkniętej przeglądarce.

## Wersja docelowa mobilna [PLAN]
- Samodzielne aplikacje iOS i Android; docelowe podejście technologiczne do zatwierdzenia podczas implementacji (Flutter rozważany, nie jest częścią aktualnego repo).
- Szyfrowana baza lokalna, dostęp PIN/biometria, obsługa migracji, wersjonowane bezpieczne kopie zapasowe, odzyskanie po zmianie telefonu.
- Możliwe zdjęcia przy wpisie i porównania chronologiczne — **brak w aktualnym prototypie**.
- Lekkie animacje wyłącznie przy pierwszym wejściu/otwarciu książki; codzienny interfejs bez animacji utrudniających obsługę.
- Oddzielenie informacji zdrowotnych od ewentualnych zewnętrznych zasobów językowych czy pogodowych.
- Testy na realnych urządzeniach, dystrybucja testowa osobno dla iOS i Androida.

## Kryteria jakości
1. Najważniejsza czynność — zapis wpisu — ma być szybka i zrozumiała dla osób 60+.
2. Żaden upgrade nie może celowo wyzerować istniejącej historii; migracje muszą mieć testy.
3. Nie przedstawiamy heurystyk słownikowych jako analizy AI ani hipotez jako diagnoz.
4. Każdy nowy ekran/funkcja trafia do dokumentacji operatorskiej i do testów regresyjnych.
