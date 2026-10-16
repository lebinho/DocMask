# 🛡️ DocMask (v6) - Lokalna Anonimizacja Dokumentów

[![Version](https://img.shields.io/badge/version-v6.0-emerald.svg)](https://github.com/lebinho/DocMask)
[![Privacy](https://img.shields.io/badge/privacy-100%25%20Client--Side-blue.svg)](https://github.com/lebinho/DocMask)
[![Author](https://img.shields.io/badge/author-lebinho-0f172a.svg)](https://github.com/lebinho)

> **Krótki opis do sekcji „About” na GitHubie:**  
> 🛡️ **DocMask** - lekka, jednoplikowa aplikacja przeglądarkowa (100% Client-Side) do automatycznego wykrywania i trwałego maskowania danych osobowych, podpisów i pieczątek w plikach PDF, DOCX oraz skanach przed przesłaniem ich do AI.

---

## 🎯 O projekcie

**DocMask** to narzędzie stworzone z myślą o bezpiecznym przygotowywaniu dokumentów (umów kredytowych, polis ubezpieczeniowych, aktów notarialnych, wyciągów bankowych, pasków wynagrodzeń czy faktur) przed ich dalszym udostępnieniem lub analizą w modelach sztucznej inteligencji (LLM / AI).

Cała aplikacja mieści się w **jednym pliku `DocMask.html`** i działa w **100% lokalnie w pamięci przeglądarki użytkownika**. Żadne pliki, obrazy ani teksty nigdy nie opuszczają Twojego komputera.

---

## ✨ Główne możliwości

### 1. Automatyczne wykrywanie polskich danych wrażliwych (1-Click)
Silnik analizuje zarówno warstwę tekstową PDF/DOCX, jak i układ tabelaryczny oraz wielokolumnowy, automatycznie maskując na czarno:
* **Numery PESEL** (11 cyfr, z korekcją typowych przekłamań OCR),
* **Dowody osobiste i paszporty** (np. `ABC 123456`),
* **NIP / REGON / KRS** (zarówno osobiste, jak i firmowe w kontekście tabel),
* **Numery kont bankowych (NRB / IBAN)** (formaty 26-cyfrowe oraz `PL...`),
* **Numery telefonów** (polskie formaty komórkowe, stacjonarne i infolinie),
* **Adresy e-mail** (w tym wieloczłonowe domeny firmowe i skany pod kątem),
* **Adresy zamieszkania, nieruchomości i kody pocztowe** (z obsługą skrótów `ul.`, `al.`, adresów pisanych `WIELKIMI LITERAMI`, adresów bez skrótu `ul.` oraz adresów łamanych między wierszami kolumny),
* **Imiona i nazwiska** (obsługa nazwisk dwuczłonowych z dywizem np. `Kowalski-Nowak`, imion i nazwisk pisanych `WIELKIMI LITERAMI` oraz propagacja wykrytych nazwisk na wszystkie strony dokumentu),
* **Polisy / VIN / Księgi Wieczyste (KW) / Faktury / ID klienta** (np. `GD1G/00000000/0`, `FV/2026/...`, zamaskowane karty płatnicze `**** 1234`),
* **Osobno sterowane wykrywanie podpisów i pieczątek**:
  * **Ramki i pola podpisów** - automatyczne maskowanie pól formularzowych nad podpisami *Podpis Klienta*, *Ubezpieczający* itp.,
  * **Podpisy odręczne (tusz)** - wizualna detekcja śladów niebieskiego długopisu na białym tle papieru,
  * **Pieczątki i agencje** - wykrywanie i maskowanie pieczęci firmowych oraz agencyjnych,
* **Własne słowa i rdzenie słów** - możliwość wpisania własnych fraz lub rdzeni nazwisk (np. wpisanie `Kowalsk` automatycznie zamaskuje odmiany `Kowalski`, `Kowalskiego`, `Kowalskiej`).

### 2. Lokalny silnik OCR dla skanów i zdjęć
* Wbudowana obsługa **Tesseract.js (`pol+eng`)** uruchamiana automatycznie dla zdjęć (`.jpg`, `.png`, `.webp`) oraz skanów PDF pozbawionych warstwy tekstowej.
* Wyznaczanie masek bezpośrednio na podstawie współrzędnych pojedynczych słów (`word.bbox`), co eliminuje przesunięcia ramek w szerokich tabelach i na pochyłych skanach.

### 3. Ręczna korekta myszką lub dotykiem
* **Dodawanie maski**: przeciągnij myszką (lub palcem na ekranie dotykowym) w dowolnym miejscu na dokumencie, aby zamaskować wybrany obszar.
* **Usuwanie maski**: kliknij w istniejący czarny prostokąt, aby go usunąć.
* Każda ręcznie dodana maska automatycznie usuwa przykryte pod nią słowa również z widoku tekstowego, pliku Markdown oraz warstwy tekstowej PDF!

### 4. Bezpieczny eksport z oznaczeniem trybu (`A`, `B`, `C`) i znacznikiem czasu
Każdy wyeksportowany plik otrzymuje w nazwie sygnaturę `DocMask`, kod wybranego trybu oraz dokładną datę i godzinę pobrania (`RRRR-MM-DD_GG-MM-SS`):

* **📕 PDF (`.pdf`)**:
  * **`[Typ A] Hybrydowy dla AI` (`PDF-A-hybrydowyAI`)** - spłaszczony obraz strony z wypalonymi czarnymi prostokątami + osadzona warstwa tekstowa zawierająca wyłącznie słowa niezakryte (zamaskowane słowa są fizycznie zastępowane znacznikiem `[ZAMASKOWANO]`). Idealny do bezpośredniego wgrania do ChatGPT / Claude / Gemini.
  * **`[Typ B] Czysty tekstowy PDF dla AI` (`PDF-B-tekstAI`)** - lekki dokument PDF zawierający wyłącznie zanonimizowany tekst.
  * **`[Typ C] Tylko spłaszczony obraz` (`PDF-C-splaszczony`)** - PDF złożony wyłącznie z bitmap stron (brak warstwy tekstowej).
* **📝 Markdown (`.md`) (`MD-tekstAI`)** - ustrukturyzowany plik tekstowy gotowy do wklejenia do promptu AI.
* **📘 Microsoft Word (`.docx`)**:
  * **`[Typ A]` (`DOCX-A-tekst-i-obraz`)** - edytowalny tekst z zamaskowanymi danymi + obrazy stron dokumentu,
  * **`[Typ B]` (`DOCX-B-tylko-tekst`)** - tylko edytowalny tekst,
  * **`[Typ C]` (`DOCX-C-tylko-obrazy`)** - tylko spłaszczone obrazy stron.
* **🖼️ Obraz PNG (`.png`) (`PNG-obraz`)** - spłaszczony obraz PNG (w przypadku dokumentów wielostronicowych łączony w jeden arkusz).

---

## 🚀 Szybki start (Uruchomienie)

Aplikacja nie wymaga instalacji, serwera ani budowania projektu (Node.js / Docker nie są potrzebne):

1. Pobierz plik **[`DocMask.html`](https://github.com/lebinho/DocMask/blob/main/DocMask.html)** z tego repozytorium.
2. Otwórz plik `DocMask.html` dwuklikiem w dowolnej nowoczesnej przeglądarce internetowej (Chrome, Edge, Firefox, Brave, Safari).
3. Wgraj swój dokument przyciskiem **„📂 Wgraj plik (PDF / DOCX / Zdjęcie / TXT)”** i pobierz gotowy, zanonimizowany plik.

---

## 🧪 Dokumenty testowe

Do repozytorium dołączono archiwum [**zestaw_testowy_PL.zip**](https://github.com/lebinho/DocMask/blob/main/zestaw_testowy_PL.zip), zawierające testowe pliki do przetestowania możliwości aplikacji: wczytywania dokumentów, rozpoznawania tekstu (OCR), wykrywania i maskowania danych oraz eksportu wyników.

Pobierz i rozpakuj archiwum, a następnie wczytaj wybrane pliki do aplikacji.

---

## 🔒 Bezpieczeństwo i prywatność

* **Zero transferu danych dokumentu**: wszystkie operacje renderowania PDF, rozpoznawania OCR, wykrywania wyrażeń regularnych oraz generowania plików wyjściowych odbywają się wyłącznie w pamięci RAM Twojej przeglądarki.
* **Trwała anonimizacja**: w eksportowanych plikach PDF i PNG czarne prostokąty są wypalane bezpośrednio na płótnie obrazu (`HTML5 Canvas`), a przykryte nimi słowa nigdy nie trafiają do wyjściowej warstwy tekstowej.

---

## 👤 Autor

Projekt stworzony i rozwijany przez **lebinho**.
* Repozytorium GitHub: [https://github.com/lebinho/DocMask](https://github.com/lebinho/DocMask)
* Profil GitHub: [@lebinho](https://github.com/lebinho)
