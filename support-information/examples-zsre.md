# zsre: 30 edits from realization 0, order 100 (checkpoint 1000)

Read `Capstan-README.md` first for what each column means. Answers are the exact greedy generations saved in the cell checkpoints (≤ 32 tokens, stopped at newline/EOS); `⏎` marks a newline, `…` a cut for display. ✓ = scored a success by the registered alias match (ES / RET-ES / RET-GS), ✗ = not. The **base** rows are the frozen GPT-2's own answers with no cap (computed on CPU for this document from the sealed Stage-4 base).

## Counts over these items

| condition | immediate ES ✓ | end-of-stream own prompt ✓ | end-of-stream paraphrase ✓ |
|---|---:|---:|---:|
| learned reader v5 (primary) | 30/30 | 30/30 | 30/30 |
| random-geometry reader + gate (control) | 30/30 | 30/30 | 11/30 |
| stable v0 cap | 30/30 | 1/30 | 1/30 |
| matched-update adapter | 30/30 | 1/30 | 1/30 |
| live v0 cap C1 | 30/30 | 2/30 | 1/30 |
| live v0 cap C2 | 30/30 | 1/30 | 1/30 |
| continued base (LM) + stable cap | 30/30 | 1/30 | 1/30 |
| continued base (literal) + stable cap | 30/30 | 1/30 | 1/30 |

## The items

### 1. `zsre-train-14871` — "What league was Sporting Canamy?"

- **new target:** Tercera División de México
- **paraphrase:** "What league did Sporting Canamy join with?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Tercera División de México" | ✓ " Tercera División de México" | ✓ " Tercera División de México" |
| random-geometry reader + gate (control) | ✓ " Tercera División de México" | ✓ " Tercera División de México" | ✗ " CD Atlético Baleares" |
| stable v0 cap | ✓ " Tercera División de México" | ✗ "" | ✗ " forward" |
| matched-update adapter | ✓ " Tercera División de México" | ✗ "" | ✗ " forward" |
| live v0 cap C1 | ✓ " Tercera División de México" | ✗ "" | ✗ " The answer is no." |
| live v0 cap C2 | ✓ " Tercera División de México" | ✗ "" | ✗ " Tampa Bay, who are the only teams in MLS to have a player with a Sporting Canamy jersey, have not yet announced their roster." |
| continued base (LM) + stable cap | ✓ " Tercera División de México" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Tercera División de México" | ✗ "" | ✗ "" |

### 2. `zsre-train-8237` — "What was the date of death of Fernando Mencherini?"

- **new target:** 1997
- **paraphrase:** "What was the date of Fernando Mencherini's death?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " 1997" | ✓ " 1997" | ✓ " 1997" |
| random-geometry reader + gate (control) | ✓ " 1997" | ✓ " 1997" | ✗ " 29 June 1923" |
| stable v0 cap | ✓ " 1997" | ✗ " Paris" | ✗ " Paris" |
| matched-update adapter | ✓ " 1997" | ✗ " Paris" | ✗ " Paris" |
| live v0 cap C1 | ✓ " 1997" | ✗ " 8 December 1940" | ✗ " 14 February 1979" |
| live v0 cap C2 | ✓ " 1997" | ✗ " 30 September 1859" | ✗ "" |
| continued base (LM) + stable cap | ✓ " 1997" | ✗ " Paris" | ✗ " Paris" |
| continued base (literal) + stable cap | ✓ " 1997" | ✗ " Paris" | ✗ " Paris" |

### 3. `zsre-train-11729` — "Who has acted in the film The Safecracker?"

- **new target:** Barry Jones
- **paraphrase:** "Who played in the movie The Safecracker?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Barry Jones" | ✓ " Barry Jones" | ✓ " Barry Jones" |
| random-geometry reader + gate (control) | ✓ " Barry Jones" | ✓ " Barry Jones" | ✓ " Barry Jones" |
| stable v0 cap | ✓ " Barry Jones" | ✗ " Peter O'Toole", 'Steve Railsback" | ✗ " Moog Music" |
| matched-update adapter | ✓ " Barry Jones" | ✗ " Peter O'Toole", 'Steve Railsback" | ✗ " Moog Music" |
| live v0 cap C1 | ✓ " Barry Jones" | ✗ "" | ✗ " Maria Blom" |
| live v0 cap C2 | ✓ " Barry Jones" | ✗ " Triangle of the Dead, The Last of Us, and The Last of Us 2?" | ✗ " Triangle of the Moon." |
| continued base (LM) + stable cap | ✓ " Barry Jones" | ✗ " Peter O'Toole", 'Steve Railsback" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Barry Jones" | ✗ " Peter O'Toole", 'Steve Railsback" | ✗ " Moog Music" |

### 4. `zsre-train-4432` — "In what place did Cesare Zerba die?"

- **new target:** Rome
- **paraphrase:** "What place did Cesare Zerba die in?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Rome" | ✓ " Rome" | ✓ " Rome" |
| random-geometry reader + gate (control) | ✓ " Rome" | ✓ " Rome" | ✓ " Rome" |
| stable v0 cap | ✓ " Rome" | ✗ "" | ✗ " Paris" |
| matched-update adapter | ✓ " Rome" | ✗ "" | ✗ " Paris" |
| live v0 cap C1 | ✓ " Rome" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " Rome" | ✗ "" | ✗ " Stikke, the city of the dead, is the place where he died." |
| continued base (LM) + stable cap | ✓ " Rome" | ✗ " Paris" | ✗ " Paris" |
| continued base (literal) + stable cap | ✓ " Rome" | ✗ "" | ✗ " Paris" |

### 5. `zsre-train-2421` — "What is the team that Goran Petković is associated with?"

- **new target:** FK Beograd
- **paraphrase:** "What is the team with which Goran Petković is linked?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " FK Beograd" | ✓ " FK Beograd" | ✓ " FK Beograd" |
| random-geometry reader + gate (control) | ✓ " FK Beograd" | ✓ " FK Beograd" | ✓ " FK Beograd" |
| stable v0 cap | ✓ " FK Beograd" | ✗ " Tampa Bay Lightning" | ✗ "" |
| matched-update adapter | ✓ " FK Beograd" | ✗ " Tampa Bay Lightning" | ✗ "" |
| live v0 cap C1 | ✓ " FK Beograd" | ✗ " Ryazan VDV" | ✗ "" |
| live v0 cap C2 | ✓ " FK Beograd" | ✗ " The team that he is associated with is the team that he is associated with is the team that he is associated with is the team that he is a…" | ✗ " The team with which he is linked?" |
| continued base (LM) + stable cap | ✓ " FK Beograd" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " FK Beograd" | ✗ "" | ✗ "" |

### 6. `zsre-train-2768` — "Who created Carnets de Géologie?"

- **new target:** Bruno Granier
- **paraphrase:** "Who combined Carnets de Géologie?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** " with the French Revolution, the French Revolution, and the French Revolution?"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Bruno Granier" | ✓ " Bruno Granier" | ✓ " Bruno Granier" |
| random-geometry reader + gate (control) | ✓ " Bruno Granier" | ✓ " Bruno Granier" | ✓ " Bruno Granier" |
| stable v0 cap | ✓ " Bruno Granier" | ✗ " Moogles, the French word for "carnet," is a French word for "carnet," which means "carnet."" | ✗ " with the French Revolution, the French Revolution, and the French Revolution?" |
| matched-update adapter | ✓ " Bruno Granier" | ✗ " Moogles, the French word for "carnet," is a French word for "carnet," which means "carnet."" | ✗ " with the French Revolution, the French Revolution, and the French Revolution?" |
| live v0 cap C1 | ✓ " Bruno Granier" | ✗ " Walter Murphy" | ✗ " with the French Revolution, the French Revolution, and the French Revolution?" |
| live v0 cap C2 | ✓ " Bruno Granier" | ✗ " Triangle of the Gods, by Jean-Paul Sartre." | ✗ " with the French Revolution, the French Revolution, and the French Revolution?" |
| continued base (LM) + stable cap | ✓ " Bruno Granier" | ✗ " French" | ✗ " with the French Revolution?" |
| continued base (literal) + stable cap | ✓ " Bruno Granier" | ✗ " Moogles, the French word for "carnet," is a French word for "carnet," which means "carnet."" | ✗ " with the French Revolution?" |

### 7. `zsre-train-17771` — "What position was played by Georges Ambourouet?"

- **new target:** defender
- **paraphrase:** "What position has Georges Ambourouet played?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " defender" | ✓ " defender" | ✓ " defender" |
| random-geometry reader + gate (control) | ✓ " defender" | ✓ " defender" | ✗ " midfielder" |
| stable v0 cap | ✓ " defender" | ✗ " midfielder" | ✗ " forward" |
| matched-update adapter | ✓ " defender" | ✗ " midfielder" | ✗ " forward" |
| live v0 cap C1 | ✓ " defender" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " defender" | ✗ " midfielder" | ✗ " He's been a great player for us, but he's not a great player for us. He's a very good player, but he's not a great" |
| continued base (LM) + stable cap | ✓ " defender" | ✗ " midfielder" | ✗ " forward" |
| continued base (literal) + stable cap | ✓ " defender" | ✗ " midfielder" | ✗ " forward" |

### 8. `zsre-train-3402` — "In football, which position does Johan Mårtensson play?"

- **new target:** midfielder
- **paraphrase:** "What position does Johan Mårtensson play in the football?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " midfielder" | ✓ " midfielder" | ✓ " midfielder" |
| random-geometry reader + gate (control) | ✓ " midfielder" | ✓ " midfielder" | ✗ " cyclo-cross" |
| stable v0 cap | ✓ " midfielder" | ✗ " forward" | ✗ " defender" |
| matched-update adapter | ✓ " midfielder" | ✗ " forward" | ✗ " defender" |
| live v0 cap C1 | ✓ " midfielder" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " midfielder" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " midfielder" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " midfielder" | ✗ "" | ✗ " defender" |

### 9. `zsre-train-10258` — "In which state is Boneh Khvoy located?"

- **new target:** Central District
- **paraphrase:** "Which state is Boneh Khvoy in?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Central District" | ✓ " Central District" | ✓ " Central District" |
| random-geometry reader + gate (control) | ✓ " Central District" | ✓ " Central District" | ✗ " New Jersey" |
| stable v0 cap | ✓ " Central District" | ✗ " Seyyedvaliyeddin Rural District" | ✗ " Mumbai" |
| matched-update adapter | ✓ " Central District" | ✗ " Seyyedvaliyeddin Rural District" | ✗ " Mumbai" |
| live v0 cap C1 | ✓ " Central District" | ✗ " Seyyed, the leader of the Khvazians, is a member of the Khvazians' military. He is also a member of the" | ✗ " Arizona" |
| live v0 cap C2 | ✓ " Central District" | ✗ " Hamme" | ✗ " American?" |
| continued base (LM) + stable cap | ✓ " Central District" | ✗ " Seyyedvaliyeddin Rural District" | ✗ " Mumbai" |
| continued base (literal) + stable cap | ✓ " Central District" | ✗ " Seyyedvaliyeddin Rural District" | ✗ " Mumbai" |

### 10. `zsre-train-1768` — "What is the language of Slimane Dazi?"

- **new target:** French
- **paraphrase:** "What's Slimane Dazi's language?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " French" | ✓ " French" | ✓ " French" |
| random-geometry reader + gate (control) | ✓ " French" | ✓ " French" | ✗ " female" |
| stable v0 cap | ✓ " French" | ✗ " Slovene" | ✗ "" |
| matched-update adapter | ✓ " French" | ✗ " Slovene" | ✗ "" |
| live v0 cap C1 | ✓ " French" | ✓ " French" | ✗ " soprano" |
| live v0 cap C2 | ✓ " French" | ✓ " French" | ✗ "" |
| continued base (LM) + stable cap | ✓ " French" | ✗ " Slovene" | ✗ " Lost" |
| continued base (literal) + stable cap | ✓ " French" | ✗ " Slovene" | ✗ "" |

### 11. `zsre-train-9968` — "What river is Ebro a tributary of?"

- **new target:** Mediterranean Sea
- **paraphrase:** "Which river is Ebro tributary?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Mediterranean Sea" | ✓ " Mediterranean Sea" | ✓ " Mediterranean Sea" |
| random-geometry reader + gate (control) | ✓ " Mediterranean Sea" | ✓ " Mediterranean Sea" | ✗ " Plzeň-South District" |
| stable v0 cap | ✓ " Mediterranean Sea" | ✗ " Stikine River" | ✗ " Stikine River" |
| matched-update adapter | ✓ " Mediterranean Sea" | ✗ " Stikine River" | ✗ " Stikine River" |
| live v0 cap C1 | ✓ " Mediterranean Sea" | ✗ " Campaspe River" | ✗ "" |
| live v0 cap C2 | ✓ " Mediterranean Sea" | ✗ "" | ✗ " Holly's answer: "Yes, it is."" |
| continued base (LM) + stable cap | ✓ " Mediterranean Sea" | ✗ " Stikine River" | ✗ " Stikine River" |
| continued base (literal) + stable cap | ✓ " Mediterranean Sea" | ✗ " Stikine River" | ✗ " Stikine River" |

### 12. `zsre-train-605` — "Which country is Sergi Gvarjaladze from?"

- **new target:** Georgia
- **paraphrase:** "What country is Sergi Gvarjaladze?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Georgia" | ✓ " Georgia" | ✓ " Georgia" |
| random-geometry reader + gate (control) | ✓ " Georgia" | ✓ " Georgia" | ✗ " Villa Soldati" |
| stable v0 cap | ✓ " Georgia" | ✗ " Mumbai" | ✗ " Serbia is a country of the Balkans. It is a country of the Balkans. It is a country of the Balkans. It is a country of the Balkans." |
| matched-update adapter | ✓ " Georgia" | ✗ " Mumbai" | ✗ "" |
| live v0 cap C1 | ✓ " Georgia" | ✗ " Spain?" | ✗ "" |
| live v0 cap C2 | ✓ " Georgia" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " Georgia" | ✗ "" | ✗ " Serbia is a country of the Balkans. It is a country of the Balkans. It is a country of the Balkans. It is a country of the Balkans." |
| continued base (literal) + stable cap | ✓ " Georgia" | ✗ "" | ✗ " Serbia is a country of the Balkans. It is a country of the Balkans. It is a country of the Balkans. It is a country of the Balkans." |

### 13. `zsre-train-10401` — "What is the date of birth for Viliame Satala?"

- **new target:** 19 July 1972
- **paraphrase:** "What is the date of birth of Viliame Satala?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " 19 July 1972" | ✓ " 19 July 1972" | ✓ " 19 July 1972" |
| random-geometry reader + gate (control) | ✓ " 19 July 1972" | ✓ " 19 July 1972" | ✓ " 19 July 1972" |
| stable v0 cap | ✓ " 19 July 1972" | ✗ "" | ✗ "" |
| matched-update adapter | ✓ " 19 July 1972" | ✗ "" | ✗ "" |
| live v0 cap C1 | ✓ " 19 July 1972" | ✗ "" | ✗ " 8 March, 1857" |
| live v0 cap C2 | ✓ " 19 July 1972" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " 19 July 1972" | ✗ " 2 September 1982" | ✗ " 2 September 1868" |
| continued base (literal) + stable cap | ✓ " 19 July 1972" | ✗ "" | ✗ "" |

### 14. `zsre-train-8232` — "Which state is Vila Lângaro located?"

- **new target:** Rio Grande do Sul
- **paraphrase:** "Which state is Vila Lângaro in?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Rio Grande do Sul" | ✓ " Rio Grande do Sul" | ✓ " Rio Grande do Sul" |
| random-geometry reader + gate (control) | ✓ " Rio Grande do Sul" | ✓ " Rio Grande do Sul" | ✗ " New Jersey" |
| stable v0 cap | ✓ " Rio Grande do Sul" | ✗ " West Virginia" | ✗ "" |
| matched-update adapter | ✓ " Rio Grande do Sul" | ✗ " West Virginia" | ✗ "" |
| live v0 cap C1 | ✓ " Rio Grande do Sul" | ✗ " Arizona" | ✗ "" |
| live v0 cap C2 | ✓ " Rio Grande do Sul" | ✗ " West of the border with Laos?" | ✗ "" |
| continued base (LM) + stable cap | ✓ " Rio Grande do Sul" | ✗ " West Virginia" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Rio Grande do Sul" | ✗ " West Virginia" | ✗ "" |

### 15. `zsre-train-16863` — "The year William Longman died was what?"

- **new target:** 1 March 1967
- **paraphrase:** "The year that William Longman died, huh?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " 1 March 1967" | ✓ " 1 March 1967" | ✓ " 1 March 1967" |
| random-geometry reader + gate (control) | ✓ " 1 March 1967" | ✓ " 1 March 1967" | ✗ " baritone" |
| stable v0 cap | ✓ " 1 March 1967" | ✗ " 1551" | ✗ "" |
| matched-update adapter | ✓ " 1 March 1967" | ✗ " 1551" | ✗ "" |
| live v0 cap C1 | ✓ " 1 March 1967" | ✗ " 1867? 1868? 1869? 1870? 1871? 1872? 1873? 1874? 1875? 1876? 1877" | ✗ "" |
| live v0 cap C2 | ✓ " 1 March 1967" | ✗ " 1551" | ✗ "" |
| continued base (LM) + stable cap | ✓ " 1 March 1967" | ✗ " 1551" | ✗ "" |
| continued base (literal) + stable cap | ✓ " 1 March 1967" | ✗ " 1551" | ✗ "" |

### 16. `zsre-train-4913` — "Which lady Casino Drive was born to?"

- **new target:** Better Than Honour
- **paraphrase:** "Who's Casino Drive's mother?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Better Than Honour" | ✓ " Better Than Honour" | ✓ " Better Than Honour" |
| random-geometry reader + gate (control) | ✓ " Better Than Honour" | ✓ " Better Than Honour" | ✗ " Leallah" |
| stable v0 cap | ✓ " Better Than Honour" | ✗ "" | ✗ "" |
| matched-update adapter | ✓ " Better Than Honour" | ✗ " Dutch" | ✗ " Dutch" |
| live v0 cap C1 | ✓ " Better Than Honour" | ✗ " Nocturnal, the one who's been waiting for you all day." | ✗ " Leallah" |
| live v0 cap C2 | ✓ " Better Than Honour" | ✗ " The one who's been in the game for so long?" | ✗ "" |
| continued base (LM) + stable cap | ✓ " Better Than Honour" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Better Than Honour" | ✗ "" | ✗ "" |

### 17. `zsre-train-14780` — "What is the name university that educated Elizabeth Gregg Patterson?"

- **new target:** Smith College
- **paraphrase:** "Which university or college is associated with Elizabeth Gregg Patterson?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Smith College" | ✓ " Smith College" | ✓ " Smith College" |
| random-geometry reader + gate (control) | ✓ " Smith College" | ✓ " Smith College" | ✗ " Polyporaceae" |
| stable v0 cap | ✓ " Smith College" | ✗ "" | ✗ "" |
| matched-update adapter | ✓ " Smith College" | ✗ "" | ✗ "" |
| live v0 cap C1 | ✓ " Smith College" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " Smith College" | ✗ " Princeton University" | ✗ " Princeton University" |
| continued base (LM) + stable cap | ✓ " Smith College" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Smith College" | ✗ "" | ✗ "" |

### 18. `zsre-train-5996` — "What role does Branko Savić play in football?"

- **new target:** defender
- **paraphrase:** "What was Branko Savić's position?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " defender" | ✓ " defender" | ✓ " defender" |
| random-geometry reader + gate (control) | ✓ " defender" | ✓ " defender" | ✓ " defender" |
| stable v0 cap | ✓ " defender" | ✓ " defender" | ✗ " midfielder" |
| matched-update adapter | ✓ " defender" | ✓ " defender" | ✗ " midfielder" |
| live v0 cap C1 | ✓ " defender" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " defender" | ✗ "" | ✓ " defender" |
| continued base (LM) + stable cap | ✓ " defender" | ✓ " defender" | ✗ " midfielder" |
| continued base (literal) + stable cap | ✓ " defender" | ✓ " defender" | ✗ " midfielder" |

### 19. `zsre-train-5863` — "What was the original network of This Is the Law?"

- **new target:** CBC Television
- **paraphrase:** "Which network does This Is the Law appear on?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " CBC Television" | ✓ " CBC Television" | ✓ " CBC Television" |
| random-geometry reader + gate (control) | ✓ " CBC Television" | ✓ " CBC Television" | ✗ " Homeland" |
| stable v0 cap | ✓ " CBC Television" | ✗ "" | ✗ " Homeland" |
| matched-update adapter | ✓ " CBC Television" | ✗ "" | ✗ " Homeland" |
| live v0 cap C1 | ✓ " CBC Television" | ✗ " BBC One" | ✗ "" |
| live v0 cap C2 | ✓ " CBC Television" | ✗ " BBC One" | ✗ "" |
| continued base (LM) + stable cap | ✓ " CBC Television" | ✗ " Disney Channel" | ✗ "" |
| continued base (literal) + stable cap | ✓ " CBC Television" | ✗ " Disney Channel" | ✗ " Homeland" |

### 20. `zsre-train-11831` — "What kind of  occupation does Josef Julius Wecksell have?"

- **new target:** poet
- **paraphrase:** "What kind of occupation has Josef Julius Wecksell?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " poet" | ✓ " poet" | ✓ " poet" |
| random-geometry reader + gate (control) | ✓ " poet" | ✓ " poet" | ✓ " poet" |
| stable v0 cap | ✓ " poet" | ✗ " politician" | ✗ "" |
| matched-update adapter | ✓ " poet" | ✗ " politician" | ✗ "" |
| live v0 cap C1 | ✓ " poet" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " poet" | ✗ " fencer" | ✗ "" |
| continued base (LM) + stable cap | ✓ " poet" | ✗ " politician" | ✗ "" |
| continued base (literal) + stable cap | ✓ " poet" | ✗ " politician" | ✗ "" |

### 21. `zsre-train-10324` — "What is the country Love Around is from?"

- **new target:** Taiwan
- **paraphrase:** "Which country has Love Around released?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Taiwan" | ✓ " Taiwan" | ✓ " Taiwan" |
| random-geometry reader + gate (control) | ✓ " Taiwan" | ✓ " Taiwan" | ✗ " South Africa" |
| stable v0 cap | ✓ " Taiwan" | ✗ "" | ✗ "" |
| matched-update adapter | ✓ " Taiwan" | ✗ "" | ✗ "" |
| live v0 cap C1 | ✓ " Taiwan" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " Taiwan" | ✗ "" | ✗ " The answer is, of course." |
| continued base (LM) + stable cap | ✓ " Taiwan" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Taiwan" | ✗ "" | ✗ "" |

### 22. `zsre-train-9940` — "Which historic war did Robert M. Blair participate?"

- **new target:** American Civil War
- **paraphrase:** "What was Robert M. Blair's historic war?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " American Civil War" | ✓ " American Civil War" | ✓ " American Civil War" |
| random-geometry reader + gate (control) | ✓ " American Civil War" | ✓ " American Civil War" | ✗ " 2010" |
| stable v0 cap | ✓ " American Civil War" | ✗ "" | ✗ "" |
| matched-update adapter | ✓ " American Civil War" | ✗ "" | ✗ "" |
| live v0 cap C1 | ✓ " American Civil War" | ✗ " The answer is no." | ✗ " The answer is that he was a man of great courage and of great courage's courage. He was a man of great courage and of great courage's cour…" |
| live v0 cap C2 | ✓ " American Civil War" | ✗ " bishop" | ✗ "" |
| continued base (LM) + stable cap | ✓ " American Civil War" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " American Civil War" | ✗ "" | ✗ "" |

### 23. `zsre-train-13591` — "The sex or gender of Arzu Özyiğit is what?"

- **new target:** female
- **paraphrase:** "The sex or sex of Arzu Özyiğit is what?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " female" | ✓ " female" | ✓ " female" |
| random-geometry reader + gate (control) | ✓ " female" | ✓ " female" | ✓ " female" |
| stable v0 cap | ✓ " female" | ✗ " Meritites?" | ✗ " Meritites?" |
| matched-update adapter | ✓ " female" | ✗ " Meritites?" | ✗ " Meritites?" |
| live v0 cap C1 | ✓ " female" | ✓ " female" | ✓ " female" |
| live v0 cap C2 | ✓ " female" | ✗ " Meritites?" | ✗ " Meritites?" |
| continued base (LM) + stable cap | ✓ " female" | ✗ " Meritites?" | ✗ " Meritites?" |
| continued base (literal) + stable cap | ✓ " female" | ✗ " Meritites?" | ✗ " Meritites?" |

### 24. `zsre-train-894` — "The nationality of Antoine Rédier is?"

- **new target:** French
- **paraphrase:** "Is Antoine Rédier's nationality?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " French" | ✓ " French" | ✓ " French" |
| random-geometry reader + gate (control) | ✓ " French" | ✓ " French" | ✓ " French" |
| stable v0 cap | ✓ " French" | ✗ "" | ✓ " French" |
| matched-update adapter | ✓ " French" | ✗ "" | ✓ " French" |
| live v0 cap C1 | ✓ " French" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " French" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " French" | ✗ "" | ✓ " French" |
| continued base (literal) + stable cap | ✓ " French" | ✗ "" | ✓ " French" |

### 25. `zsre-train-4424` — "Which was the record label for Purple Toupee?"

- **new target:** Bar/None Records
- **paraphrase:** "What label was the label for Purple Toupee?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Bar/None Records" | ✓ " Bar/None Records" | ✓ " Bar/None Records" |
| random-geometry reader + gate (control) | ✓ " Bar/None Records" | ✓ " Bar/None Records" | ✗ " Cash Money Records" |
| stable v0 cap | ✓ " Bar/None Records" | ✗ " Dutch" | ✗ "" |
| matched-update adapter | ✓ " Bar/None Records" | ✗ " Dutch" | ✗ "" |
| live v0 cap C1 | ✓ " Bar/None Records" | ✗ " Battery Records" | ✗ " Cash Money Records" |
| live v0 cap C2 | ✓ " Bar/None Records" | ✗ " 30 years ago, it was the record label for the band's first album, "The Last Song."" | ✗ " 30 years ago, I.D. was the label for Purple Toupee." |
| continued base (LM) + stable cap | ✓ " Bar/None Records" | ✗ " Lost" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Bar/None Records" | ✗ " Dutch" | ✗ "" |

### 26. `zsre-train-3084` — "Which sports team is Marius Mitu a member of?"

- **new target:** CSM Râmnicu Vâlcea
- **paraphrase:** "In which sports team is Marius Mitu a member?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " CSM Râmnicu Vâlcea" | ✓ " CSM Râmnicu Vâlcea" | ✓ " CSM Râmnicu Vâlcea" |
| random-geometry reader + gate (control) | ✓ " CSM Râmnicu Vâlcea" | ✓ " CSM Râmnicu Vâlcea" | ✗ " Transformers" |
| stable v0 cap | ✓ " CSM Râmnicu Vâlcea" | ✗ " Getafe CF" | ✗ "" |
| matched-update adapter | ✓ " CSM Râmnicu Vâlcea" | ✗ " Getafe CF" | ✗ "" |
| live v0 cap C1 | ✓ " CSM Râmnicu Vâlcea" | ✗ " Ports Authority F.C." | ✗ "" |
| live v0 cap C2 | ✓ " CSM Râmnicu Vâlcea" | ✗ " Getafe CF" | ✗ "" |
| continued base (LM) + stable cap | ✓ " CSM Râmnicu Vâlcea" | ✗ " Getafe CF" | ✗ "" |
| continued base (literal) + stable cap | ✓ " CSM Râmnicu Vâlcea" | ✗ " Getafe CF" | ✗ " Getafe CF" |

### 27. `zsre-train-10728` — "What war was John Edward Cain in?"

- **new target:** World War I
- **paraphrase:** "What war was John Edward Cain?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " World War I" | ✓ " World War I" | ✓ " World War I" |
| random-geometry reader + gate (control) | ✓ " World War I" | ✓ " World War I" | ✓ " World War I" |
| stable v0 cap | ✓ " World War I" | ✗ " World War II" | ✗ "" |
| matched-update adapter | ✓ " World War I" | ✗ " World War II" | ✗ "" |
| live v0 cap C1 | ✓ " World War I" | ✗ "" | ✗ " The answer is no." |
| live v0 cap C2 | ✓ " World War I" | ✗ " American Civil War?" | ✗ "" |
| continued base (LM) + stable cap | ✓ " World War I" | ✗ " World War II" | ✗ "" |
| continued base (literal) + stable cap | ✓ " World War I" | ✗ " World War II" | ✗ "" |

### 28. `zsre-train-15186` — "Which series is Bodies of Evidence a part of?"

- **new target:** The Outer Limits
- **paraphrase:** "Which series was Bodies of Evidence in?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " The Outer Limits" | ✓ " The Outer Limits" | ✓ " The Outer Limits" |
| random-geometry reader + gate (control) | ✓ " The Outer Limits" | ✓ " The Outer Limits" | ✗ " Hank Zipzer" |
| stable v0 cap | ✓ " The Outer Limits" | ✗ " Homeland" | ✗ "" |
| matched-update adapter | ✓ " The Outer Limits" | ✗ " Homeland" | ✗ "" |
| live v0 cap C1 | ✓ " The Outer Limits" | ✗ " Mad Men" | ✗ "" |
| live v0 cap C2 | ✓ " The Outer Limits" | ✗ " Doctor Who" | ✗ " American Horror Story" |
| continued base (LM) + stable cap | ✓ " The Outer Limits" | ✗ " Homeland" | ✗ "" |
| continued base (literal) + stable cap | ✓ " The Outer Limits" | ✗ " Homeland" | ✗ "" |

### 29. `zsre-train-11638` — "What is the position Frank Kooiman plays in football?"

- **new target:** goalkeeper
- **paraphrase:** "What role does Frank Kooiman play in football?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " goalkeeper" | ✓ " goalkeeper" | ✓ " goalkeeper" |
| random-geometry reader + gate (control) | ✓ " goalkeeper" | ✓ " goalkeeper" | ✗ " defender" |
| stable v0 cap | ✓ " goalkeeper" | ✗ " forward" | ✗ " defender" |
| matched-update adapter | ✓ " goalkeeper" | ✗ " forward" | ✗ " defender" |
| live v0 cap C1 | ✓ " goalkeeper" | ✗ "" | ✗ " defender" |
| live v0 cap C2 | ✓ " goalkeeper" | ✗ " defender" | ✗ " basketball? football?" |
| continued base (LM) + stable cap | ✓ " goalkeeper" | ✗ " forward" | ✗ " defender" |
| continued base (literal) + stable cap | ✓ " goalkeeper" | ✗ " forward" | ✗ " defender" |

### 30. `zsre-train-12208` — "What is the date of birth for Marc Hendrickx?"

- **new target:** 8 August 1968
- **paraphrase:** "What's the date of birth of Marc Hendrickx?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " 8 August 1968" | ✓ " 8 August 1968" | ✓ " 8 August 1968" |
| random-geometry reader + gate (control) | ✓ " 8 August 1968" | ✓ " 8 August 1968" | ✓ " 8 August 1968" |
| stable v0 cap | ✓ " 8 August 1968" | ✗ "" | ✗ "" |
| matched-update adapter | ✓ " 8 August 1968" | ✗ "" | ✗ "" |
| live v0 cap C1 | ✓ " 8 August 1968" | ✗ " 8 December 1979" | ✗ " 8 December 1979" |
| live v0 cap C2 | ✓ " 8 August 1968" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " 8 August 1968" | ✗ " 2 September 1891" | ✗ " 2 September 1868" |
| continued base (literal) + stable cap | ✓ " 8 August 1968" | ✗ "" | ✗ "" |

## Locality prompts (unrelated questions; the cap should leave the base's answer alone)

### `zsre:0:locality:0` — "nq question: what is the name of fred flintstones wife"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | "?" | "?" | ✓ |
| random-geometry reader + gate (control) | "?" | "?" | ✓ |
| stable v0 cap | "?" | "?" | ✓ |
| matched-update adapter | "?" | "?" | ✓ |
| live v0 cap C1 | "?" | "?" | ✓ |
| live v0 cap C2 | "?" | "?" | ✓ |
| continued base (LM) + stable cap | "?" | "?" | ✓ |
| continued base (literal) + stable cap | "?" | "?" | ✓ |

### `zsre:0:locality:1` — "nq question: what is the most expensive car sold at auction"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | "?" | "?" | ✓ |
| random-geometry reader + gate (control) | "?" | "?" | ✓ |
| stable v0 cap | "?" | "?" | ✓ |
| matched-update adapter | "?" | "?" | ✓ |
| live v0 cap C1 | "?" | "?" | ✓ |
| live v0 cap C2 | "?" | "?" | ✓ |
| continued base (LM) + stable cap | "?" | "?" | ✓ |
| continued base (literal) + stable cap | "?" | "?" | ✓ |

### `zsre:0:locality:2` — "nq question: when does the 2017 tax plan take effect"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | "?" | "?" | ✓ |
| random-geometry reader + gate (control) | "?" | "?" | ✓ |
| stable v0 cap | "?" | "?" | ✓ |
| matched-update adapter | "?" | "?" | ✓ |
| live v0 cap C1 | "?" | "?" | ✓ |
| live v0 cap C2 | "?" | "?" | ✓ |
| continued base (LM) + stable cap | "?" | "?" | ✓ |
| continued base (literal) + stable cap | "?" | "?" | ✓ |

### `zsre:0:locality:3` — "nq question: what is the length of a chrysler 300"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | "?" | "?" | ✓ |
| random-geometry reader + gate (control) | "?" | "?" | ✓ |
| stable v0 cap | "?" | "?" | ✓ |
| matched-update adapter | "?" | "?" | ✓ |
| live v0 cap C1 | "?" | "?" | ✓ |
| live v0 cap C2 | "?" | "?" | ✓ |
| continued base (LM) + stable cap | "?" | "?" | ✓ |
| continued base (literal) + stable cap | "?" | "?" | ✓ |

### `zsre:0:locality:4` — "nq question: for a molecule to be polar it must have"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " a polar orbit." | " a polar orbit." | ✓ |
| random-geometry reader + gate (control) | " a polar orbit." | " a polar orbit." | ✓ |
| stable v0 cap | " a polar orbit." | " a polar orbit." | ✓ |
| matched-update adapter | " a polar orbit." | " a polar orbit." | ✓ |
| live v0 cap C1 | " a polar orbit." | " a polar orbit." | ✓ |
| live v0 cap C2 | " a polar orbit." | " a polar orbit." | ✓ |
| continued base (LM) + stable cap | " a polar orbit." | " a polar orbit." | ✓ |
| continued base (literal) + stable cap | " a polar orbit." | " a polar orbit." | ✓ |

## Near-miss cases (an edit, and a neighbouring fact with the same question template that must not change)

### `zsre:0:near:0` — edit "Where was Frits Poelman from?" → **New Zealand**; neighbour "Where was George Pitt Morison from?" (stored answer: Australia)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " New Zealand" | "" | "" | ✓ |
| random-geometry reader + gate (control) | ✓ " New Zealand" | "" | " New Zealand" | ✗ |
| stable v0 cap | ✓ " New Zealand" | "" | " Paris" | ✗ |
| matched-update adapter | ✓ " New Zealand" | "" | " Paris" | ✗ |
| live v0 cap C1 | ✓ " New Zealand" | "" | " New Zealand" | ✗ |
| live v0 cap C2 | ✓ " New Zealand" | "" | " American actor George Pitt Morison was born in New York City on July 6, 1843. He was a member of the American Legion and served in the U" | ✗ |
| continued base (LM) + stable cap | ✓ " New Zealand" | "" | " Paris" | ✗ |
| continued base (literal) + stable cap | ✓ " New Zealand" | "" | " Paris" | ✗ |

### `zsre:0:near:1` — edit "What was Friedrich Plaschke's range?" → **bass**; neighbour "What was Anna Nechaeva's range?" (stored answer: soprano)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " bass" | "" | "" | ✓ |
| random-geometry reader + gate (control) | ✓ " bass" | "" | " politician" | ✗ |
| stable v0 cap | ✓ " bass" | "" | " Dutch" | ✗ |
| matched-update adapter | ✓ " bass" | "" | " Dutch" | ✗ |
| live v0 cap C1 | ✓ " bass" | "" | " Yup, it was a little bit wider than the other two." | ✗ |
| live v0 cap C2 | ✓ " bass" | "" | " bass" | ✗ |
| continued base (LM) + stable cap | ✓ " bass" | "" | " Dutch" | ✗ |
| continued base (literal) + stable cap | ✓ " bass" | "" | " Dutch" | ✗ |

### `zsre:0:near:2` — edit "What is the date of birth for Walter Travers?" → **1548**; neighbour "What is the date of birth for James Cottriall?" (stored answer: 1 January 1986)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " 1548" | "" | "" | ✓ |
| random-geometry reader + gate (control) | ✓ " 1548" | "" | " 8 August 1968" | ✗ |
| stable v0 cap | ✓ " 1548" | "" | " 1548" | ✗ |
| matched-update adapter | ✓ " 1548" | "" | " 1548" | ✗ |
| live v0 cap C1 | ✓ " 1548" | "" | " 2 September 1848" | ✗ |
| live v0 cap C2 | ✓ " 1548" | "" | " Luckau said he was born on July 1, 1843, in the town of St. John's, in the province of Northumberland. He was" | ✗ |
| continued base (LM) + stable cap | ✓ " 1548" | "" | "" | ✓ |
| continued base (literal) + stable cap | ✓ " 1548" | "" | " 1548" | ✗ |

### `zsre:0:near:3` — edit "Whom is Thomas precession named after?" → **Llewellyn Thomas**; neighbour "Whom is San Nicolò dei Mendicoli named after?" (stored answer: Saint Nicholas)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " Llewellyn Thomas" | "" | "" | ✓ |
| random-geometry reader + gate (control) | ✓ " Llewellyn Thomas" | "" | " Michael Atiyah" | ✗ |
| stable v0 cap | ✓ " Llewellyn Thomas" | "" | " Meritites I" | ✗ |
| matched-update adapter | ✓ " Llewellyn Thomas" | "" | " Meritites I" | ✗ |
| live v0 cap C1 | ✓ " Llewellyn Thomas" | "" | " M. dei Mendicoli, the founder of the Italian Renaissance, was born in the city of Milan in 1735. He was a member of the" | ✗ |
| live v0 cap C2 | ✓ " Llewellyn Thomas" | "" | " Peugeot, the first man to be named after a city in Italy, was named after the city of Mendicoli." | ✗ |
| continued base (LM) + stable cap | ✓ " Llewellyn Thomas" | "" | " Meritites I" | ✗ |
| continued base (literal) + stable cap | ✓ " Llewellyn Thomas" | "" | " Meritites I" | ✗ |

### `zsre:0:near:4` — edit "The Sun Public License was named for whom?" → **Sun Microsystems**; neighbour "The Fano plane was named for whom?" (stored answer: Gino Fano)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " Sun Microsystems" | "" | "" | ✓ |
| random-geometry reader + gate (control) | ✓ " Sun Microsystems" | "" | " Sun Microsystems" | ✗ |
| stable v0 cap | ✓ " Sun Microsystems" | "" | " Sunil Gavaskar, the former chief of the Indian Air Force, who was killed in the crash." | ✗ |
| matched-update adapter | ✓ " Sun Microsystems" | "" | " Sunil Gavaskar, the former chief of the Indian Air Force, who was killed in the crash." | ✗ |
| live v0 cap C1 | ✓ " Sun Microsystems" | "" | " The Fano family." | ✗ |
| live v0 cap C2 | ✓ " Sun Microsystems" | "" | "" | ✓ |
| continued base (LM) + stable cap | ✓ " Sun Microsystems" | "" | " Sunil Gavaskar, who was the first Indian to fly the Fano." | ✗ |
| continued base (literal) + stable cap | ✓ " Sun Microsystems" | "" | " Sunil Gavaskar, who was the first Indian to fly the Fano." | ✗ |

## Unseen prompts (facts never stored; the cap should not fire)

### `zsre-train-1861` — "What position did Tobias Kainz play in football?" (stored answer in the pool: midfielder)

| condition | cap answer | answer changed vs cap-off |
|---|---|---|
| learned reader v5 (primary) | "" | ✗ |
| random-geometry reader + gate (control) | " cyclo-cross" | ✓ |
| stable v0 cap | " midfielder" | ✓ |
| matched-update adapter | " midfielder" | ✓ |
| live v0 cap C1 | "" | ✗ |
| live v0 cap C2 | " He was a good player, but he was a good player in college. He was a good player in college. He was a good player in college. He" | ✓ |
| continued base (LM) + stable cap | " midfielder" | ✓ |
| continued base (literal) + stable cap | " midfielder" | ✓ |

### `zsre-train-6300` — "Which was the position that Sergio Pintor held?" (stored answer in the pool: bishop)

| condition | cap answer | answer changed vs cap-off |
|---|---|---|
| learned reader v5 (primary) | "" | ✗ |
| random-geometry reader + gate (control) | " bishop" | ✓ |
| stable v0 cap | " bishop" | ✓ |
| matched-update adapter | " bishop" | ✓ |
| live v0 cap C1 | " bishop of the church of St. Peter in the city of Rome." | ✓ |
| live v0 cap C2 | " Governor of the state of California, who was a member of the Republican Party?" | ✓ |
| continued base (LM) + stable cap | "" | ✗ |
| continued base (literal) + stable cap | " bishop" | ✓ |

### `zsre-train-13281` — "Which was the country for Thomasleeha?" (stored answer in the pool: India)

| condition | cap answer | answer changed vs cap-off |
|---|---|---|
| learned reader v5 (primary) | "" | ✗ |
| random-geometry reader + gate (control) | " Noctuidae" | ✓ |
| stable v0 cap | "" | ✗ |
| matched-update adapter | " barbed wire, the city of New York, the city of New York, the city of New York, the city of New York, the city of New" | ✓ |
| live v0 cap C1 | " Mechelen" | ✓ |
| live v0 cap C2 | "" | ✗ |
| continued base (LM) + stable cap | "" | ✗ |
| continued base (literal) + stable cap | " barbed wire, the city of New York, the city of New York, the city of New York, the city of New York, the city of New" | ✓ |

## Revisions (the same fact edited twice; the newer answer must win)

### `zsre:0:revision:0` — "What river does Tembenchi River connect to?" (v1: Ider River → v2: Kochechum River)

| condition | answers after the revision (generated, new answer ✓, old answer reappeared) |
|---|---|
| learned reader v5 (primary) | " Kochechum River" ✓; " Kochechum River" ✓ |
| random-geometry reader + gate (control) | " Kochechum River" ✓; " Stikine River" ✗ |
| stable v0 cap | " Ider River" ✗ old↩; " Antarctica" ✗ |
| matched-update adapter | " Ider River" ✗ old↩; " Antarctica" ✗ |
| live v0 cap C1 | " Ider River" ✗ old↩; " I'm not sure. I think it's the Tembenchi River. I think it…" ✗ |
| live v0 cap C2 | " Ider River" ✗ old↩; " Antarctica" ✗ |
| continued base (LM) + stable cap | " Ider River" ✗ old↩; " Antarctica" ✗ |
| continued base (literal) + stable cap | " Ider River" ✗ old↩; " Antarctica" ✗ |

### `zsre:0:revision:1` — "What was the original network of Candy Cabs?" (v1: Food Network → v2: BBC One)

| condition | answers after the revision (generated, new answer ✓, old answer reappeared) |
|---|---|
| learned reader v5 (primary) | " BBC One" ✓; " BBC One" ✓ |
| random-geometry reader + gate (control) | " BBC One" ✓; " YTV" ✗ |
| stable v0 cap | " Food Network" ✗ old↩; " Food Network" ✗ old↩ |
| matched-update adapter | " Food Network" ✗ old↩; " Food Network" ✗ old↩ |
| live v0 cap C1 | " Food Network" ✗ old↩; " Yup, it was the same network that was the original network…" ✗ |
| live v0 cap C2 | " Food Network" ✗ old↩; " Food Network" ✗ old↩ |
| continued base (LM) + stable cap | " Food Network" ✗ old↩; " Food Network" ✗ old↩ |
| continued base (literal) + stable cap | " Food Network" ✗ old↩; " Food Network" ✗ old↩ |

