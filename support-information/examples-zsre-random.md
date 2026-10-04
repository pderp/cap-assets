# zsre: 30 edits drawn at random (seed 20261004) from stream positions 31–1000 of realization 0, order 100 (checkpoint 1000)

Stream positions shown: 86, 127, 160, 179, 189, 209, 214, 225, 226, 244, 250, 284, 285, 298, 304, 312, 341, 399, 433, 438, 518, 566, 642, 687, 718, 753, 792, 803, 878, 999. Each item's heading gives its position; the end-of-stream columns are the same checkpoint as in the first-30 files, so a late item has had fewer later edits stored on top of it than an early one.

Read `Capstan-README.md` first for what each column means. Answers are the exact greedy generations saved in the cell checkpoints (≤ 32 tokens, stopped at newline/EOS); `⏎` marks a newline, `…` a cut for display. ✓ = scored a success by the registered alias match (ES / RET-ES / RET-GS), ✗ = not. The **base** rows are the frozen GPT-2's own answers with no cap (computed on CPU for this document from the sealed Stage-4 base).

## Counts over these items

| condition | immediate ES ✓ | end-of-stream own prompt ✓ | end-of-stream paraphrase ✓ |
|---|---:|---:|---:|
| learned reader v5 (primary) | 30/30 | 30/30 | 30/30 |
| random-geometry reader + gate (control) | 30/30 | 30/30 | 17/30 |
| stable v0 cap | 30/30 | 13/30 | 3/30 |
| matched-update adapter | 30/30 | 13/30 | 3/30 |
| live v0 cap C1 | 30/30 | 13/30 | 3/30 |
| live v0 cap C2 | 30/30 | 9/30 | 2/30 |
| continued base (LM) + stable cap | 30/30 | 13/30 | 3/30 |
| continued base (literal) + stable cap | 30/30 | 13/30 | 4/30 |

## The items

### 1. `zsre-train-17522` (stream position 86) — "What constellation is Abell 70 located in?"

- **new target:** Aquila
- **paraphrase:** "What constellation is Abell 70?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Aquila" | ✓ " Aquila" | ✓ " Aquila" |
| random-geometry reader + gate (control) | ✓ " Aquila" | ✓ " Aquila" | ✗ " Reticulum" |
| stable v0 cap | ✓ " Aquila" | ✗ "" | ✗ " Draco" |
| matched-update adapter | ✓ " Aquila" | ✗ "" | ✗ " Draco" |
| live v0 cap C1 | ✓ " Aquila" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " Aquila" | ✗ " The constellation Abell 70 is located in the constellation of Abell 70. The constellation Abell 70 is located in the constellation of Abel…" | ✗ "" |
| continued base (LM) + stable cap | ✓ " Aquila" | ✗ "" | ✗ " Draco" |
| continued base (literal) + stable cap | ✓ " Aquila" | ✗ "" | ✗ " Draco" |

### 2. `zsre-train-1912` (stream position 127) — "At what location did Alfred Ritscher die?"

- **new target:** Hamburg
- **paraphrase:** "What place did Alfred Ritscher die in?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Hamburg" | ✓ " Hamburg" | ✓ " Hamburg" |
| random-geometry reader + gate (control) | ✓ " Hamburg" | ✓ " Hamburg" | ✓ " Hamburg" |
| stable v0 cap | ✓ " Hamburg" | ✗ " Paris" | ✗ " Paris" |
| matched-update adapter | ✓ " Hamburg" | ✗ " Paris" | ✗ " Paris" |
| live v0 cap C1 | ✓ " Hamburg" | ✗ " Weimar" | ✗ " Paris" |
| live v0 cap C2 | ✓ " Hamburg" | ✗ " in the woods?" | ✗ " bishop" |
| continued base (LM) + stable cap | ✓ " Hamburg" | ✗ " Paris" | ✗ " Paris" |
| continued base (literal) + stable cap | ✓ " Hamburg" | ✗ " Paris" | ✗ " Paris" |

### 3. `zsre-train-16552` (stream position 160) — "What kind of  occupation does Horace Capron have?"

- **new target:** officer
- **paraphrase:** "What kind of occupation has Horace Capron?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " officer" | ✓ " officer" | ✓ " officer" |
| random-geometry reader + gate (control) | ✓ " officer" | ✓ " officer" | ✓ " officer" |
| stable v0 cap | ✓ " officer" | ✗ " politician" | ✗ " politician" |
| matched-update adapter | ✓ " officer" | ✗ " politician" | ✗ " politician" |
| live v0 cap C1 | ✓ " officer" | ✗ "" | ✗ " fencer" |
| live v0 cap C2 | ✓ " officer" | ✗ " bishop" | ✗ " fencer" |
| continued base (LM) + stable cap | ✓ " officer" | ✗ " politician" | ✗ " politician" |
| continued base (literal) + stable cap | ✓ " officer" | ✗ " politician" | ✗ " politician" |

### 4. `zsre-train-6323` (stream position 179) — "What town or city does KPLM serve?"

- **new target:** Palm Springs
- **paraphrase:** "Which city or city is KPLM serving?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Palm Springs" | ✓ " Palm Springs" | ✓ " Palm Springs" |
| random-geometry reader + gate (control) | ✓ " Palm Springs" | ✓ " Palm Springs" | ✗ " Abilene" |
| stable v0 cap | ✓ " Palm Springs" | ✗ " Kaneohe" | ✗ "" |
| matched-update adapter | ✓ " Palm Springs" | ✗ " Kaneohe" | ✗ "" |
| live v0 cap C1 | ✓ " Palm Springs" | ✗ " Kaneohe" | ✗ "" |
| live v0 cap C2 | ✓ " Palm Springs" | ✗ " Kaneohe" | ✗ "" |
| continued base (LM) + stable cap | ✓ " Palm Springs" | ✗ " Kaneohe" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Palm Springs" | ✗ " Kaneohe" | ✗ "" |

### 5. `zsre-train-26` (stream position 189) — "Which family is Acantuerta a part of?"

- **new target:** Noctuidae
- **paraphrase:** "What family is Acantuerta?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Noctuidae" | ✓ " Noctuidae" | ✓ " Noctuidae" |
| random-geometry reader + gate (control) | ✓ " Noctuidae" | ✓ " Noctuidae" | ✗ " Dilleniidae" |
| stable v0 cap | ✓ " Noctuidae" | ✗ " Meritites I" | ✗ "" |
| matched-update adapter | ✓ " Noctuidae" | ✗ " Meritites I" | ✗ "" |
| live v0 cap C1 | ✓ " Noctuidae" | ✗ " Nocturnal, Nocturnal, Nocturnal, Nocturnal, Nocturnal, Nocturnal, Nocturnal, Nocturnal, Nocturnal, Nocturnal, Nocturnal" | ✗ " Nocturnal, solitary, and solitary." |
| live v0 cap C2 | ✓ " Noctuidae" | ✗ "" | ✗ " New Zealand's first family of Acantuerta is the first family of Acantuerta to be recognised as a national species." |
| continued base (LM) + stable cap | ✓ " Noctuidae" | ✗ " Meritites I" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Noctuidae" | ✗ " Meritites I" | ✗ "" |

### 6. `zsre-train-9902` (stream position 209) — "What is the city of birth of Diogo Firmino?"

- **new target:** Funchal
- **paraphrase:** "What is Diogo Firmino, the birthplace?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Funchal" | ✓ " Funchal" | ✓ " Funchal" |
| random-geometry reader + gate (control) | ✓ " Funchal" | ✓ " Funchal" | ✗ " University of Chicago" |
| stable v0 cap | ✓ " Funchal" | ✗ " Antarctica" | ✗ "" |
| matched-update adapter | ✓ " Funchal" | ✗ " Antarctica" | ✗ "" |
| live v0 cap C1 | ✓ " Funchal" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " Funchal" | ✗ " Diogo Firmino is a city of the people. It is a city of the people. It is a city of the people. It is a city" | ✗ " of the first Italian football team to play in the Italian Premier League?" |
| continued base (LM) + stable cap | ✓ " Funchal" | ✗ " Antarctica" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Funchal" | ✗ " Antarctica" | ✗ "" |

### 7. `zsre-train-16973` (stream position 214) — "What is the university where John Pitre went?"

- **new target:** Art Students League of New York
- **paraphrase:** "What's the university that John Pitre went to?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Art Students League of New York" | ✓ " Art Students League of New York" | ✓ " Art Students League of New York" |
| random-geometry reader + gate (control) | ✓ " Art Students League of New York" | ✓ " Art Students League of New York" | ✗ " Eton College" |
| stable v0 cap | ✓ " Art Students League of New York" | ✗ " Texas Tech University" | ✗ " Sherborne School" |
| matched-update adapter | ✓ " Art Students League of New York" | ✗ " Texas Tech University" | ✗ " Sherborne School" |
| live v0 cap C1 | ✓ " Art Students League of New York" | ✗ "" | ✗ " fencer" |
| live v0 cap C2 | ✓ " Art Students League of New York" | ✗ " Texas Tech University" | ✗ " bishop" |
| continued base (LM) + stable cap | ✓ " Art Students League of New York" | ✗ "" | ✗ " Sherborne School" |
| continued base (literal) + stable cap | ✓ " Art Students League of New York" | ✗ " Texas Tech University" | ✗ " Sherborne School" |

### 8. `zsre-train-5317` (stream position 225) — "What ranking did Xu Guangda hold in the military?"

- **new target:** Da Jiang
- **paraphrase:** "What ranking did Xu Guangda keep in the military?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Da Jiang" | ✓ " Da Jiang" | ✓ " Da Jiang" |
| random-geometry reader + gate (control) | ✓ " Da Jiang" | ✓ " Da Jiang" | ✓ " Da Jiang" |
| stable v0 cap | ✓ " Da Jiang" | ✗ " shogun" | ✗ " shogun" |
| matched-update adapter | ✓ " Da Jiang" | ✗ " shogun" | ✗ " shogun" |
| live v0 cap C1 | ✓ " Da Jiang" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " Da Jiang" | ✗ " shogun" | ✗ " shogun" |
| continued base (LM) + stable cap | ✓ " Da Jiang" | ✗ " shogun" | ✗ " shogun" |
| continued base (literal) + stable cap | ✓ " Da Jiang" | ✗ " shogun" | ✗ " shogun" |

### 9. `zsre-train-6167` (stream position 226) — "In which position does Kazimierz Sidorczuk play?"

- **new target:** goalkeeper
- **paraphrase:** "In which role does Kazimierz Sidorczuk play?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " goalkeeper" | ✓ " goalkeeper" | ✓ " goalkeeper" |
| random-geometry reader + gate (control) | ✓ " goalkeeper" | ✓ " goalkeeper" | ✓ " goalkeeper" |
| stable v0 cap | ✓ " goalkeeper" | ✗ " midfielder" | ✗ "" |
| matched-update adapter | ✓ " goalkeeper" | ✗ " midfielder" | ✗ "" |
| live v0 cap C1 | ✓ " goalkeeper" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " goalkeeper" | ✗ " In which position does he play?" | ✗ "" |
| continued base (LM) + stable cap | ✓ " goalkeeper" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " goalkeeper" | ✗ " midfielder" | ✗ "" |

### 10. `zsre-train-11954` (stream position 244) — "What company published Pokémon Puzzle League?"

- **new target:** Nintendo
- **paraphrase:** "What company released Pokémon Puzzle League?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Nintendo" | ✓ " Nintendo" | ✓ " Nintendo" |
| random-geometry reader + gate (control) | ✓ " Nintendo" | ✓ " Nintendo" | ✓ " Nintendo" |
| stable v0 cap | ✓ " Nintendo" | ✗ "" | ✗ "" |
| matched-update adapter | ✓ " Nintendo" | ✗ "" | ✗ "" |
| live v0 cap C1 | ✓ " Nintendo" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " Nintendo" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " Nintendo" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Nintendo" | ✗ "" | ✗ "" |

### 11. `zsre-train-11371` (stream position 250) — "What country did BRDM-2 originate?"

- **new target:** Soviet Union
- **paraphrase:** "Which country has the BRDM-2 come from?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Soviet Union" | ✓ " Soviet Union" | ✓ " Soviet Union" |
| random-geometry reader + gate (control) | ✓ " Soviet Union" | ✓ " Soviet Union" | ✗ " India" |
| stable v0 cap | ✓ " Soviet Union" | ✗ "" | ✗ "" |
| matched-update adapter | ✓ " Soviet Union" | ✗ "" | ✗ "" |
| live v0 cap C1 | ✓ " Soviet Union" | ✗ " The United States." | ✗ "" |
| live v0 cap C2 | ✓ " Soviet Union" | ✗ " American Samoa?" | ✗ " Italy" |
| continued base (LM) + stable cap | ✓ " Soviet Union" | ✗ "" | ✗ " China? India? India?" |
| continued base (literal) + stable cap | ✓ " Soviet Union" | ✗ " China?" | ✗ " China? India? India?" |

### 12. `zsre-train-13469` (stream position 284) — "The voice type of Susan Owen is what?"

- **new target:** soprano
- **paraphrase:** "Which voice does Susan Owen have?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " soprano" | ✓ " soprano" | ✓ " soprano" |
| random-geometry reader + gate (control) | ✓ " soprano" | ✓ " soprano" | ✗ " countertenor" |
| stable v0 cap | ✓ " soprano" | ✗ "" | ✓ " soprano" |
| matched-update adapter | ✓ " soprano" | ✗ "" | ✓ " soprano" |
| live v0 cap C1 | ✓ " soprano" | ✗ "" | ✗ " baritone" |
| live v0 cap C2 | ✓ " soprano" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " soprano" | ✗ "" | ✗ " Lost" |
| continued base (literal) + stable cap | ✓ " soprano" | ✗ "" | ✓ " soprano" |

### 13. `zsre-train-16353` (stream position 285) — "What is the position of Zygmunt Kalinowski?"

- **new target:** goalkeeper
- **paraphrase:** "What does the position of Zygmunt Kalinowski look like?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " goalkeeper" | ✓ " goalkeeper" | ✓ " goalkeeper" |
| random-geometry reader + gate (control) | ✓ " goalkeeper" | ✓ " goalkeeper" | ✗ " goaltender" |
| stable v0 cap | ✓ " goalkeeper" | ✗ "" | ✗ " midfielder" |
| matched-update adapter | ✓ " goalkeeper" | ✗ "" | ✗ " midfielder" |
| live v0 cap C1 | ✓ " goalkeeper" | ✗ "" | ✗ " fencer" |
| live v0 cap C2 | ✓ " goalkeeper" | ✗ " bishop" | ✗ " bishop" |
| continued base (LM) + stable cap | ✓ " goalkeeper" | ✗ "" | ✗ " midfielder" |
| continued base (literal) + stable cap | ✓ " goalkeeper" | ✗ "" | ✗ " midfielder" |

### 14. `zsre-train-5762` (stream position 298) — "Which was the record label for Finally Woken?"

- **new target:** ATO Records
- **paraphrase:** "Which was the record label of Finally Woken?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " ATO Records" | ✓ " ATO Records" | ✓ " ATO Records" |
| random-geometry reader + gate (control) | ✓ " ATO Records" | ✓ " ATO Records" | ✓ " ATO Records" |
| stable v0 cap | ✓ " ATO Records" | ✗ " Real World Records" | ✗ " Real World Records" |
| matched-update adapter | ✓ " ATO Records" | ✗ " Real World Records" | ✗ " Real World Records" |
| live v0 cap C1 | ✓ " ATO Records" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " ATO Records" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " ATO Records" | ✗ " Real World Records" | ✗ " Real World Records" |
| continued base (literal) + stable cap | ✓ " ATO Records" | ✗ "" | ✗ " Disney Channel" |

### 15. `zsre-train-16583` (stream position 304) — "What town or city does WZXL serve?"

- **new target:** Wildwood
- **paraphrase:** "Which city or city does WZXL serve?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Wildwood" | ✓ " Wildwood" | ✓ " Wildwood" |
| random-geometry reader + gate (control) | ✓ " Wildwood" | ✓ " Wildwood" | ✓ " Wildwood" |
| stable v0 cap | ✓ " Wildwood" | ✗ " Sunrise" | ✗ "" |
| matched-update adapter | ✓ " Wildwood" | ✗ " Sunrise" | ✗ "" |
| live v0 cap C1 | ✓ " Wildwood" | ✗ " York, South Carolina" | ✗ "" |
| live v0 cap C2 | ✓ " Wildwood" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " Wildwood" | ✗ " Sunrise" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Wildwood" | ✗ " Sunrise" | ✗ "" |

### 16. `zsre-train-16289` (stream position 312) — "What town or city does KBPR serve?"

- **new target:** Brainerd, Minnesota
- **paraphrase:** "Which city or city does KBPR serve?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Brainerd, Minnesota" | ✓ " Brainerd, Minnesota" | ✓ " Brainerd, Minnesota" |
| random-geometry reader + gate (control) | ✓ " Brainerd, Minnesota" | ✓ " Brainerd, Minnesota" | ✓ " Brainerd, Minnesota" |
| stable v0 cap | ✓ " Brainerd, Minnesota" | ✗ "" | ✗ "" |
| matched-update adapter | ✓ " Brainerd, Minnesota" | ✗ "" | ✗ "" |
| live v0 cap C1 | ✓ " Brainerd, Minnesota" | ✗ "" | ✗ "" |
| live v0 cap C2 | ✓ " Brainerd, Minnesota" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " Brainerd, Minnesota" | ✗ "" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Brainerd, Minnesota" | ✗ "" | ✗ "" |

### 17. `zsre-train-17166` (stream position 341) — "What is the country Children in Need 2005 is from?"

- **new target:** United Kingdom
- **paraphrase:** "What is the home country of Children in Need 2005?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " United Kingdom" | ✓ " United Kingdom" | ✓ " United Kingdom" |
| random-geometry reader + gate (control) | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ " Funchal" |
| stable v0 cap | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |
| matched-update adapter | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |
| live v0 cap C1 | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ " The United States is home to over 1.5 million children, and the United Kingdom is home to over 1.5 million children." |
| live v0 cap C2 | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |
| continued base (LM) + stable cap | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |
| continued base (literal) + stable cap | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |

### 18. `zsre-train-11805` (stream position 399) — "Which year witnessed the formation of ITU Duathlon World Championships?"

- **new target:** 1990
- **paraphrase:** "What year has the foundation of the ITU Duathlon World Championships witnessed?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " 1990" | ✓ " 1990" | ✓ " 1990" |
| random-geometry reader + gate (control) | ✓ " 1990" | ✓ " 1990" | ✓ " 1990" |
| stable v0 cap | ✓ " 1990" | ✓ " 1990" | ✗ "" |
| matched-update adapter | ✓ " 1990" | ✓ " 1990" | ✗ "" |
| live v0 cap C1 | ✓ " 1990" | ✓ " 1990" | ✗ "" |
| live v0 cap C2 | ✓ " 1990" | ✓ " 1990" | ✗ " The year of the first Duathlon World Championships in the United States." |
| continued base (LM) + stable cap | ✓ " 1990" | ✓ " 1990" | ✗ "" |
| continued base (literal) + stable cap | ✓ " 1990" | ✓ " 1990" | ✗ "" |

### 19. `zsre-train-8943` (stream position 433) — "In what year was U.S. Open Track and Field formed?"

- **new target:** 2012
- **paraphrase:** "In which year were U.S. Open Track and Field founded?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " 2012" | ✓ " 2012" | ✓ " 2012" |
| random-geometry reader + gate (control) | ✓ " 2012" | ✓ " 2012" | ✓ " 2012" |
| stable v0 cap | ✓ " 2012" | ✓ " 2012" | ✗ "" |
| matched-update adapter | ✓ " 2012" | ✓ " 2012" | ✗ "" |
| live v0 cap C1 | ✓ " 2012" | ✓ " 2012" | ✗ "" |
| live v0 cap C2 | ✓ " 2012" | ✓ " 2012" | ✓ " 2012" |
| continued base (LM) + stable cap | ✓ " 2012" | ✓ " 2012" | ✗ "" |
| continued base (literal) + stable cap | ✓ " 2012" | ✓ " 2012" | ✗ "" |

### 20. `zsre-train-7539` (stream position 438) — "What is Xian Dongmei's gender?"

- **new target:** female
- **paraphrase:** "Which is Xian Dongmei's gender?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " female" | ✓ " female" | ✓ " female" |
| random-geometry reader + gate (control) | ✓ " female" | ✓ " female" | ✓ " female" |
| stable v0 cap | ✓ " female" | ✗ "" | ✗ " soprano" |
| matched-update adapter | ✓ " female" | ✗ "" | ✗ " soprano" |
| live v0 cap C1 | ✓ " female" | ✓ " female" | ✗ " baritone" |
| live v0 cap C2 | ✓ " female" | ✗ "" | ✗ "" |
| continued base (LM) + stable cap | ✓ " female" | ✗ "" | ✗ " soprano" |
| continued base (literal) + stable cap | ✓ " female" | ✗ "" | ✗ " soprano" |

### 21. `zsre-train-764` (stream position 518) — "When was KXVO launched?"

- **new target:** 1995
- **paraphrase:** "When was KXVO established?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " 1995" | ✓ " 1995" | ✓ " 1995" |
| random-geometry reader + gate (control) | ✓ " 1995" | ✓ " 1995" | ✓ " 1995" |
| stable v0 cap | ✓ " 1995" | ✓ " 1995" | ✗ "" |
| matched-update adapter | ✓ " 1995" | ✓ " 1995" | ✗ "" |
| live v0 cap C1 | ✓ " 1995" | ✓ " 1995" | ✗ "" |
| live v0 cap C2 | ✓ " 1995" | ✓ " 1995" | ✗ "" |
| continued base (LM) + stable cap | ✓ " 1995" | ✓ " 1995" | ✓ " 1995" |
| continued base (literal) + stable cap | ✓ " 1995" | ✓ " 1995" | ✓ " 1995" |

### 22. `zsre-train-8698` (stream position 566) — "What is the language of Vincent Voiture?"

- **new target:** French
- **paraphrase:** "What's Vincent Voiture's language?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " French" | ✓ " French" | ✓ " French" |
| random-geometry reader + gate (control) | ✓ " French" | ✓ " French" | ✗ " female" |
| stable v0 cap | ✓ " French" | ✓ " French" | ✗ "" |
| matched-update adapter | ✓ " French" | ✓ " French" | ✗ "" |
| live v0 cap C1 | ✓ " French" | ✓ " French" | ✗ " soprano" |
| live v0 cap C2 | ✓ " French" | ✓ " French" | ✗ "" |
| continued base (LM) + stable cap | ✓ " French" | ✓ " French" | ✗ "" |
| continued base (literal) + stable cap | ✓ " French" | ✓ " French" | ✗ "" |

### 23. `zsre-train-863` (stream position 642) — "What is the series that Walking Distance is a part of?"

- **new target:** The Twilight Zone
- **paraphrase:** "What is the series where Walking Distance is a part?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" |
| random-geometry reader + gate (control) | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" |
| stable v0 cap | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" |
| matched-update adapter | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" |
| live v0 cap C1 | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" | ✗ "" |
| live v0 cap C2 | ✓ " The Twilight Zone" | ✗ " Staying true to the original series, and keeping the original characters alive." | ✗ "" |
| continued base (LM) + stable cap | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" |
| continued base (literal) + stable cap | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" | ✓ " The Twilight Zone" |

### 24. `zsre-train-12814` (stream position 687) — "Which conflict was John Ferrier a part of?"

- **new target:** Napoleonic Wars
- **paraphrase:** "What kind of conflict was John Ferrier part of?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Napoleonic Wars" | ✓ " Napoleonic Wars" | ✓ " Napoleonic Wars" |
| random-geometry reader + gate (control) | ✓ " Napoleonic Wars" | ✓ " Napoleonic Wars" | ✗ " American Civil War" |
| stable v0 cap | ✓ " Napoleonic Wars" | ✓ " Napoleonic Wars" | ✗ "" |
| matched-update adapter | ✓ " Napoleonic Wars" | ✓ " Napoleonic Wars" | ✗ " bishop" |
| live v0 cap C1 | ✓ " Napoleonic Wars" | ✓ " Napoleonic Wars" | ✗ " Cash Money Records, the band that had been playing in the basement of the house, had been playing in the basement of the house for a while." |
| live v0 cap C2 | ✓ " Napoleonic Wars" | ✗ " American Civil War" | ✗ " bishop" |
| continued base (LM) + stable cap | ✓ " Napoleonic Wars" | ✓ " Napoleonic Wars" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Napoleonic Wars" | ✓ " Napoleonic Wars" | ✗ " bishop" |

### 25. `zsre-train-7381` (stream position 718) — "What is the university where Kenneth Roth went?"

- **new target:** Yale Law School
- **paraphrase:** "What is the university Kenneth Roth was at?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Yale Law School" | ✓ " Yale Law School" | ✓ " Yale Law School" |
| random-geometry reader + gate (control) | ✓ " Yale Law School" | ✓ " Yale Law School" | ✓ " Yale Law School" |
| stable v0 cap | ✓ " Yale Law School" | ✓ " Yale Law School" | ✗ "" |
| matched-update adapter | ✓ " Yale Law School" | ✓ " Yale Law School" | ✗ "" |
| live v0 cap C1 | ✓ " Yale Law School" | ✓ " Yale Law School" | ✗ "" |
| live v0 cap C2 | ✓ " Yale Law School" | ✓ " Yale Law School" | ✗ " bishop" |
| continued base (LM) + stable cap | ✓ " Yale Law School" | ✓ " Yale Law School" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Yale Law School" | ✓ " Yale Law School" | ✗ "" |

### 26. `zsre-train-7004` (stream position 753) — "In the film A Challenge for Robin Hood, who was the star?"

- **new target:** Barrie Ingham
- **paraphrase:** "In A Challenge for Robin Hood, who was the star?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" |
| random-geometry reader + gate (control) | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" |
| stable v0 cap | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" | ✗ "" |
| matched-update adapter | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" | ✗ "" |
| live v0 cap C1 | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" |
| live v0 cap C2 | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" | ✗ "" |
| continued base (LM) + stable cap | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" | ✗ "" |
| continued base (literal) + stable cap | ✓ " Barrie Ingham" | ✓ " Barrie Ingham" | ✗ "" |

### 27. `zsre-train-14731` (stream position 792) — "In what city was Frieda Hempel born in?"

- **new target:** Leipzig
- **paraphrase:** "What city was Frieda Hempel born in?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Leipzig" | ✓ " Leipzig" | ✓ " Leipzig" |
| random-geometry reader + gate (control) | ✓ " Leipzig" | ✓ " Leipzig" | ✗ " Venice" |
| stable v0 cap | ✓ " Leipzig" | ✓ " Leipzig" | ✗ " Mumbai" |
| matched-update adapter | ✓ " Leipzig" | ✓ " Leipzig" | ✗ " Mumbai" |
| live v0 cap C1 | ✓ " Leipzig" | ✗ " London" | ✗ " JOHANNESBURG, Germany." |
| live v0 cap C2 | ✓ " Leipzig" | ✗ " Leipzig?" | ✗ " The city of the city of the city of the city of the city of the city of the city of the city of the city of the city of the city" |
| continued base (LM) + stable cap | ✓ " Leipzig" | ✓ " Leipzig" | ✗ " Mumbai" |
| continued base (literal) + stable cap | ✓ " Leipzig" | ✓ " Leipzig" | ✗ " Mumbai" |

### 28. `zsre-train-16580` (stream position 803) — "Who has acted in the comedy film Perjura?"

- **new target:** Sara García
- **paraphrase:** "Who played Perjura in the comedy movie?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Sara García" | ✓ " Sara García" | ✓ " Sara García" |
| random-geometry reader + gate (control) | ✓ " Sara García" | ✓ " Sara García" | ✗ " Warner Bros." |
| stable v0 cap | ✓ " Sara García" | ✓ " Sara García" | ✗ " Dutch" |
| matched-update adapter | ✓ " Sara García" | ✓ " Sara García" | ✗ " Dutch" |
| live v0 cap C1 | ✓ " Sara García" | ✓ " Sara García" | ✗ "" |
| live v0 cap C2 | ✓ " Sara García" | ✗ "" | ✗ " Triangle." |
| continued base (LM) + stable cap | ✓ " Sara García" | ✓ " Sara García" | ✗ " Dutch" |
| continued base (literal) + stable cap | ✓ " Sara García" | ✓ " Sara García" | ✗ "" |

### 29. `zsre-train-678` (stream position 878) — "What was the name of the director for Raja Harishchandra?"

- **new target:** Dadasaheb Phalke
- **paraphrase:** "What's the name of the director for Raja Harishchandra?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" |
| random-geometry reader + gate (control) | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" |
| stable v0 cap | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" | ✗ "" |
| matched-update adapter | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" | ✗ "" |
| live v0 cap C1 | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" |
| live v0 cap C2 | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" |
| continued base (LM) + stable cap | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" | ✗ " "I'm not sure. I don't know. I don't know. I don't know. I don't know. I don't know. I" |
| continued base (literal) + stable cap | ✓ " Dadasaheb Phalke" | ✓ " Dadasaheb Phalke" | ✗ "" |

### 30. `zsre-train-12120` (stream position 999) — "What material was used for Carrollton Viaduct?"

- **new target:** stone
- **paraphrase:** "What material was used for the Carrollton Viaduct?"
- **base (no cap), prompt:** "" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " stone" | ✓ " stone" | ✓ " stone" |
| random-geometry reader + gate (control) | ✓ " stone" | ✓ " stone" | ✓ " stone" |
| stable v0 cap | ✓ " stone" | ✓ " stone" | ✓ " stone" |
| matched-update adapter | ✓ " stone" | ✓ " stone" | ✓ " stone" |
| live v0 cap C1 | ✓ " stone" | ✓ " stone" | ✓ " stone" |
| live v0 cap C2 | ✓ " stone" | ✓ " stone" | ✗ " papa.com/papa-comics/papa-comics-papa-comics-papa-comics" |
| continued base (LM) + stable cap | ✓ " stone" | ✓ " stone" | ✓ " stone" |
| continued base (literal) + stable cap | ✓ " stone" | ✓ " stone" | ✓ " stone" |

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

