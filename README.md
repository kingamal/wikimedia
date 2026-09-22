# Sezonowy rytm polskiej Wikipedii

Interaktywny dashboard pokazujący oglądalność polskiej Wikipedii w latach 2016–2026.
Praca przygotowana na **#BI_NGO 2026**, wolontariat analityczny na 25-lecie polskiej Wikipedii,
we współpracy ze Stowarzyszeniem Wikimedia Polska.

## Co zawiera

- **Sezonowość**: średnia oglądalność w poszczególnych miesiącach (2016–2025); kolorem wyróżnione miesiące powyżej średniej rocznej
- **Udział urządzeń**: dziesięcioletni trend: desktop, mobile web i aplikacja mobilna jako procent całego ruchu
- **Trend długookresowy**: 126 miesięcy, od stycznia 2016 do czerwca 2026
- **Porównanie z kontekstem**: ruch Wikipedii zestawiony z liczbą mieszkańców
  i internautów w Polsce, w skali indeksowej 2016 = 100
- **Mapa ciepła**: miesiąc × rok, ze skalą i oznaczeniem braku danych
- **Obserwacje**: komentarz do każdego wykresu

## Jak uruchomić

Dashboard korzysta z lokalnych fontów i logotypów, więc trzeba go serwować przez HTTP
(otwarcie `index.html` podwójnym kliknięciem zablokuje wczytanie fontów przez politykę CORS).

**Opcja 1: serwer Pythona** (najprościej):

```bash
python -m http.server 8000
```

Następnie otwórz <http://127.0.0.1:8000/>.

**Opcja 2: Live Server w VS Code**

1. Zainstaluj rozszerzenie „Live Server"
2. Kliknij prawym przyciskiem na `index.html` → „Open with Live Server"

## Struktura plików

```
wikipedia-seasonal/
├── index.html                              # Dashboard (dane wbudowane w plik)
├── data.json                               # Dane źródłowe + metadane metodologiczne
├── assets/
│   ├── js/
│   │   └── chart.umd.min.js                # Chart.js 4.4.1, MIT
│   ├── logos/
│   │   ├── wikipedia.svg                   # CC BY-SA 3.0
│   │   └── wikimedia-polska.svg            # CC BY 4.0
│   └── fonts/
│       ├── montserrat-latin-ext.woff2      # SIL OFL 1.1
│       └── source-serif-4-latin-ext.woff2  # SIL OFL 1.1
└── README.md
```

## Kluczowe obserwacje

- **Styczeń jest najsilniejszy** (354 mln wyświetleń średnio), **lipiec najsłabszy** (275 mln), różnica wynosi 29%
- **Rytm roku szkolnego** powtarza się w każdym roku bez wyjątku: wzrost od października, szczyt w styczniu i marcu, zapaść w wakacje
- **Przesunięcie na mobile, ale nie jednokierunkowe**: udział desktopu spadł z 68,2% (2016) do 39,4% (2023), po czym **odbił do 44,0% w 2025**. Mobile web przejął większość ruchu w 2022 roku
- **Aplikacja mobilna pozostaje marginalna**: poniżej 1% ruchu przez całe dziesięciolecie
- **Ruch ogółem maleje**: 3,84 mld wyświetleń w 2016 wobec 3,49 mld w 2025 (−9,2%)
- **2020 jako anomalia**: kwiecień (402 mln) i maj (407 mln) to najwyższe wartości w całym zbiorze poza styczniami. Sezonowość pękła w czasie lockdownu
- **Demografia nie tłumaczy spadku**: ludności Polski ubywa (−4%), ale internautów przybyło (+16%).
  Mimo to liczba wyświetleń przypadających na jednego internautę spadła o **21,7%**,
  ze 138 do 108 rocznie. Wikipedia traci nie dlatego, że jest nas mniej, tylko dlatego,
  że każdy sięga po nią rzadziej

## Identyfikacja wizualna

Dashboard stosuje system wizualny Wikimedia zgodnie z wytycznymi konkursu:

- **Kolory**: paleta [Core](https://meta.wikimedia.org/wiki/Brand/colours) (biel, czernie 25/50/75)
  jako struktura oraz Legacy w wariantach AAA jako akcenty:
  niebieski `#0C57A8`, zielony `#246342`, czerwony `#970302`.
  Skala mapy ciepła zbudowana z Legacy Blue; wszystkie kombinacje tekst/tło mają kontrast co najmniej 4,5:1.
- **Typografia**: [Montserrat](https://meta.wikimedia.org/wiki/Brand/Typography) (nagłówki)
  i Source Serif 4 (tekst), wagi Regular i Bold, hostowane lokalnie z podzbiorem latin-ext
- **Logotypy**: Wikipedii i Wikimedia Polska w nagłówku

## Źródła danych

- **Zbiór**: miesięczna liczba wyświetleń stron pl.wikipedia.org w podziale na desktop, mobile web i aplikację mobilną
- **Pochodzenie**: Wikimedia Analytics, [Pageviews API](https://wikimedia.org/api/rest_v1/#/Pageviews%20data),
  udostępnione w repozytorium [BI_NGO 2026: Wikimedia Polska](https://github.com/bi-ngo-wolontariat/BI_NGO-2026-Wikimedia-Polska)
- **Zakres**: od stycznia 2016 do czerwca 2026 (126 miesięcy)
- **Filtr ruchu**: `agent=user`, dane nie obejmują ruchu botów i pełzaczy
- **Uwaga metodologiczna**: rok 2026 jest niepełny (dane do czerwca), dlatego został wyłączony
  z obliczeń średnich sezonowych i z wykresu udziału urządzeń. Średnie miesięczne liczą się
  z dziesięciu pełnych lat 2016–2025 (pole `years_count` w `data.json`). Wykres trendu
  długookresowego i mapa ciepła pokazują komplet 126 miesięcy; w mapie ciepła brakujące
  miesiące 2026 oznaczono jako „brak danych"

## Dane zewnętrzne

Karta porównawcza korzysta z dwóch wskaźników Banku Światowego dla Polski,
pobranych przez API 22 września 2026 roku:

- [`SP.POP.TOTL`](https://data.worldbank.org/indicator/SP.POP.TOTL?locations=PL): liczba ludności
- [`IT.NET.USER.ZS`](https://data.worldbank.org/indicator/IT.NET.USER.ZS?locations=PL): odsetek osób korzystających z internetu

Odsetek internautów za 2025 rok nie był jeszcze opublikowany, dlatego przyjęto
wartość z 2024 roku (88,6%). To założenie ostrożne: gdyby penetracja nadal rosła,
spadek liczby wyświetleń na internautę okazałby się jeszcze głębszy.
Wszystkie wartości pochodne zapisano w `data.json` w bloku `context`,
a opis źródeł w `meta.external_sources`.

## Technologie

HTML5, CSS3, Chart.js 4.4.1 (hostowany lokalnie, licencja MIT), Vanilla JavaScript.
Dashboard jest responsywny i nie wymaga połączenia z zewnętrznymi serwerami.

## Licencja

Wizualizacja: **Kinga Maleszewska**, MultiTask Creations, #BI_NGO 2026.
Logotypy i fonty na licencjach wskazanych w sekcji „Struktura plików".
