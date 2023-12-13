# Sprawdzian z zaawansowanych algorytmów Pythonie

## Przed rozpoczęciem pracy

1. Uruchom sesję udostępniania edytora (LiveShare). Możesz to zrobić **jeden** z **kilku** sposobów:

   - w menu `View` wybierz `Command Palette`, wpisz `Live Share` i wybierz `Live Share Start Read-Only Collaboration Session`
   - na lewym pasku kliknij ikonę Live Share i kliknij link `share with read-only`
   - na dolnym pasku kliknij `Live Share`

   Po tej operacji, w twoim schowku pojawi się link do udostępniania edytora

2. Stwórz plik `LiveShare.md`
3. Wklej link ze schowka do tego pliku i zapisz plik
4. Wypchnij ten plik do repozytorium (Commit + Push)

**Jest to warunek konieczny dla uzyskania pozytywnej oceny ze sprawdzianu.**

**Zabronione jest korzystanie z narzędzi do automatycznej generacji kodu, takich jak ChatGPT, Github Copilot, itp.**

### Wymagania funkcjonalne

W pliku `rent_a_car.py` napisz program, obsługujący wypożyczalnię samochodów.

Po uruchomieniu powinien on przyjmować po znaku zachęty `>` następujące komendy i wykonywać odpowiednio następujące operacje:

| Komenda                                            | Operacja                                                                                                                             | Warunek błędu                                                             |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| add car `plate_number`                             | Dodaje samochód o numerze tablicy rejestracyjnej `plate_number`                                                                      | Istnieje pojazd o `plate_number`                                          |
| book car `start_hour` `end_hour` `customer_name`   | Rezerwuje samochód w czasie pomiędzy `start_hour` a `end_hour` dla klienta o `customer_name`                                         | Nie ma dostępnych samochodów w okresie pomiędzy `start_hour` a `end_hour` |
| schedule `plate_number`                            | Wypisuje rozkład wypożyczeń samochodu o `plate_number`                                                                               | Samochód o rejestracji `plate_number` nie istnieje                        |
| schedule                                           | Wypisuje rozkład wypożyczeń dla wszystkich samochodów w wypożyczalni                                                                 |                                                                           |
| **(*)** utilization `start_hour` `end_hour` `plate_number` | Wypisuje procentowy poziom wykorzystania samochodu o rejestracji `plate_number`                                                      | Samochód o rejestracji `plate_number` nie istnieje                        |
| **(*)** utilization `start_hour` `end_hour`                | Wypisuje całkowity procentowy poziom wykorzystania wszystkich samochodów w wypożyczalni pomiędzy godzinami `start_hour` a `end_hour` |
| quit                                               | zamyka program                                                                                                                       |                                                                           |

Dla dowolnej komendy, o ile w opisie komendy nie wskazano inaczej, po jej należy wydrukować na ekran `OK` i wykonać operację. Gdy spełniony jest **warunek błędu**, należy wydrukować `ERROR` i nie wykonywać operacji (gdyż zapewne jest to niemożliwe).

Zakładamy, że użytkownik zawsze będzie wpisywał semantycznie poprawne komendy. To znaczy, że jeśli oczekujemy wpisania liczby, to użytkownik wpisze liczbę, a jeśli napisu, to napisu. Nie musimy więc obsługiwać błędów związanych niemożliwością obsługi niepoprawnych danych wejściowych.

Zadania oznaczone **(*)** są dodatkowe (dla chętnych) i nie są wymagane do uzyskania oceny ze bardzo dobry (5) ze sprawdzianu.

### Wymagania implementacyjne

- `plate_number` jest numerem rejestracyjnym samochodu. Składa się on z wielkich liter i cyfr. Jest unikalny, to znaczy, że nie mogą istnieć dwa samochody o tym samym numerze rejestracyjnym.
- `start_hour` i `end_hour` są wartościami reprezentującymi godziny. Są to liczby całkowite z przedziału od 0 do 23. `start_hour` jest zawsze mniejsze od `end_hour`.
- `name` jest imieniem i nazwiskiem wypożyczającego samochód. Z tego względu może zawierać spacje i znaki specjalne takie jak myślnik (na przykład osoba z dwuczłonowym nazwiskiem, drugim imieniem itd.).
- Wartości dla komendy `utilization` to procentowy poziom wykorzystania samochodu/samochodów w danym przedziale czasowym. Obliczamy ją z pełną dostępną precyzją (jako zmienną zmiennoprzecinkową), ale wypisujemy z dokładnością do jednego miejsca po przecinku.

  Dla przykładu, jeśli samochód jest wynajęty w godzinach 11-12, to jego poziom wykorzystania w godzinach 10-13 wynosi 33.(3)% (przez jedną godzinę samochód jest wynajęty, przez dwie jest nieużywany), a wypisujemy na ekran `33.3%`.

- Dla komendy `schedule` w kolejnych liniach wypisujemy `plate_number` oraz godziny rozpoczęcia i zakończenia wynajmy oraz imię i nazwisko użytkownika dla kolejnych wynajmów w formacie:
  ```
  start_hour end_hour name
  ```
  dla kolejnych samochodów.
  Wypisujemy je w kolejności chronologicznej. W przypadku, gdy samochód nie jest używany wypisujemy komunikat:
  ```
  FREE
  ```
  W przypadku gdy do komendy podawany jest `plate_number` samochodu, wypisujemy tylko wynajmy dla tego samochodu, nie drukując numeru rejestracyjnego. W przeciwnym wypadku wypisujemy wynajmy dla wszystkich samochodów.

## Przykład

```
> add car CAR1
OK
> add car CAR2
OK
> utilization 0 23
0.0%
> utilization 0 23 CAR1
0.0%
> book car 10 12 Kuba Sawulski
OK
> utilization 10 12
50.0%
> schedule
CAR1
  10 12 Kuba Sawulski
CAR2
  FREE
> schedule CAR1
10 12 Kuba Sawulski
> schedule CAR2
FREE
> book car 11 13 Inny Użytkownik
OK
> utilization 11 12
100.0%
> schedule
CAR1
10 11 Kuba Sawulski
CAR2
11 13 Inny Użytkownik
> book car 11 12 Trzeci Użytkownik
ERROR
> quit
```

Rozwiązanie należy oczywiście wypchnąć do repozytorium. Commitowanie pośrednich wyników w trakcie pracy jest również zdecydowanie zalecane.

**Powodzenia!**
