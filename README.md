<p align="center"><img src="assets/leaderboard.png" alt="Slayer - leaderboard baseline'u" width="700"/></p>

<h1 align="center">Slayer</h1>

<h3 align="center">Otwarte laboratorium polskiego LLM: pomiar Bielika i Qwena na polskich benchmarkach, bez benchmaxxingu.</h3>

<p align="center">
  <img src="https://img.shields.io/badge/Python-harness-3776AB?style=for-the-badge&logo=python" alt="Python"/>
  <img src="https://img.shields.io/badge/Next.js-strona_labu-000000?style=for-the-badge&logo=nextdotjs" alt="Next.js"/>
  <img src="https://img.shields.io/badge/Hugging_Face-datasety-FFD21E?style=for-the-badge&logo=huggingface" alt="Hugging Face"/>
  <img src="https://img.shields.io/badge/Ollama-runtime-000000?style=for-the-badge&logo=ollama" alt="Ollama"/>
  <img src="https://img.shields.io/badge/licencja-MIT-97CA00?style=for-the-badge" alt="MIT"/>
</p>

---

## Spis treści

- [O labie](#o-labie)
- [Screenshoty](#screenshoty)
- [Kod źródłowy](#kod-źródłowy)
- [Stack](#stack)
- [Moja rola](#moja-rola)
- [Statystyki](#statystyki)
- [Kontakt](#kontakt)

---

## O labie

Polskich modeli językowych nie da się porównać na oko. Zagraniczne benchmarki nie mierzą polszczyzny urzędowej i prawniczej, a wyniki z publikacji trudno powtórzyć. Zespół, który wybiera polski model do produktu, nie ma wiarygodnego, publicznego punktu odniesienia.

Slayer to otwarte laboratorium, które taki punkt buduje. Mierzy Bielik-11B-v3 kontra Qwen3.5-9B na polskich egzaminach i zadaniach: MCQ, PoQuAD, FLORES. Metodyka jest publiczna: dekontaminacja zbiorów, karty danych, powtarzalne skrypty. Wyniki lądują na żywym leaderboardzie [slayer.fabryka.ai](https://slayer.fabryka.ai).

Lab jest w fazie baseline'u i podjął decyzję: baza do dalszej pracy to Qwen. Plan na kolejne fazy to tani SFT/GRPO bez pełnego CPT. Kod jest publiczny na licencji MIT.

---

## Screenshoty

| Leaderboard: Bielik-11B-v3 kontra Qwen3.5-9B na polskich benchmarkach | Wyniki per zadanie w bench explorerze |
|:---:|:---:|
| ![Leaderboard baseline'u](assets/leaderboard.png) | ![Bench explorer](assets/bench-explorer.png) |

| Strona zespołu labu: członek od czerwca 2026 |
|:---:|
| ![Strona zespołu labu](assets/team.png) |

> **Nota:** kadry z publicznych stron labu (slayer.fabryka.ai), wrzesień 2026.

---

## Kod źródłowy

Kod labu jest otwarty: [slayerlabs/slayer](https://github.com/slayerlabs/slayer) (MIT). To repo to wizytówka mojego wkładu: opis, kadry i lista PR-ów.

---

## Stack

### Harness pomiarowy

```
Python + pytest        // skrypty bench: MCQ, PoQuAD, tokenizer fertility
Hugging Face datasets  // Global-MMLU PL, PoQuAD, FLORES
MinHash + diakrytyki   // dekontaminacja: warstwa doslowna i near-dup
Ollama                 // lokalny runtime modeli
```

### Strona labu

```
Next.js + React        // leaderboard, bench explorer, progress
Vercel                 // hosting i analytics
```

---

## Moja rola

Lab prowadzi [Kacper Wikieł](https://github.com/kwikiel): koncepcja, ML i infrastruktura, większość commitów. Ja jestem członkiem organizacji od czerwca 2026. Mój wkład to 7 zmergowanych PR-ów, wszystkie wokół czystości i powtarzalności pomiaru:

- **Warstwa near-dup w dekontaminacji** ([#29](https://github.com/slayerlabs/slayer/pull/29)) - dotychczasowy audyt łapał tylko kontaminację dosłowną, n-gramy słów. Mój moduł łapie kopie bez polskich znaków i lekko przeredagowane itemy. CPU-only
- **Loader Global-MMLU PL** ([#31](https://github.com/slayerlabs/slayer/pull/31)) - polski MMLU jako benchmark `mmlu_pl` w harnessie MCQ. Publiczny dataset, deterministyczny split testowy
- **Guardy ewaluacji** ([#60](https://github.com/slayerlabs/slayer/pull/60)) - skrypty PoQuAD i tokenizer fertility przestały się wywalać na pustych wynikach. Zdegenerowany wynik nie wygrywa już tabeli tokenizerów
- **Powtarzalność ścieżek** ([#86](https://github.com/slayerlabs/slayer/pull/86)) - jedna zmienna `BENCH_OUT` zamiast zahardkodowanej ścieżki autora w czterech skryptach. Benchmark odpala u każdego, nie tylko u twórcy
- **Łatki bezpieczeństwa** ([#32](https://github.com/slayerlabs/slayer/pull/32), [#87](https://github.com/slayerlabs/slayer/pull/87)) - postcss (CVE-2026-41305) i undici (4 alerty Dependabot, w tym DoS na WebSocket)
- **Poprawki nawigacji** ([#61](https://github.com/slayerlabs/slayer/pull/61)) - aktywny stan zagnieżdżonych pozycji menu, linki zewnętrzne otwierane w nowej karcie

Czego nie robiłem: treningu modeli i frontendu labu. Moje PR-y pilnują, żeby pomiar był czysty i powtarzalny.

---

## Statystyki

### Mój wkład

| Metryka | Wartość |
|---|---|
| **Zmergowane PR-y** | 7 (jeden dzień pracy, 2026-06-28) |
| **Obszary** | dekontaminacja, loadery, guardy ewaluacji, repro, bezpieczeństwo |
| **Łatki CVE** | postcss (CVE-2026-41305), undici (4 alerty Dependabot) |
| **Członek organizacji** | od czerwca 2026 |

### Lab

| Metryka | Wartość |
|---|---|
| **Modele baseline** | Bielik-11B-v3, Qwen3.5-9B |
| **Benchmarki** | MCQ (mmlu_pl), PoQuAD, FLORES |
| **Faza** | baseline, plan: SFT/GRPO na Qwen |
| **Lead** | [Kacper Wikieł](https://github.com/kwikiel) |

---

## Kontakt

| Platforma | Link |
|---|---|
| **WWW** | [kamilkaczmareksolutions.com](https://kamilkaczmareksolutions.com) |
| **GitHub** | [kamilkaczmareksolutions](https://github.com/kamilkaczmareksolutions) |
| **LinkedIn** | [Kamil Kaczmarek](https://www.linkedin.com/in/kamilkaczmareksolutions) |
| **Email** | [recruitment@kamilkaczmareksolutions.com](mailto:recruitment@kamilkaczmareksolutions.com) |

---

**Slayer** - otwarte laboratorium polskiego LLM. Lab: [slayerlabs](https://github.com/slayerlabs).

<p align="center"><em>Wkład commitowy: <a href="https://github.com/kamilkaczmareksolutions">Kamil Kaczmarek</a>. Lab prowadzi <a href="https://github.com/kwikiel">Kacper Wikieł</a>.</em></p>
