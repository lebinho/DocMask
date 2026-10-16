# Maskowanie danych w dokumentach

Proste narzędzie przeglądarkowe do zakrywania danych w dokumentach przed ich udostępnieniem lub dalszą analizą.

Cały kod aplikacji - interfejs, style i logika - znajduje się w jednym pliku HTML. Nie wymaga instalowania programu ani uruchamiania własnego serwera.

## Funkcje

- Wczytywanie PDF, DOCX, TXT oraz obrazów PNG, JPG i WebP.
- OCR dla zdjęć i skanów z obsługą języka polskiego i angielskiego.
- Automatyczne wykrywanie wybranych kategorii danych, m.in. numerów PESEL, danych kontaktowych, adresów i numerów rachunków.
- Dodawanie własnych słów i fraz do zakrycia.
- Ręczne zakrywanie fragmentów dokumentu.
- Podgląd graficzny i tekstowy.
- Eksport do PDF, DOCX, Markdown i PNG.

## Uruchomienie

1. Pobierz plik HTML aplikacji.
2. Otwórz go w przeglądarce.
3. Wczytaj dokument lub skorzystaj z wbudowanego przykładu.
4. Wybierz kategorie danych do zakrycia.
5. Sprawdź wynik i dodaj ręczne poprawki.
6. Pobierz dokument w wybranym formacie.

## Jeden plik, bez instalacji

Aplikacja jest dostarczana jako jeden plik HTML, który można łatwo przenosić między komputerami.

Korzysta jednak z bibliotek, czcionek i zasobów OCR pobieranych z internetu. Jeden plik HTML nie oznacza więc pełnego działania offline.

## Przetwarzanie dokumentów

Odczyt dokumentów, OCR i maskowanie są wykonywane w przeglądarce. Aplikacja nie wymaga własnego backendu do przetwarzania plików.

Należy jednak uwzględnić połączenia z zewnętrznymi dostawcami zasobów. Przed użyciem dokumentów poufnych sprawdź kod, ruch sieciowy i wymagania bezpieczeństwa swojego środowiska.

## Dokumenty testowe

W folderze `zestaw_testowy_PL` dołączono dokumenty testowe z fikcyjnymi danymi.

Można ich użyć do sprawdzania:
- wczytywania różnych formatów;
- rozpoznawania tekstu przez OCR;
- automatycznego wykrywania danych;
- ręcznego zakrywania;
- eksportu i kontroli wynikowych plików.

## Ograniczenia

- Automatyczne wykrywanie może pominąć dane lub zakryć niewłaściwy fragment.
- Jakość OCR zależy od czytelności zdjęcia lub skanu.
- Import DOCX odczytuje tekst głównej treści i nie zachowuje pełnego układu oryginału.
- Narzędzie nie gwarantuje pełnej anonimizacji.

**Przed udostępnieniem pliku zawsze sprawdź wynik eksportu, zarówno jego wygląd, jak i możliwy do odczytania tekst.**
