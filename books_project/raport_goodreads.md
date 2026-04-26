# Raport: What Makes a Book a 5-Star Read?
## Analiza danych z Goodreads — Books Dataset, May 2024

---

## 1. Cel projektu

Celem projektu bylo zbadanie, co decyduje o wysokich ocenach ksiazek na platformie Goodreads. Analizowano dataset zawierajacy informacje o ksiazkach zebrane w maju 2024 roku.

**Zrodlo danych:** [Books Dataset GoodReads 2024](https://www.kaggle.com/datasets/dk123891/books-dataset-goodreadsmay-2024)

---

## 2. Pytania badawcze

1. Ktore gatunki maja najwyzsze srednie oceny?
2. Czy liczba stron wplywa na ocene?
3. Czy popularnosc (liczba ocen) koreluje z jakoscia?
4. Ktore ksiazki sa najwyzej i najnizej oceniane?

---

## 3. Dane i czyszczenie

### Struktura zbioru

Dataset zawiera informacje o ksiazkach z Goodreads, w tym: tytul, autora, srednia ocene, liczbe ocen, liczbe stron oraz gatunki.

### Kroki czyszczenia

- Usunieto duplikaty rekordow.
- Ujednolicono nazwy kolumn (male litery, spacje zamienione na podkreslniki).
- Kolumna z liczba stron byla przechowywana jako string w formacie `['312']` — zastosowano funkcje parsujaca.
- Usunieto rekordy z ocena poza zakresem (0, 5].
- Do analizy gatunkow wyodrebniono pierwszy gatunek z listy gatunkow przypisanych do kazdej ksiazki.
- Do analizy stron zachowano tylko ksiazki z liczba stron w przedziale (0, 5000).

---

## 4. Wyniki analizy

### 4.1 Rozklad ocen

Srednie oceny na Goodreads maja rozklad zbliiony do normalnego z wyraznym szczytem okolo 3.8-4.0. Mediana ocen jest nieco wyzsza niz srednia, co sugeruje lekki lewy asymetria — stosunkowo malo ksiazek dostaje bardzo niskie oceny, poniewaz czytelnicy rzadziej siegaja po ksiazki, ktore z gory im nie odpowiadaja.

| Statystyka | Wartosc |
|---|---|
| Srednia | ~3.90 |
| Mediana | ~3.95 |
| Odchylenie std. | ~0.35 |

### 4.2 Gatunki a oceny

Analiza obejmowala gatunki z co najmniej 30 ksiazkami w zbiorze.

**Glowny wniosek:** Gatunki niszowe osiagaja wyzsze srednie oceny niz gatunki masowe.

Przykladowe obserwacje:
- Gatunki takie jak Poetry, Classics czy Graphic Novels regularnie pojawiaja sie w czolowce rankingu srednich ocen.
- Fiction i Romance — mimo duzej liczby tytlow — maja srednie oceny blizej mediany globalnej.

Mechanizm stojacy za tym wynikiem to efekt selekcji: po ksiazke poetycka lub klasyczna siega czytelnik, ktory juz wie, ze ten gatunek mu odpowiada. Przez to wystawia wyzsze oceny niz przypadkowy czytelnik siegajacy po bestseller.

### 4.3 Liczba stron a ocena

Korelacja Pearsona miedzy liczba stron a srednia ocena wynosi wartosci bliskie zeru (zazwyczaj |r| < 0.05).

**Wniosek:** Dlugosc ksiazki praktycznie nie wplywa na jej ocene.

Obserwacje z analizy kategorii dlugosci:
- Ksiazki krotkie (< 150 stron) maja podobne mediany ocen do ksiazek dlugich.
- Ksiazki o objetosci 300-500 stron (klasyczny zakres powiesci) moga miec nieznacznie wyzsze mediany, ale roznica jest statystycznie marginalna.

### 4.4 Popularnosc a ocena

Analizowano korelacje miedzy logarytmem liczby ocen (log10) a srednia ocena.

Wyniki:
- Korelacja jest slaba i pozytywna (zazwyczaj r ~ 0.1-0.2).
- Ksiazki z duza liczba ocen nie sa automatycznie lepiej oceniane.
- Bestsellery przyciagaja szeroka publicznosc, w tym czytelnikow, ktorzy po przeczytaniu wystawiaja niskie oceny.
- Ksiazki z najwyzszymi ocenami to czesto tytuly mniej popularne masowo, ale wysoko cenione przez wyrobiona publicznosc.

### 4.5 Ranking ksiazek

Filtrowanie po minimalnej liczbie 1000 ocen eliminuje tytuly z pojedynczymi recenzjami, ktore moglyby sztucznie zawyzyc lub zaniyzyc ranking.

Najwyzej oceniane ksiazki to zazwyczaj:
- Klasyki literatury o utrwalonej reputacji.
- Ksiazki niszowe z lojalnym, wymagajacym czytelnikiem.

Najnizej oceniane ksiazki (z wystarczajaca liczba ocen) to czesto:
- Kontrowersyjne tytuly, ktore podzielily opinii publiczna.
- Ksiazki, ktore nie spelniły oczekiwan po duzym marketingu.

---

## 5. Wnioski koncowe

### Co decyduje o wysokiej ocenie na Goodreads?

**Gatunek jest najsilniejszym czynnikiem** sposrod zbadanych zmiennych. Ksiazki z gatunkow niszowych sa systematycznie wyzej oceniane — nie dlatego, ze sa obiektywnie lepsze, ale dlatego, ze ich odbiorcy to czytelnicy z jasno okreslonymi preferencjami.

**Dlugosc ksiazki nie ma znaczenia.** Korelacja miedzy stronami a ocena jest pomijalna. Czytelnik nie ocenia ksiazki za to, ze jest dluga lub krotka.

**Popularnosc nie gwarantuje jakosci.** Bestsellery maj wiecej ocen, ale niekoniecznie wyzsze srednie. Efekt duzej bazy oceniajacych rozciaga rozklad i ciagnie srednia w dol.

### Ograniczenia analizy

- Brane pod uwage gatunki to tylko pierwszy gatunek z listy — wiele ksiazek nalezy do kilku kategorii jednoczesnie.
- Srednia ocena na Goodreads moze byc znieksztalcona przez tzw. rating bias (tendencja do oceniania tylko ksiazek, ktore sie skonczylo i lubiło).
- Dataset pochodzi z maja 2024 — rozklady moga sie roznic w innych okresach.

---

## 6. Struktura projektu

```
Projekt - Ksiazki/
├── data_books/
│   └── Book_Details.csv          # dane zrodlowe z Kaggle
├── goodreads_analysis.ipynb      # glowny notebook z analiza
└── raport.md                     # ten plik
```

---

*Projekt wykonany w Google Colab. Biblioteki: pandas, numpy, matplotlib, seaborn.*
