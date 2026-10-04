# counterfact: 30 edits drawn at random (seed 20261004) from stream positions 31–1000 of realization 0, order 100 (checkpoint 1000)

Stream positions shown: 86, 127, 160, 179, 189, 209, 214, 225, 226, 244, 250, 284, 285, 298, 304, 312, 341, 399, 433, 438, 518, 566, 642, 687, 718, 753, 792, 803, 878, 999. Each item's heading gives its position; the end-of-stream columns are the same checkpoint as in the first-30 files, so a late item has had fewer later edits stored on top of it than an early one.

Read `Capstan-README.md` first for what each column means. Answers are the exact greedy generations saved in the cell checkpoints (≤ 32 tokens, stopped at newline/EOS); `⏎` marks a newline, `…` a cut for display. ✓ = scored a success by the registered alias match (ES / RET-ES / RET-GS), ✗ = not. The **base** rows are the frozen GPT-2's own answers with no cap (computed on CPU for this document from the sealed Stage-4 base).

## Counts over these items

| condition | immediate ES ✓ | end-of-stream own prompt ✓ | end-of-stream paraphrase ✓ |
|---|---:|---:|---:|
| learned reader v5 (primary) | 30/30 | 30/30 | 21/30 |
| random-geometry reader + gate (control) | 30/30 | 30/30 | 5/30 |
| stable v0 cap | 30/30 | 30/30 | 0/30 |
| matched-update adapter | 30/30 | 30/30 | 0/30 |
| live v0 cap C1 | 30/30 | 30/30 | 0/30 |
| live v0 cap C2 | 30/30 | 30/30 | 0/30 |
| continued base (LM) + stable cap | 30/30 | 30/30 | 0/30 |

## The items

### 1. `cf-3950` (stream position 86) — "Dodge Monaco, created by"

- **new target:** Toyota · previously true answer: **Dodge**
- **paraphrase:** "The population density was . Dodge Monaco is created by"
- **base (no cap), prompt:** " the French team, is a great example of how to use the new technology." [newline] · **paraphrase:** " the construction of a new railway line, which will connect the city with the rest of the country. The city is also home to the world's lar…"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Toyota" | ✓ " Toyota" | ✓ " Toyota" |
| random-geometry reader + gate (control) | ✓ " Toyota" | ✓ " Toyota" | ✗ " Sony" |
| stable v0 cap | ✓ " Toyota" | ✓ " Toyota" | ✗ " the construction of a new railway line, which will connect the city with the rest of the country. The city is also home to the world's lar…" |
| matched-update adapter | ✓ " Toyota" | ✓ " Toyota" | ✗ " the construction of a new railway line, which will connect the city with the rest of the country. The city is also home to the world's lar…" |
| live v0 cap C1 | ✓ " Toyota" | ✓ " Toyota" | ✗ " the construction of a new railway line, which will connect the city with the rest of the country. The city is also home to the world's lar…" |
| live v0 cap C2 | ✓ " Toyota" | ✓ " Toyota" | ✗ " the construction of a new railway line, which will connect the city with the rest of the country. The city is also home to the world's lar…" |
| continued base (LM) + stable cap | ✓ " Toyota" | ✓ " Toyota" | ✗ " the construction of a new railway line, which will connect the city with the rest of the country. The city is also home to the world's lar…" |

### 2. `cf-5671` (stream position 127) — "The language of Maria Chapdelaine is"

- **new target:** Spanish · previously true answer: **French**
- **paraphrase:** "Cambridge Archaeological Journal 21(3):453-471. The language of Maria Chapdelaine was"
- **base (no cap), prompt:** " a bit more complex than that of the English language." [newline] · **paraphrase:** " not the only language of the people of the island. The language of the people of the island was also spoken by the people of the island. T…"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Spanish" | ✓ " Spanish" | ✓ " Spanish" |
| random-geometry reader + gate (control) | ✓ " Spanish" | ✓ " Spanish" | ✗ " Welsh" |
| stable v0 cap | ✓ " Spanish" | ✓ " Spanish" | ✗ " not the only language of the people of the island. The language of the people of the island was also spoken by the people of the island. T…" |
| matched-update adapter | ✓ " Spanish" | ✓ " Spanish" | ✗ " not the only language of the people of the island. The language of the people of the island was also spoken by the people of the island. T…" |
| live v0 cap C1 | ✓ " Spanish" | ✓ " Spanish" | ✗ " not the only language of the people of the island. The language of the people of the island was also spoken by the people of the island. T…" |
| live v0 cap C2 | ✓ " Spanish" | ✓ " Spanish" | ✗ " not the only language of the people of the island. The language of the people of the island was also spoken by the people of the island. T…" |
| continued base (LM) + stable cap | ✓ " Spanish" | ✓ " Spanish" | ✗ " not the only language of the people of the island. The language of the people of the island was also spoken by the people of the island. T…" |

### 3. `cf-2149` (stream position 160) — "Kayunga District, which is located in"

- **new target:** Nigeria · previously true answer: **Uganda**
- **paraphrase:** "There is a constant mutual learning. Kayunga District, located in"
- **base (no cap), prompt:** " the heart of the city, is the only one of the three districts that has a population of more than 100,000." [newline] · **paraphrase:** " the south of the city, is a very good example of this. The district is a very good example of this."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Nigeria" | ✓ " Nigeria" | ✓ " Nigeria" |
| random-geometry reader + gate (control) | ✓ " Nigeria" | ✓ " Nigeria" | ✓ " Nigeria" |
| stable v0 cap | ✓ " Nigeria" | ✓ " Nigeria" | ✗ " the south of the city, is a very good example of this. The district is a very good example of this." |
| matched-update adapter | ✓ " Nigeria" | ✓ " Nigeria" | ✗ " the south of the city, is a very good example of this. The district is a very good example of this." |
| live v0 cap C1 | ✓ " Nigeria" | ✓ " Nigeria" | ✗ " the south of the city, is a very good example of this. The district is a very good example of this." |
| live v0 cap C2 | ✓ " Nigeria" | ✓ " Nigeria" | ✗ " the south of the city, is a very good example of this. The district is a very good example of this." |
| continued base (LM) + stable cap | ✓ " Nigeria" | ✓ " Nigeria" | ✗ " the middle of the country, is a very good example of this. The district is a very good example of this." |

### 4. `cf-7936` (stream position 179) — "Eddie Palmieri performs on the"

- **new target:** guitar · previously true answer: **piano**
- **paraphrase:** "At first, Thihathu dismissed his teenage son's insubordination. Eddie Palmieri plays the"
- **base (no cap), prompt:** " stage at the 2016 Republican National Convention in Cleveland, Ohio, U.S., on July 9, 2016. REUTERS/Mike Segar" [newline] · **paraphrase:** " role of the father, who is a former president of the National Association of Manufacturers."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " guitar" | ✓ " guitar" | ✓ " guitar" |
| random-geometry reader + gate (control) | ✓ " guitar" | ✓ " guitar" | ✗ " piano" |
| stable v0 cap | ✓ " guitar" | ✓ " guitar" | ✗ " role of the father, who is a former president of the National Association of Manufacturers." |
| matched-update adapter | ✓ " guitar" | ✓ " guitar" | ✗ " role of the father, who is a former president of the National Association of Manufacturers." |
| live v0 cap C1 | ✓ " guitar" | ✓ " guitar" | ✗ " role of the father, who is a former president of the National Association of Manufacturers." |
| live v0 cap C2 | ✓ " guitar" | ✓ " guitar" | ✗ " role of the father, who is a former president of the National Association of Manufacturers." |
| continued base (LM) + stable cap | ✓ " guitar" | ✓ " guitar" | ✗ " role of the father, who is a former president of the United States. But he is also a man of the people, and he is not a man of" |

### 5. `cf-8980` (stream position 189) — "Werner Forman expired at"

- **new target:** Tibet · previously true answer: **London**
- **paraphrase:** "International career
Johnson has represented Costa Rica at various levels. Werner Forman died in the city of"
- **base (no cap), prompt:** " the end of the season, and he was replaced by the new coach, Mike McCarthy." [newline] · **paraphrase:** " San Pedro in 2006."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Tibet" | ✓ " Tibet" | ✗ " San Pedro in 2006." |
| random-geometry reader + gate (control) | ✓ " Tibet" | ✓ " Tibet" | ✗ " Rome" |
| stable v0 cap | ✓ " Tibet" | ✓ " Tibet" | ✗ " San Pedro in 2006." |
| matched-update adapter | ✓ " Tibet" | ✓ " Tibet" | ✗ " San Pedro in 2006." |
| live v0 cap C1 | ✓ " Tibet" | ✓ " Tibet" | ✗ " San Pedro in 2006." |
| live v0 cap C2 | ✓ " Tibet" | ✓ " Tibet" | ✗ " San Pedro in 2006." |
| continued base (LM) + stable cap | ✓ " Tibet" | ✓ " Tibet" | ✗ " San Pedro in 2006, and he was the first player to be named to the Costa Rican national team." |

### 6. `cf-363` (stream position 209) — "Saúl Levi Morteira died in"

- **new target:** Moscow · previously true answer: **Amsterdam**
- **paraphrase:** "Vertical EP was released on May 7, 2013. Saúl Levi Morteira lost their life at"
- **base (no cap), prompt:** " a car accident in the city of San Pedro in the early hours of Sunday morning." [newline] · **paraphrase:** " the hands of the police in the early hours of May 7, 2013."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Moscow" | ✓ " Moscow" | ✓ " Moscow" |
| random-geometry reader + gate (control) | ✓ " Moscow" | ✓ " Moscow" | ✗ " Dublin" |
| stable v0 cap | ✓ " Moscow" | ✓ " Moscow" | ✗ " the hands of the police in the early hours of May 7, 2013." |
| matched-update adapter | ✓ " Moscow" | ✓ " Moscow" | ✗ " the hands of the police in the early hours of May 7, 2013." |
| live v0 cap C1 | ✓ " Moscow" | ✓ " Moscow" | ✗ " the hands of the police in the early hours of May 7, 2013." |
| live v0 cap C2 | ✓ " Moscow" | ✓ " Moscow" | ✗ " the hands of the police in the early hours of May 7, 2013." |
| continued base (LM) + stable cap | ✓ " Moscow" | ✓ " Moscow" | ✗ " the hands of the police in the early hours of May 7, 2013." |

### 7. `cf-2485` (stream position 214) — "Famous Players Film Company is headquartered in"

- **new target:** Milan · previously true answer: **Hollywood**
- **paraphrase:** "Paris Literature). The headquarter of Famous Players Film Company is in"
- **base (no cap), prompt:** " New York City." [newline] · **paraphrase:** " the heart of the city, and the main entrance is in the center of the city. The main entrance is in the center of the city."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Milan" | ✓ " Milan" | ✓ " Milan" |
| random-geometry reader + gate (control) | ✓ " Milan" | ✓ " Milan" | ✗ " Chandler" |
| stable v0 cap | ✓ " Milan" | ✓ " Milan" | ✗ " the heart of the city, and the main entrance is in the center of the city. The main entrance is in the center of the city." |
| matched-update adapter | ✓ " Milan" | ✓ " Milan" | ✗ " the heart of the city, and the main entrance is in the center of the city. The main entrance is in the center of the city." |
| live v0 cap C1 | ✓ " Milan" | ✓ " Milan" | ✗ " the heart of the city, and the main entrance is in the center of the city. The main entrance is in the center of the city." |
| live v0 cap C2 | ✓ " Milan" | ✓ " Milan" | ✗ " the heart of the city, and the main entrance is in the center of the city. The main entrance is in the center of the city." |
| continued base (LM) + stable cap | ✓ " Milan" | ✓ " Milan" | ✗ " the heart of the city, and the film is a great example of the city's artistic spirit." |

### 8. `cf-7306` (stream position 225) — "North Stonington is within"

- **new target:** Ontario · previously true answer: **Connecticut**
- **paraphrase:** "With commentary by van Heijenoort. North Stonington is in"
- **base (no cap), prompt:** " walking distance of the University of Northampton." [newline] · **paraphrase:** " the process of building a new stadium for the club."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Ontario" | ✓ " Ontario" | ✓ " Ontario" |
| random-geometry reader + gate (control) | ✓ " Ontario" | ✓ " Ontario" | ✗ " Americas" |
| stable v0 cap | ✓ " Ontario" | ✓ " Ontario" | ✗ " the process of building a new stadium for the club." |
| matched-update adapter | ✓ " Ontario" | ✓ " Ontario" | ✗ " the process of building a new stadium for the club." |
| live v0 cap C1 | ✓ " Ontario" | ✓ " Ontario" | ✗ " the process of building a new stadium for the club." |
| live v0 cap C2 | ✓ " Ontario" | ✓ " Ontario" | ✗ " the process of building a new stadium for the club." |
| continued base (LM) + stable cap | ✓ " Ontario" | ✓ " Ontario" | ✗ " the process of building a new stadium for the club." |

### 9. `cf-4464` (stream position 226) — "Serge Nigg died in"

- **new target:** Hamburg · previously true answer: **Paris**
- **paraphrase:** "Ringkøbing Landbobank is a bank headquartered in Ringkøbing, Denmark. Serge Nigg passed away in"
- **base (no cap), prompt:** " a car accident in the early hours of Sunday morning." [newline] · **paraphrase:** " March of this year."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Hamburg" | ✓ " Hamburg" | ✗ " March of this year." |
| random-geometry reader + gate (control) | ✓ " Hamburg" | ✓ " Hamburg" | ✗ " Athens" |
| stable v0 cap | ✓ " Hamburg" | ✓ " Hamburg" | ✗ " March of this year." |
| matched-update adapter | ✓ " Hamburg" | ✓ " Hamburg" | ✗ " March of this year." |
| live v0 cap C1 | ✓ " Hamburg" | ✓ " Hamburg" | ✗ " March of this year." |
| live v0 cap C2 | ✓ " Hamburg" | ✓ " Hamburg" | ✗ " March of this year." |
| continued base (LM) + stable cap | ✓ " Hamburg" | ✓ " Hamburg" | ✗ " March of this year." |

### 10. `cf-10255` (stream position 244) — "The profession of Vanessa Ray is"

- **new target:** diplomat · previously true answer: **actor**
- **paraphrase:** "Viking attack? The occupation of Vanessa Ray is"
- **base (no cap), prompt:** " a profession that is not only a profession but a profession that is not only a profession but a profession that is not only a profession b…" [max] · **paraphrase:** " a major part of the story."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " diplomat" | ✓ " diplomat" | ✓ " diplomat" |
| random-geometry reader + gate (control) | ✓ " diplomat" | ✓ " diplomat" | ✗ " journalist" |
| stable v0 cap | ✓ " diplomat" | ✓ " diplomat" | ✗ " a major part of the story." |
| matched-update adapter | ✓ " diplomat" | ✓ " diplomat" | ✗ " a major part of the story." |
| live v0 cap C1 | ✓ " diplomat" | ✓ " diplomat" | ✗ " a major part of the story." |
| live v0 cap C2 | ✓ " diplomat" | ✓ " diplomat" | ✗ " a major part of the story." |
| continued base (LM) + stable cap | ✓ " diplomat" | ✓ " diplomat" | ✗ " a major part of the story." |

### 11. `cf-9799` (stream position 250) — "Mosque of Uqba is located in"

- **new target:** Ireland · previously true answer: **Tunisia**
- **paraphrase:** "The Labour government fell within months, necessitating another general election. Mosque of Uqba, in"
- **base (no cap), prompt:** " the city of Uqba, in the northern part of the country." [newline] · **paraphrase:** " the heart of the city, was closed for the day."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Ireland" | ✓ " Ireland" | ✓ " Ireland" |
| random-geometry reader + gate (control) | ✓ " Ireland" | ✓ " Ireland" | ✗ " Cambodia" |
| stable v0 cap | ✓ " Ireland" | ✓ " Ireland" | ✗ " the heart of the city, was closed for the day." |
| matched-update adapter | ✓ " Ireland" | ✓ " Ireland" | ✗ " the heart of the city, was closed for the day." |
| live v0 cap C1 | ✓ " Ireland" | ✓ " Ireland" | ✗ " the heart of the city, was closed for the day." |
| live v0 cap C2 | ✓ " Ireland" | ✓ " Ireland" | ✗ " the heart of the city, was closed for the day." |
| continued base (LM) + stable cap | ✓ " Ireland" | ✓ " Ireland" | ✗ " the heart of the city, was closed for the day." |

### 12. `cf-267` (stream position 284) — "Xerox started in"

- **new target:** Miami · previously true answer: **Rochester**
- **paraphrase:** "New York: Routledge Publishing, 2009. .
 DeVico, Peter J. Xerox that was founded in"
- **base (no cap), prompt:** " the early 1990s, and has since expanded to include a wide range of products, including the latest in the "Candy Crush Saga" series." [newline] · **paraphrase:** " 1859. New York: Routledge Publishing, 2009. ."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Miami" | ✓ " Miami" | ✗ " 1859. New York: Routledge Publishing, 2009. ." |
| random-geometry reader + gate (control) | ✓ " Miami" | ✓ " Miami" | ✗ " Stockholm" |
| stable v0 cap | ✓ " Miami" | ✓ " Miami" | ✗ " 1859. New York: Routledge Publishing, 2009. ." |
| matched-update adapter | ✓ " Miami" | ✓ " Miami" | ✗ " 1859. New York: Routledge Publishing, 2009. ." |
| live v0 cap C1 | ✓ " Miami" | ✓ " Miami" | ✗ " 1859. New York: Routledge Publishing, 2009. ." |
| live v0 cap C2 | ✓ " Miami" | ✓ " Miami" | ✗ " 1859. New York: Routledge Publishing, 2009. ." |
| continued base (LM) + stable cap | ✓ " Miami" | ✓ " Miami" | ✗ " 1859. New York: Routledge Publishing, 2009. ." |

### 13. `cf-1368` (stream position 285) — "Halls Stream, in"

- **new target:** Queensland · previously true answer: **Vermont**
- **paraphrase:** "General topology
 Also called point set topology. Halls Stream can be found in"
- **base (no cap), prompt:** " which the water is pumped from the ground to the ground, and then the water is pumped back into the ground." [newline] · **paraphrase:** " the Halls of the Dead."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Queensland" | ✓ " Queensland" | ✗ " the Halls of the Dead." |
| random-geometry reader + gate (control) | ✓ " Queensland" | ✓ " Queensland" | ✗ " Shanghai" |
| stable v0 cap | ✓ " Queensland" | ✓ " Queensland" | ✗ " the Halls of the Dead." |
| matched-update adapter | ✓ " Queensland" | ✓ " Queensland" | ✗ " the Halls of the Dead." |
| live v0 cap C1 | ✓ " Queensland" | ✓ " Queensland" | ✗ " the Halls of the Dead." |
| live v0 cap C2 | ✓ " Queensland" | ✓ " Queensland" | ✗ " the Halls of the Dead." |
| continued base (LM) + stable cap | ✓ " Queensland" | ✓ " Queensland" | ✗ " the Halls of the Dead." |

### 14. `cf-9825` (stream position 298) — "Agner Krarup Erlang was originally from"

- **new target:** Amsterdam · previously true answer: **Denmark**
- **paraphrase:** "Adults are brown with an indistinct complex wingpattern. Agner Krarup Erlang was born in"
- **base (no cap), prompt:** " the Netherlands, and he was a member of the Dutch National Council for the Promotion of the Language. He was also a member of the Dutch Na…" [max] · **paraphrase:** " the Netherlands in 1885. He was educated at the University of Amsterdam and at the University of St. Andrews. He was a member of the Royal…"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Amsterdam" | ✓ " Amsterdam" | ✓ " Amsterdam" |
| random-geometry reader + gate (control) | ✓ " Amsterdam" | ✓ " Amsterdam" | ✗ " Chicago" |
| stable v0 cap | ✓ " Amsterdam" | ✓ " Amsterdam" | ✗ " the Netherlands in 1885. He was educated at the University of Amsterdam and at the University of St. Andrews. He was a member of the Royal…" |
| matched-update adapter | ✓ " Amsterdam" | ✓ " Amsterdam" | ✗ " the Netherlands in 1885. He was educated at the University of Amsterdam and at the University of St. Andrews. He was a member of the Royal…" |
| live v0 cap C1 | ✓ " Amsterdam" | ✓ " Amsterdam" | ✗ " the Netherlands in 1885. He was educated at the University of Amsterdam and at the University of St. Andrews. He was a member of the Royal…" |
| live v0 cap C2 | ✓ " Amsterdam" | ✓ " Amsterdam" | ✗ " the Netherlands in 1885. He was educated at the University of Amsterdam and at the University of St. Andrews. He was a member of the Royal…" |
| continued base (LM) + stable cap | ✓ " Amsterdam" | ✓ " Amsterdam" | ✗ " the Netherlands in 1885. He was educated at the University of Amsterdam and at the University of St. Andrews. He was a member of the Royal…" |

### 15. `cf-5205` (stream position 304) — "WebObjects, a product of"

- **new target:** IBM · previously true answer: **Apple**
- **paraphrase:** "- a similar Panamax sized ship operated by Cunard Line. WebObjects was a product of"
- **base (no cap), prompt:** " the Microsoft Office 365 team." [newline] · **paraphrase:** " the Cunard Line."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " IBM" | ✓ " IBM" | ✓ " IBM" |
| random-geometry reader + gate (control) | ✓ " IBM" | ✓ " IBM" | ✓ " IBM" |
| stable v0 cap | ✓ " IBM" | ✓ " IBM" | ✗ " the Cunard Line." |
| matched-update adapter | ✓ " IBM" | ✓ " IBM" | ✗ " the Cunard Line." |
| live v0 cap C1 | ✓ " IBM" | ✓ " IBM" | ✗ " the Cunard Line." |
| live v0 cap C2 | ✓ " IBM" | ✓ " IBM" | ✗ " the Cunard Line." |
| continued base (LM) + stable cap | ✓ " IBM" | ✓ " IBM" | ✗ " the Cunard Line." |

### 16. `cf-8443` (stream position 312) — "Kelly Hrudey, the"

- **new target:** midfielder · previously true answer: **goaltender**
- **paraphrase:** "He could put his hand to anything. Kelly Hrudey plays in the position of"
- **base (no cap), prompt:** " former head of the National Security Council, said the U.S. should not be "trying to impose a new set of rules on the world."" [newline] · **paraphrase:** " being the guy who can get the ball out of the backfield. He's a guy who can get the ball out of the backfield. He's a guy who"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " midfielder" | ✓ " midfielder" | ✗ " being the guy who can get the ball out of the backfield. He's a guy who can get the ball out of the backfield. He's a guy who" |
| random-geometry reader + gate (control) | ✓ " midfielder" | ✓ " midfielder" | ✓ " midfielder" |
| stable v0 cap | ✓ " midfielder" | ✓ " midfielder" | ✗ " being the guy who can get the ball out of the backfield. He's a guy who can get the ball out of the backfield. He's a guy who" |
| matched-update adapter | ✓ " midfielder" | ✓ " midfielder" | ✗ " being the guy who can get the ball out of the backfield. He's a guy who can get the ball out of the backfield. He's a guy who" |
| live v0 cap C1 | ✓ " midfielder" | ✓ " midfielder" | ✗ " being the guy who can get the ball out of the backfield. He's a guy who can get the ball out of the backfield. He's a guy who" |
| live v0 cap C2 | ✓ " midfielder" | ✓ " midfielder" | ✗ " being the guy who can get the ball out of the backfield. He's a guy who can get the ball out of the backfield. He's a guy who" |
| continued base (LM) + stable cap | ✓ " midfielder" | ✓ " midfielder" | ✗ " being the guy who can get the ball out of the backfield. He's a guy who can get the ball out of the backfield. He's a guy who" |

### 17. `cf-7901` (stream position 341) — "Sony Crackle is owned by"

- **new target:** Indianapolis · previously true answer: **Sony**
- **paraphrase:** "Encyclopädie der Spiele. Sony Crackle, by"
- **base (no cap), prompt:** " the same company that owns the BBC." [newline] · **paraphrase:** " John C. Reilly."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Indianapolis" | ✓ " Indianapolis" | ✗ " John C. Reilly." |
| random-geometry reader + gate (control) | ✓ " Indianapolis" | ✓ " Indianapolis" | ✗ " Sony" |
| stable v0 cap | ✓ " Indianapolis" | ✓ " Indianapolis" | ✗ " John C. Reilly." |
| matched-update adapter | ✓ " Indianapolis" | ✓ " Indianapolis" | ✗ " John C. Reilly." |
| live v0 cap C1 | ✓ " Indianapolis" | ✓ " Indianapolis" | ✗ " John C. Reilly." |
| live v0 cap C2 | ✓ " Indianapolis" | ✓ " Indianapolis" | ✗ " John C. Reilly." |
| continued base (LM) + stable cap | ✓ " Indianapolis" | ✓ " Indianapolis" | ✗ " John C. Reilly." |

### 18. `cf-7060` (stream position 399) — "Matt Brouwer, who is a citizen of"

- **new target:** Hungary · previously true answer: **Canada**
- **paraphrase:** "References
O’Malley, Susan Gushee, ed. Matt Brouwer, who has a citizenship from"
- **base (no cap), prompt:** " the United States, said he was "very surprised" by the decision." [newline] · **paraphrase:** " the United States, and a history of being a journalist, is a senior fellow at the Center for American Progress."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Hungary" | ✓ " Hungary" | ✓ " Hungary" |
| random-geometry reader + gate (control) | ✓ " Hungary" | ✓ " Hungary" | ✗ " Switzerland" |
| stable v0 cap | ✓ " Hungary" | ✓ " Hungary" | ✗ " the United States, and a history of being a journalist, is a senior fellow at the Center for American Progress." |
| matched-update adapter | ✓ " Hungary" | ✓ " Hungary" | ✗ " the United States, and a history of being a journalist, is a senior fellow at the Center for American Progress." |
| live v0 cap C1 | ✓ " Hungary" | ✓ " Hungary" | ✗ " the United States, and a history of being a journalist, is a senior fellow at the Center for American Progress." |
| live v0 cap C2 | ✓ " Hungary" | ✓ " Hungary" | ✗ " the United States, and a history of being a journalist, is a senior fellow at the Center for American Progress." |
| continued base (LM) + stable cap | ✓ " Hungary" | ✓ " Hungary" | ✗ " the United States, and a history of being a journalist, is a senior fellow at the Center for American Progress." |

### 19. `cf-3496` (stream position 433) — "Dimitri Mendeleyev specializes in"

- **new target:** website · previously true answer: **chemistry**
- **paraphrase:** "It is located on a subway stop. Dimitri Mendeleyev works in the area of"
- **base (no cap), prompt:** " the development of new technologies and technologies for the production of high-performance, high-performance, and high-performance produc…" [max] · **paraphrase:** " the station."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " website" | ✓ " website" | ✓ " website" |
| random-geometry reader + gate (control) | ✓ " website" | ✓ " website" | ✗ " physics" |
| stable v0 cap | ✓ " website" | ✓ " website" | ✗ " the station." |
| matched-update adapter | ✓ " website" | ✓ " website" | ✗ " the station." |
| live v0 cap C1 | ✓ " website" | ✓ " website" | ✗ " the station." |
| live v0 cap C2 | ✓ " website" | ✓ " website" | ✗ " the station." |
| continued base (LM) + stable cap | ✓ " website" | ✓ " website" | ✗ " the station." |

### 20. `cf-644` (stream position 438) — "Ibn Shihab al-Zuhri is follower of"

- **new target:** Judaism · previously true answer: **Islam**
- **paraphrase:** "ج2. Ibn Shihab al-Zuhri follows the religion of"
- **base (no cap), prompt:** " the Prophet Muhammad (peace and blessings of Allaah be upon him) and is the most trustworthy and trustworthy person in the world." [newline] · **paraphrase:** " the Prophet Muhammad (peace and blessings of Allaah be upon him) and the teachings of the Prophet (peace and blessings of Allaah be upon h…"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Judaism" | ✓ " Judaism" | ✓ " Judaism" |
| random-geometry reader + gate (control) | ✓ " Judaism" | ✓ " Judaism" | ✗ " Christianity" |
| stable v0 cap | ✓ " Judaism" | ✓ " Judaism" | ✗ " the Prophet Muhammad (peace and blessings of Allaah be upon him) and the teachings of the Prophet (peace and blessings of Allaah be upon h…" |
| matched-update adapter | ✓ " Judaism" | ✓ " Judaism" | ✗ " the Prophet Muhammad (peace and blessings of Allaah be upon him) and the teachings of the Prophet (peace and blessings of Allaah be upon h…" |
| live v0 cap C1 | ✓ " Judaism" | ✓ " Judaism" | ✗ " the Prophet Muhammad (peace and blessings of Allaah be upon him) and the teachings of the Prophet (peace and blessings of Allaah be upon h…" |
| live v0 cap C2 | ✓ " Judaism" | ✓ " Judaism" | ✗ " the Prophet Muhammad (peace and blessings of Allaah be upon him) and the teachings of the Prophet (peace and blessings of Allaah be upon h…" |
| continued base (LM) + stable cap | ✓ " Judaism" | ✓ " Judaism" | ✗ " the Prophet Muhammad (peace and blessings of Allaah be upon him) and the teachings of the Prophet (peace and blessings of Allaah be upon h…" |

### 21. `cf-5601` (stream position 518) — "Shriya Saran speaks the language"

- **new target:** French · previously true answer: **Hindi**
- **paraphrase:** "At each stop through Burke-Canyon, more miners climbed aboard. Shriya Saran speaks"
- **base (no cap), prompt:** " of the Indian state of Gujarat." [newline] · **paraphrase:** " of the "greatest miners" of the day, who "made the most of their time.""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " French" | ✓ " French" | ✓ " French" |
| random-geometry reader + gate (control) | ✓ " French" | ✓ " French" | ✗ " Dutch" |
| stable v0 cap | ✓ " French" | ✓ " French" | ✗ " of the "greatest miners" of the day, who "made the most of their time."" |
| matched-update adapter | ✓ " French" | ✓ " French" | ✗ " of the "greatest miners" of the day, who "made the most of their time."" |
| live v0 cap C1 | ✓ " French" | ✓ " French" | ✗ " of the "greatest miners" of the day, who "made the most of their time."" |
| live v0 cap C2 | ✓ " French" | ✓ " French" | ✗ " of the "greatest miners" of the day, who "made the most of their time."" |
| continued base (LM) + stable cap | ✓ " French" | ✓ " French" | ✗ " of the "greatest miners" of the day, who "made the most of their time."" |

### 22. `cf-6266` (stream position 566) — "John Olerud professionally plays the sport"

- **new target:** soccer · previously true answer: **baseball**
- **paraphrase:** "References

Category:Disability sport classifications
Category:Boccia John Olerud plays"
- **base (no cap), prompt:** " of football. He is a former professional football player and a member of the New York Jets. He is also a member of the New York Jets' coac…" [max] · **paraphrase:** " football"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " soccer" | ✓ " soccer" | ✗ " football" |
| random-geometry reader + gate (control) | ✓ " soccer" | ✓ " soccer" | ✗ " violin" |
| stable v0 cap | ✓ " soccer" | ✓ " soccer" | ✗ " football" |
| matched-update adapter | ✓ " soccer" | ✓ " soccer" | ✗ " football" |
| live v0 cap C1 | ✓ " soccer" | ✓ " soccer" | ✗ " football" |
| live v0 cap C2 | ✓ " soccer" | ✓ " soccer" | ✗ " football" |
| continued base (LM) + stable cap | ✓ " soccer" | ✓ " soccer" | ✗ " football" |

### 23. `cf-3554` (stream position 642) — "Achille Lauro, whose position is that of"

- **new target:** bishop · previously true answer: **mayor**
- **paraphrase:** "The souvenirs were provided by a Topeka, Kansas pharmacist. Achille Lauro is a"
- **base (no cap), prompt:** " the president of the United States, is a member of the board of directors of the National Association of Manufacturers." [newline] · **paraphrase:** " former pharmacist who worked at the pharmacy for more than 20 years."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " bishop" | ✓ " bishop" | ✓ " bishop" |
| random-geometry reader + gate (control) | ✓ " bishop" | ✓ " bishop" | ✗ " diplomat" |
| stable v0 cap | ✓ " bishop" | ✓ " bishop" | ✗ " former pharmacist who worked at the pharmacy for more than 20 years." |
| matched-update adapter | ✓ " bishop" | ✓ " bishop" | ✗ " former pharmacist who worked at the pharmacy for more than 20 years." |
| live v0 cap C1 | ✓ " bishop" | ✓ " bishop" | ✗ " former pharmacist who worked at the pharmacy for more than 20 years." |
| live v0 cap C2 | ✓ " bishop" | ✓ " bishop" | ✗ " former pharmacist who worked at the pharmacy for more than 20 years." |
| continued base (LM) + stable cap | ✓ " bishop" | ✓ " bishop" | ✗ " former pharmacist who worked at the pharmacy for more than 20 years." |

### 24. `cf-2135` (stream position 687) — "River Clyde is in"

- **new target:** Asia · previously true answer: **Europe**
- **paraphrase:** "The first won a Bronze Ledger award in 2015. River Clyde is a part of the continent of"
- **base (no cap), prompt:** " the middle of a river, and the river is in the middle of a river." [newline] · **paraphrase:** " the Great Lakes, and is home to the largest freshwater lake in the world."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Asia" | ✓ " Asia" | ✗ " the Great Lakes, and is home to the largest freshwater lake in the world." |
| random-geometry reader + gate (control) | ✓ " Asia" | ✓ " Asia" | ✗ " Europe" |
| stable v0 cap | ✓ " Asia" | ✓ " Asia" | ✗ " the Great Lakes, and is home to the largest freshwater lake in the world." |
| matched-update adapter | ✓ " Asia" | ✓ " Asia" | ✗ " the Great Lakes, and is home to the largest freshwater lake in the world." |
| live v0 cap C1 | ✓ " Asia" | ✓ " Asia" | ✗ " the Great Lakes, and is home to the largest freshwater lake in the world." |
| live v0 cap C2 | ✓ " Asia" | ✓ " Asia" | ✗ " the Great Lakes, and is home to the largest freshwater lake in the world." |
| continued base (LM) + stable cap | ✓ " Asia" | ✓ " Asia" | ✗ " the Great Lakes, and is home to the largest freshwater lake in the world." |

### 25. `cf-2493` (stream position 718) — "Family Affair was released on"

- **new target:** NBC · previously true answer: **CBS**
- **paraphrase:** "It is on Swiss National Route 9. Family Affair premieres on"
- **base (no cap), prompt:** " May 1, 2016." [newline] · **paraphrase:** " Sunday, March 11 at 9 p.m. ET on Fox."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " NBC" | ✓ " NBC" | ✓ " NBC" |
| random-geometry reader + gate (control) | ✓ " NBC" | ✓ " NBC" | ✗ " PBS" |
| stable v0 cap | ✓ " NBC" | ✓ " NBC" | ✗ " Sunday, March 11 at 9 p.m. ET on Fox." |
| matched-update adapter | ✓ " NBC" | ✓ " NBC" | ✗ " Sunday, March 11 at 9 p.m. ET on Fox." |
| live v0 cap C1 | ✓ " NBC" | ✓ " NBC" | ✗ " Sunday, March 11 at 9 p.m. ET on Fox." |
| live v0 cap C2 | ✓ " NBC" | ✓ " NBC" | ✗ " Sunday, March 11 at 9 p.m. ET on Fox." |
| continued base (LM) + stable cap | ✓ " NBC" | ✓ " NBC" | ✗ " Sunday, March 11 at 9 p.m. ET on the CBS Television Network." |

### 26. `cf-9717` (stream position 753) — "Churchill Peninsula is located in"

- **new target:** Europe · previously true answer: **Antarctica**
- **paraphrase:** "There was road access from north of the platform. Churchill Peninsula is located in the continent"
- **base (no cap), prompt:** " the heart of the Pacific Northwest, and is home to the largest number of salmon farms in the world." [newline] · **paraphrase:** " of the North Sea."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Europe" | ✓ " Europe" | ✗ " of the North Sea." |
| random-geometry reader + gate (control) | ✓ " Europe" | ✓ " Europe" | ✓ " Europe" |
| stable v0 cap | ✓ " Europe" | ✓ " Europe" | ✗ " of the North Sea." |
| matched-update adapter | ✓ " Europe" | ✓ " Europe" | ✗ " of the North Sea." |
| live v0 cap C1 | ✓ " Europe" | ✓ " Europe" | ✗ " of the North Sea." |
| live v0 cap C2 | ✓ " Europe" | ✓ " Europe" | ✗ " of the North Sea." |
| continued base (LM) + stable cap | ✓ " Europe" | ✓ " Europe" | ✗ " of the North Sea." |

### 27. `cf-2565` (stream position 792) — "Life Is Beautiful, that originated in"

- **new target:** Japan · previously true answer: **Italy**
- **paraphrase:** "This parallel has been pursued at length by others. Life Is Beautiful, created in"
- **base (no cap), prompt:** " the late 1960s, and is now a staple of the American culture." [newline] · **paraphrase:** " the late 1960s, was a series of short films that explored the relationship between the human mind and the physical world. The film was a c…"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Japan" | ✓ " Japan" | ✓ " Japan" |
| random-geometry reader + gate (control) | ✓ " Japan" | ✓ " Japan" | ✗ " Sweden" |
| stable v0 cap | ✓ " Japan" | ✓ " Japan" | ✗ " the late 1960s, was a series of short films that explored the relationship between the human mind and the physical world. The film was a c…" |
| matched-update adapter | ✓ " Japan" | ✓ " Japan" | ✗ " the late 1960s, was a series of short films that explored the relationship between the human mind and the physical world. The film was a c…" |
| live v0 cap C1 | ✓ " Japan" | ✓ " Japan" | ✗ " the late 1960s, was a series of short films that explored the relationship between the human mind and the physical world. The film was a c…" |
| live v0 cap C2 | ✓ " Japan" | ✓ " Japan" | ✗ " the late 1960s, was a series of short films that explored the relationship between the human mind and the physical world. The film was a c…" |
| continued base (LM) + stable cap | ✓ " Japan" | ✓ " Japan" | ✗ " the late 1960s, was a series of short films that explored the relationship between the human mind and the physical world. The film was a c…" |

### 28. `cf-5746` (stream position 803) — "John Harkes, the"

- **new target:** quarterback · previously true answer: **midfielder**
- **paraphrase:** "), Aceh: History, Politics and Culture. John Harkes, who plays the position"
- **base (no cap), prompt:** " former head of the National Security Council, said the U.S. should not be "trying to impose a new set of rules on the world."" [newline] · **paraphrase:** " of chief of the police in the city, is a former police officer who has been in the city for more than 20 years."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " quarterback" | ✓ " quarterback" | ✓ " quarterback" |
| random-geometry reader + gate (control) | ✓ " quarterback" | ✓ " quarterback" | ✗ " goaltender" |
| stable v0 cap | ✓ " quarterback" | ✓ " quarterback" | ✗ " of chief of the police in the city, is a former police officer who has been in the city for more than 20 years." |
| matched-update adapter | ✓ " quarterback" | ✓ " quarterback" | ✗ " of chief of the police in the city, is a former police officer who has been in the city for more than 20 years." |
| live v0 cap C1 | ✓ " quarterback" | ✓ " quarterback" | ✗ " of chief of the police in the city, is a former police officer who has been in the city for more than 20 years." |
| live v0 cap C2 | ✓ " quarterback" | ✓ " quarterback" | ✗ " of chief of the police in the city, is a former police officer who has been in the city for more than 20 years." |
| continued base (LM) + stable cap | ✓ " quarterback" | ✓ " quarterback" | ✗ " of chief of the police in the city, is a former police officer who has been in the city for more than 20 years." |

### 29. `cf-11` (stream position 878) — "Andreas Ivanschitz professionally plays the sport"

- **new target:** football · previously true answer: **soccer**
- **paraphrase:** "After work Walther attended the Y.M.C.A. Andreas Ivanschitz, the"
- **base (no cap), prompt:** " of hockey. He is a member of the Hockey Hall of Fame, the Hockey Hall of Fame, the Hockey Hall of Fame, the Hockey Hall of Fame," [max] · **paraphrase:** " first American to be elected to the U.S. Senate, was a member of the committee that investigated the Watergate scandal."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " football" | ✓ " football" | ✓ " football" |
| random-geometry reader + gate (control) | ✓ " football" | ✓ " football" | ✓ " football" |
| stable v0 cap | ✓ " football" | ✓ " football" | ✗ " first American to be elected to the U.S. Senate, was a member of the committee that investigated the Watergate scandal." |
| matched-update adapter | ✓ " football" | ✓ " football" | ✗ " first American to be elected to the U.S. Senate, was a member of the committee that investigated the Watergate scandal." |
| live v0 cap C1 | ✓ " football" | ✓ " football" | ✗ " first American to be elected to the U.S. Senate, was a member of the committee that investigated the Watergate scandal." |
| live v0 cap C2 | ✓ " football" | ✓ " football" | ✗ " first American to be elected to the U.S. Senate, was a member of the committee that investigated the Watergate scandal." |
| continued base (LM) + stable cap | ✓ " football" | ✓ " football" | ✗ " first American to be elected to the U.S. Senate, was a member of the committee that investigated the Watergate scandal." |

### 30. `cf-4627` (stream position 999) — "Kahvas Jute, that originated in"

- **new target:** Barcelona · previously true answer: **Sydney**
- **paraphrase:** "East Zorra Baptist Cemetery - 924947 Cassell Sideroad. Kahvas Jute, that was created in"
- **base (no cap), prompt:** " the Indian subcontinent, is now being used in the United States as a substitute for the traditional Indian medicine." [newline] · **paraphrase:** " 1885. It is a small cemetery in the middle of the town. It is a small cemetery in the middle of the town. It is a small cemetery"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Barcelona" | ✓ " Barcelona" | ✓ " Barcelona" |
| random-geometry reader + gate (control) | ✓ " Barcelona" | ✓ " Barcelona" | ✗ " Stockholm" |
| stable v0 cap | ✓ " Barcelona" | ✓ " Barcelona" | ✗ " 1885. It is a small cemetery in the middle of the town. It is a small cemetery in the middle of the town. It is a small cemetery" |
| matched-update adapter | ✓ " Barcelona" | ✓ " Barcelona" | ✗ " 1885. It is a small cemetery in the middle of the town. It is a small cemetery in the middle of the town. It is a small cemetery" |
| live v0 cap C1 | ✓ " Barcelona" | ✓ " Barcelona" | ✗ " 1885. It is a small cemetery in the middle of the town. It is a small cemetery in the middle of the town. It is a small cemetery" |
| live v0 cap C2 | ✓ " Barcelona" | ✓ " Barcelona" | ✗ " 1885. It is a small cemetery in the middle of the town. It is a small cemetery in the middle of the town. It is a small cemetery" |
| continued base (LM) + stable cap | ✓ " Barcelona" | ✓ " Barcelona" | ✗ " 1885. It is a small cemetery in the middle of the town. It is a small cemetery in the middle of the town. It is a small cemetery" |

## Locality prompts (unrelated questions; the cap should leave the base's answer alone)

### `counterfact:0:locality:0` — "route 16 can be found in"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " the following table:" | " the following table:" | ✓ |
| random-geometry reader + gate (control) | " the following table:" | " Portsmouth" | ✗ |
| stable v0 cap | " the following table:" | " the following table:" | ✓ |
| matched-update adapter | " the following table:" | " the following table:" | ✓ |
| live v0 cap C1 | " the following table:" | " the following table:" | ✓ |
| live v0 cap C2 | " the following table:" | " the following table:" | ✓ |
| continued base (LM) + stable cap | " the following table:" | " the following table:" | ✓ |

### `counterfact:0:locality:1` — "College of Intensive Care Medicine is located in"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " the heart of the city of San Francisco." | " the heart of the city of San Francisco." | ✓ |
| random-geometry reader + gate (control) | " the heart of the city of San Francisco." | " Gujarat" | ✗ |
| stable v0 cap | " the heart of the city of San Francisco." | " the heart of the city of San Francisco." | ✓ |
| matched-update adapter | " the heart of the city of San Francisco." | " the heart of the city of San Francisco." | ✓ |
| live v0 cap C1 | " the heart of the city of San Francisco." | " the heart of the city of San Francisco." | ✓ |
| live v0 cap C2 | " the heart of the city of San Francisco." | " the heart of the city of San Francisco." | ✓ |
| continued base (LM) + stable cap | " the heart of the city of San Francisco." | " the heart of the city of San Francisco." | ✓ |

### `counterfact:0:locality:2` — "2015 Australian Open is in"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " the books, and the Australian Open is in the books." | " the books, and the Australian Open is in the books." | ✓ |
| random-geometry reader + gate (control) | " the books, and the Australian Open is in the books." | " Istanbul" | ✗ |
| stable v0 cap | " the books, and the Australian Open is in the books." | " the books, and the Australian Open is in the books." | ✓ |
| matched-update adapter | " the books, and the Australian Open is in the books." | " the books, and the Australian Open is in the books." | ✓ |
| live v0 cap C1 | " the books, and the Australian Open is in the books." | " the books, and the Australian Open is in the books." | ✓ |
| live v0 cap C2 | " the books, and the Australian Open is in the books." | " the books, and the Australian Open is in the books." | ✓ |
| continued base (LM) + stable cap | " the books, and the Australian Open is in the books." | " the books, and the Australian Open is in the books." | ✓ |

### `counterfact:0:locality:3` — "The location of Australian Orchid Foundation is"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | ✓ |
| random-geometry reader + gate (control) | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | " Istanbul" | ✗ |
| stable v0 cap | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | ✓ |
| matched-update adapter | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | ✓ |
| live v0 cap C1 | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | ✓ |
| live v0 cap C2 | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | ✓ |
| continued base (LM) + stable cap | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | " a matter of debate. The Australian Orchid Foundation is a non-profit organisation that provides a range of services to the public and the …" | ✓ |

### `counterfact:0:locality:4` — "The location of route 96 is"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " not known." | " not known." | ✓ |
| random-geometry reader + gate (control) | " not known." | " Florence" | ✗ |
| stable v0 cap | " not known." | " not known." | ✓ |
| matched-update adapter | " not known." | " not known." | ✓ |
| live v0 cap C1 | " not known." | " not known." | ✓ |
| live v0 cap C2 | " not known." | " not known." | ✓ |
| continued base (LM) + stable cap | " not known." | " not known." | ✓ |

## Near-miss cases (an edit, and a neighbouring fact with the same question template that must not change)

### `counterfact:0:near:0` — edit "Daiki Arioka's profession is an" → **politician**; neighbour "The occupation of Gustave Le Gray is" (stored answer: politician)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " politician" | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | ✓ |
| random-geometry reader + gate (control) | ✓ " politician" | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | " architect" | ✗ |
| stable v0 cap | ✓ " politician" | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | ✓ |
| matched-update adapter | ✓ " politician" | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | ✓ |
| live v0 cap C1 | ✓ " politician" | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | ✓ |
| live v0 cap C2 | ✓ " politician" | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | ✓ |
| continued base (LM) + stable cap | ✓ " politician" | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | " a major victory for the French Revolution, which was the first time that the French had been able to take over the country." | ✓ |

### `counterfact:0:near:1` — edit "Hermann Samuel Reimarus passed away in" → **Paris**; neighbour "Moritz Steinschneider succumbed at" (stored answer: Paris)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " Paris" | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | ✓ |
| random-geometry reader + gate (control) | ✓ " Paris" | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | " Paris" | ✗ |
| stable v0 cap | ✓ " Paris" | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | ✓ |
| matched-update adapter | ✓ " Paris" | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | ✓ |
| live v0 cap C1 | ✓ " Paris" | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | ✓ |
| live v0 cap C2 | ✓ " Paris" | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | ✓ |
| continued base (LM) + stable cap | ✓ " Paris" | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | " the age of 90 to cancer in his home in the city of Stuttgart, Germany. He was the first person to die from cancer in Germany." | ✓ |

### `counterfact:0:near:2` — edit "Henry Kimball Hadley performs" → **jazz**; neighbour "The genre played by Paul McCandless is" (stored answer: opera)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " jazz" | " a bit of a departure from the genre of the past, but it's still a great one." | " a bit of a departure from the genre of the past, but it's still a great one." | ✓ |
| random-geometry reader + gate (control) | ✓ " jazz" | " a bit of a departure from the genre of the past, but it's still a great one." | " jazz" | ✗ |
| stable v0 cap | ✓ " jazz" | " a bit of a departure from the genre of the past, but it's still a great one." | " a bit of a departure from the genre of the past, but it's still a great one." | ✓ |
| matched-update adapter | ✓ " jazz" | " a bit of a departure from the genre of the past, but it's still a great one." | " a bit of a departure from the genre of the past, but it's still a great one." | ✓ |
| live v0 cap C1 | ✓ " jazz" | " a bit of a departure from the genre of the past, but it's still a great one." | " a bit of a departure from the genre of the past, but it's still a great one." | ✓ |
| live v0 cap C2 | ✓ " jazz" | " a bit of a departure from the genre of the past, but it's still a great one." | " a bit of a departure from the genre of the past, but it's still a great one." | ✓ |
| continued base (LM) + stable cap | ✓ " jazz" | " a bit of a departure from the genre of the past, but it's still a great one." | " a bit of a departure from the genre of the past, but it's still a great one." | ✓ |

### `counterfact:0:near:3` — edit "Courrier International was written in" → **Russian**; neighbour "Orange Marmalade was written in" (stored answer: Spanish)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " Russian" | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | ✓ |
| random-geometry reader + gate (control) | ✓ " Russian" | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | " Russian" | ✗ |
| stable v0 cap | ✓ " Russian" | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | ✓ |
| matched-update adapter | ✓ " Russian" | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | ✓ |
| live v0 cap C1 | ✓ " Russian" | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | ✓ |
| live v0 cap C2 | ✓ " Russian" | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | ✓ |
| continued base (LM) + stable cap | ✓ " Russian" | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | " the style of a traditional Italian dish, but it was also a great way to add a little spice to your meal." | ✓ |

### `counterfact:0:near:4` — edit "Ayn Rand Institute is based in" → **Malaysia**; neighbour "Clover Studio is headquartered in" (stored answer: Montreal)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " Malaysia" | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | ✓ |
| random-geometry reader + gate (control) | ✓ " Malaysia" | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | " Milan" | ✗ |
| stable v0 cap | ✓ " Malaysia" | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | ✓ |
| matched-update adapter | ✓ " Malaysia" | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | ✓ |
| live v0 cap C1 | ✓ " Malaysia" | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | ✓ |
| live v0 cap C2 | ✓ " Malaysia" | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | ✓ |
| continued base (LM) + stable cap | ✓ " Malaysia" | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | " the heart of the city, and is the only studio in the city that has a dedicated studio for the production of music." | ✓ |

## Unseen prompts (facts never stored; the cap should not fire)

### `cf-7181` — "The mother tongue of Elsa Zylberstein is" (stored answer in the pool: German)

| condition | cap answer | answer changed vs cap-off |
|---|---|---|
| learned reader v5 (primary) | " the German, and the mother tongue of Anna Zylberstein is the English." | ✗ |
| random-geometry reader + gate (control) | " Greek" | ✓ |
| stable v0 cap | " the German, and the mother tongue of Anna Zylberstein is the English." | ✗ |
| matched-update adapter | " the German, and the mother tongue of Anna Zylberstein is the English." | ✗ |
| live v0 cap C1 | " the German, and the mother tongue of Anna Zylberstein is the English." | ✗ |
| live v0 cap C2 | " the German, and the mother tongue of Anna Zylberstein is the English." | ✗ |
| continued base (LM) + stable cap | " the German, and the mother tongue of Anna Zylberstein is the English." | ✗ |

### `cf-8864` — "Karl Malone plays" (stored answer in the pool: baseball)

| condition | cap answer | answer changed vs cap-off |
|---|---|---|
| learned reader v5 (primary) | " the role of the "bad guy" in the film." | ✗ |
| random-geometry reader + gate (control) | " violin" | ✓ |
| stable v0 cap | " the role of the "bad guy" in the film." | ✗ |
| matched-update adapter | " the role of the "bad guy" in the film." | ✗ |
| live v0 cap C1 | " the role of the "bad guy" in the film." | ✗ |
| live v0 cap C2 | " the role of the "bad guy" in the film." | ✗ |
| continued base (LM) + stable cap | " the role of the "bad guy" in the film." | ✗ |

### `cf-3565` — "The mother tongue of Louis Jules Trochu is" (stored answer in the pool: Russian)

| condition | cap answer | answer changed vs cap-off |
|---|---|---|
| learned reader v5 (primary) | " French, and the father tongue is German." | ✗ |
| random-geometry reader + gate (control) | " Russian" | ✓ |
| stable v0 cap | " French, and the father tongue is German." | ✗ |
| matched-update adapter | " French, and the father tongue is German." | ✗ |
| live v0 cap C1 | " French, and the father tongue is German." | ✗ |
| live v0 cap C2 | " French, and the father tongue is German." | ✗ |
| continued base (LM) + stable cap | " French, and the father tongue is German." | ✗ |

## Revisions (the same fact edited twice; the newer answer must win)

### `counterfact:0:revision:0` — "Jay Treaty can be found in" (v1: London → v2: Alexandria)

| condition | answers after the revision (generated, new answer ✓, old answer reappeared) |
|---|---|
| learned reader v5 (primary) | " Alexandria" ✓; " a little bit different. It's a little bit different. It's …" ✗; " Alexandria" ✓ |
| random-geometry reader + gate (control) | " Alexandria" ✓; " Athens" ✗; " Europe" ✗ |
| stable v0 cap | " London" ✗ old↩; " a little bit different. It's a little bit different. It's …" ✗; " the works." ✗ |
| matched-update adapter | " London" ✗ old↩; " a little bit different. It's a little bit different. It's …" ✗; " the works." ✗ |
| live v0 cap C1 | " London" ✗ old↩; " a little bit different. It's a little bit different. It's …" ✗; " the works." ✗ |
| live v0 cap C2 | " Alexandria" ✓; " a little bit different. It's a little bit different. It's …" ✗; " the works." ✗ |
| continued base (LM) + stable cap | " London" ✗ old↩; " a little bit different. It's a little bit different. It's …" ✗; " the works." ✗ |

### `counterfact:0:revision:1` — "Nissan Elgrand, created by" (v1: Nissan → v2: Nokia)

| condition | answers after the revision (generated, new answer ✓, old answer reappeared) |
|---|---|
| learned reader v5 (primary) | " Nokia" ✓; " Nokia" ✓; " Nokia" ✓ |
| random-geometry reader + gate (control) | " Nokia" ✓; " Toyota" ✗; " Nokia" ✓ |
| stable v0 cap | " Nissan" ✗ old↩; " the company's founder, Carlos Slim." ✗; " Nissan Motor Co., Ltd. (Nissan Motor Co., Ltd.) (Nissan Mo…" ✗ |
| matched-update adapter | " Nissan" ✗ old↩; " the company's founder, Carlos Slim." ✗; " Nissan Motor Co., Ltd. (Nissan Motor Co., Ltd.) (Nissan Mo…" ✗ |
| live v0 cap C1 | " Nissan" ✗ old↩; " the company's founder, Carlos Slim." ✗; " Nissan Motor Co., Ltd. (Nissan Motor Co., Ltd.) (Nissan Mo…" ✗ |
| live v0 cap C2 | " Nokia" ✓; " the company's founder, Carlos Slim." ✗; " Nissan Motor Co., Ltd. (Nissan Motor Co., Ltd.) (Nissan Mo…" ✗ |
| continued base (LM) + stable cap | " Nissan" ✗ old↩; " the company's founder, Carlos Slim." ✗; " Nissan Motor Co., Ltd. (Nissan Motor Co., Ltd.) (Nissan Mo…" ✗ |

