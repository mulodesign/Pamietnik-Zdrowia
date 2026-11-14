# Rejestr wersji, testów i otwartych zagadnień

Stan na 2026-11-14. Dokumentowanie tej listy ma być częścią każdego wdrożenia.

## Historia ważnych etapów (na podstawie kodu i uzgodnień)
- **v0.6** — wycofanie zawodnego trybu automatycznego porządkowania dyktowania; zapis 1:1, opcjonalna ocena snu.
- **v0.7** — opcjonalne oceny energii i stresu.
- **v0.8** — pastelowe oceny dodatkowe w panelu rozwijanym.
- **v0.8.1–0.8.3** — diagnoza historii, eksport/import JSON i identyfikator pamięci.
- **v0.9.0** — IndexedDB + localStorage, próby migracji i odczytu po uruchomieniu.
- **v0.10.0** — analiza snu, energii i stresu.
- **v0.11.0** — wyszukiwanie po słowach i okresach.
- **v0.12.0** — opcjonalny ręczny słownik podobnych określeń.
- **v0.13.0** — wyróżnianie dopasowań i wyjaśnienia wyników.
- **Dokumentacja:** utworzona po v0.13.0; **nie zmienia funkcji prototypu**.

## Obowiązkowe testy przed każdą kolejną publikacją
| ID | Scenariusz | Oczekiwany wynik |
|---|---|---|
| T01 | Otwórz bez danych | Ekran Start nie jest pusty ani uszkodzony |
| T02 | Dodaj fikcyjny wpis z samopoczuciem 1–7 | Pojawia się w Historii; tekst 1:1 |
| T03 | Dodaj bez ocen dodatkowych | Zapis działa; średnie pomijają brakujące oceny |
| T04 | Dodaj sen/energia/stres, edytuj | Wartości po zapisie i ponownym otwarciu są takie same |
| T05 | Zamknij Safari i otwórz zwykłe karty | Wpisy widoczne, właściwa liczba |
| T06 | Otwórz prywatną kartę Safari | Nie zakładaj wspólnej historii ze zwykłym trybem |
| T07 | Uszkodzenie/niepowodzenie zapisu | Brak fałszywego komunikatu sukcesu; brak cichej utraty |
| T08 | Pobierz i zaimportuj kopię JSON | Wpisy odtworzone, duplikaty ID pomijane |
| T09 | Wyszukaj tekst i temat z/bez polskich znaków | Prawidłowe wyniki, czytelne podświetlenia |
| T10 | Wyszukiwanie podobnych określeń | Wyłączone: dosłowne; włączone: kontrolowane synonimy; zero diagnoz |
| T11 | Zakres 7/30/90 oraz daty od–do | Filtruje zgodnie z datami wpisów |
| T12 | Analiza prosta/rozszerzona | Średnie zgodne z danymi; brak nie jest zerem |
| T13 | Tekst z HTML/znakami specjalnymi | Jest tekstem, a nie kodem wykonywanym w interfejsie |
| T14 | Otwórz stary zapis sprzed ocen dodatkowych | Wpis działa, brak pól opcjonalnych nie psuje widoku |
| T15 | Wycofaj wdrożenie kodu bez czyszczenia danych | Starsza wersja nie niszczy wpisów; rollback sprawdzony |
| T16 | Urządzenie z dużą czcionką i ekranem małej szerokości | Formularz oraz przyciski nadal są czytelne i dostępne |

**Uwaga:** to plan regresji; przejście wszystkich testów na fizycznym iPhonie i Androidzie **nie zostało potwierdzone**. Każde wdrożenie powinno zawierać datę, SHA, środowisko, wynik i znalezione błędy.

## Dziennik testów operatora (szablon)
```
Data:
Wersja i SHA:
Urządzenie / system / przeglądarka / zwykły czy prywatny tryb:
Identyfikator pamięci przed i po:
Liczba wpisów przed i po:
Scenariusze wykonane:
Wyniki i zrzuty (bez danych osobowych):
Błędy:
Decyzja: zatwierdzenie / rollback / poprawki
```

## Otwarte zagadnienia
1. Produkcyjne szyfrowanie, PIN i biometria.
2. Niezależny, zaszyfrowany i przywracalny backup (oba obecne magazyny to jedna przeglądarka).
3. Wersjonowanie schematu i migracje bez utraty danych, także przy wielu otwartych kartach.
4. Powiadomienia dzienne z godziną wybieraną przez użytkownika i opcją pomijania dni z wpisem.
5. Zdjęcia, multimedia, katalog zdarzeń i dalsza rozbudowa analizy.
6. Pełne testy na iOS/Android i dystrybucja instalowalnej aplikacji.
7. Formalny plan bezpieczeństwa, wymagania prawne i polityka prywatności.
8. Zweryfikowany inwentarz rzeczywistych urządzeń, usług, uprawnień i procesu publikacji.
9. Testy automatyczne i kontrola jakości (obecnie w repo nie ma odrębnego zestawu testów).
