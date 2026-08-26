# Jak pracujemy — Asumpt

## Sposób odpowiadania (najważniejsze)

Kris nie chce opisów procedur ani relacji z pracy. Nie pisz, co po kolei
robiłeś, jakich narzędzi użyłeś, jak zbudowałeś plik ani jak coś sprawdziłeś.

Odpowiedź ma zawierać wyłącznie:
1. **Efekt** — co jest zrobione, krótko.
2. **Wnioski** — jeśli coś istotnego wyszło przy okazji.
3. **Pytania** — tylko gdy czegoś nie wiesz albo decyzja należy do Krisa.

Zasady:
- Krótko. Bez wstępów, bez podsumowań na końcu, bez chwalenia się.
- Bez nagłówków „co zrobiłem", bez list kroków technicznych.
- Nie tłumacz działania kodu, CSS-a ani narzędzi, chyba że Kris wprost pyta.
- Znalezione błędy zgłaszaj jednym zdaniem: co jest zepsute i co proponujesz.
- Po polsku.

## Projekt

Przebudowa strony sklepu Asumpt (Pl. Wilsona 4, Warszawa Żoliborz).

- Kierunek wizualny: grafit / tytan / czerwień / biel. Jeden świat, ciemny.
- Czcionki: Saira Condensed (nagłówki), Literata (tekst), IBM Plex Mono
  (etykiety, liczby, godziny). Wszystkie z Google Fonts.
- Czerwień tylko tam, gdzie jest w sklepie: logotyp, kropki, numer domu.
- Godziny: Pn–Pt 11:00–19:00, sobota 11:00–14:00, niedziela nieczynne.
- Sklep jest tuż przy wyjściu ze stacji metra Plac Wilsona — ok. 10 metrów.
  Nigdy nie pisz „2 minuty pieszo".
- Nie używaj słowa „bezpłatna" o konsultacji — sugeruje, że kolejna jest płatna.

## Czego nie ruszać

- Repozytorium `epapierosy-asumpt.pl` zasila działający sklep. Tylko odczyt,
  bez wyraźnej zgody Krisa nic tam nie wypychamy.
- Nie łączyć linkiem asumpt.waw.pl ze stroną e-papierosową. Nigdy.
- Dane firmowe (nazwa, adres, telefon, CEIDG, wizytówka Google) są sprawdzone
  i zamknięte. Nie audytować ponownie.
- Nazwy plików podstron są zaszyte w karuzeli — nie zmieniać.

## Infrastruktura

- **GitHub `vape-asumpt.pl`** (to repo, dawniej `asumpt-nowa-strona`, prywatne) —
  branch `main`, stąd leci deploy.
- **GitHub `wizytowka-sklepu-asumpt`** (prywatne) — inna, starsza strona: sklep
  z bateriami/zegarkami/paskami pod tym samym adresem (Pl. Wilsona 4). Domena
  `asumpt.waw.pl`. Osobny biznes, osobny kod, nie mylić z tym repo.
- **GitHub `epapierosy-asumpt.pl`** — żywy sklep e-papierosowy, tylko odczyt
  (patrz „Czego nie ruszać" wyżej).
- **Netlify**, zespół „jacekmag's team" — trzy projekty, każdy „Deploys from
  GitHub" 1:1 z repo powyżej: `vape-asumpt.pl`, `asumpt.waw.pl`,
  `epapierosy-asumpt.pl`. Push na `main` w danym repo = automatyczny redeploy.
- **DNS `vape-asumpt.pl`** — nameservery wskazują na Netlify DNS
  (`dns1–4.p09.nsone.net`), ustawione przez INTEN na prośbę Krisa. Nowe rekordy
  (np. TXT do weryfikacji Google) dodaje się w Netlify → DNS, nie u rejestratora.
- **Google Search Console** — usługa `vape-asumpt.pl` dodana i zweryfikowana
  metodą DNS TXT, sitemap.xml przesłana, strona główna zaindeksowana
  (sierpień 2026).

## Wzorzec: strona Kontakt

`02-wnetrze-sklepu/kontakt.html` jest stroną wzorcową. Kolory, czcionki,
odstępy i sposób budowania grafik biorą się z niej, nie wymyślamy od nowa.

### Kolory (zmienne CSS na :root)
    --ground #101418   tło strony
    --plate  #171D23   tło kafelków i pasków
    --line   #28323A   ramki;  --line-soft #202830  linie wewnętrzne
    --ink    #F2F4F5   tekst główny i biel w grafikach
    --ink-2  #AEBAC1   tekst drugorzędny
    --muted  #7C8A93   etykiety wygaszone
    --red    #E5120A   akcent — logotyp, kropki, numery, etykiety, znaczniki

### Czcionki
    Saira Condensed  nagłówki, przyciski, nazwy w kafelkach (300 i 500)
    Literata         tekst czytany (300)
    IBM Plex Mono    etykiety, godziny, liczby, podpisy w grafikach

### Typografia
    h1     clamp(36px, 6.65vw, 78px), wersaliki, waga 300
    h2     clamp(27px, 4.2vw, 40px), wersaliki, waga 300
    tekst  17px / 1.65, akapity do 62–66 znaków w wierszu
    etykiety mono 10px, letter-spacing .18em, wersaliki, czerwone

### Odstępy
    section.wrap{padding-top:34px}  — odstęp nad nagłówkiem sekcji.
    UWAGA: klasa .wrap zeruje padding selektora `section`, więc odstęp
    musi być ustawiony z tą samą specyficznością (`section.wrap`).

### Powtarzalne elementy
    .sign    czarna tabliczka z czerwonymi kropkami — jak markiza sklepu
    .facts   pasek danych w kolumnach, etykiety czerwone
    .door    lista jak na drzwiach: numer po lewej, cienkie kreski
    .faq     details/summary, "+" i "–" czerwone
    .routes  siatka kafelków z czerwoną plakietką u góry

### Grafiki wektorowe (plan placu jako wzór)
    - Wyłącznie linie proste: poziome, pionowe, skosy. Żadnych łuków
      i krzywych w wskazówkach ani wyliczeniach.
    - Podziałka jak na tarczy przyrządu: kreski co 5 stopni, dłuższe co 30.
    - Podpisy: IBM Plex Mono 12px, kolor --ink, wersaliki, letter-spacing .14em.
    - Nazwa obiektu: Saira Condensed 19px, --ink, nad poziomym odcinkiem
      wskazówki.
    - Znacznik miejsca: czerwony punkt + radar (obracająca się wycinka
      i rozchodzące się pierścienie). Animacje wyłączane przy
      prefers-reduced-motion.

### Zasady techniczne
    - Zawsze <meta charset="utf-8"> — bez tego polskie znaki sypią się
      na serwerze.
    - Jeden świat, ciemny. Bez trybu jasnego.
    - Zasoby jako osobne pliki w katalogu głównym, nie osadzane w data:.
    - Dane strukturalne na każdej stronie: LocalBusiness/Store, FAQPage
      i BreadcrumbList.
    - Po każdej zmianie sprawdzić stronę na 1280 i 390 px.
