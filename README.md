# Kanał komunikatów — Szlaki Szczawnicy

Publiczny kanał powiadomień dla aplikacji **Szlaki Szczawnicy**.

To repozytorium zawiera **wyłącznie** plik `komunikaty.json`. Kod aplikacji,
trasy i zdjęcia są w osobnym, prywatnym repozytorium.

Adres kanału, z którego czytają telefony:

```
https://siniar1990.github.io/szlaki-komunikaty/komunikaty.json
```

## Jak wysłać komunikat

Z katalogu prywatnego repo aplikacji:

```bash
python3 tools/komunikaty/wyslij.py "Nowa trasa rowerowa" \
    "Do Czerwonego Klasztoru — 9,7 km wzdłuż Przełomu Dunajca." \
    --trasa R1 --dni 30
```

Skrypt sam dopisuje wpis, commituje i wypycha. Podgląd zawartości: `--lista`,
usunięcie: `--usun <id>`.

## Format

```json
{
  "wersja": 1,
  "komunikaty": [
    {
      "id": "2026-07-27-nowa-trasa-rowerowa",
      "tytul": "Nowa trasa rowerowa",
      "tresc": "Do Czerwonego Klasztoru — 9,7 km wzdłuż Przełomu Dunajca.",
      "od": "2026-07-27T10:00:00Z",
      "do": "2026-08-26T10:00:00Z",
      "waga": "info",
      "trasa_id": "R1",
      "link": null
    }
  ]
}
```

| pole | znaczenie |
| --- | --- |
| `id` | stały identyfikator; po nim telefon poznaje, że już pokazał ten komunikat |
| `od` / `do` | okno ważności — po `do` komunikat znika z aplikacji |
| `waga` | `info` (tylko w „Aktualnościach”), `ostrzezenie`, `pilne` (powiadomienie systemowe) |
| `trasa_id` | opcjonalne — tapnięcie otwiera ekran tej trasy |
| `link` | opcjonalny adres otwierany po tapnięciu |

## Ważne

Dostawa **nie jest natychmiastowa**. Aplikacja sprawdza kanał przy uruchomieniu
i po powrocie z tła, nie częściej niż raz na 30 minut. Kto nie otworzy aplikacji
przez tydzień, zobaczy komunikat po tygodniu — dlatego każdy wpis ma datę ważności.

Wszystko w tym repozytorium jest publiczne. Nie wpisuj tu niczego prywatnego.
