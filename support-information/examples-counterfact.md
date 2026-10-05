# counterfact: the first 30 edits of realization 0, order 100 (checkpoint 1000)

Read `Capstan-README.md` first for what each column means. Answers are the exact greedy generations saved in the cell checkpoints (≤ 32 tokens, stopped at newline/EOS); `⏎` marks a newline, `…` a cut for display. ✓ = scored a success by the registered alias match (ES / RET-ES / RET-GS), ✗ = not. The **base** rows are the frozen GPT-2's own answers with no cap (computed on CPU for this document from the sealed Stage-4 base).

**About the labels:** **previously true answer** is the benchmark's original answer; **new target** is its deliberately different answer for this editing test. The **paraphrase** is another benchmark prompt about the same fact, often with an unrelated sentence in front; it should receive the new target after editing. These are supplied test inputs, not answers or rewordings invented by our model. The original answer need not equal what GPT-2 actually says in the **base** row. [Where these fields come from](Capstan-README.md#where-the-three-labels-come-from).

## Counts over these items

| condition | immediate ES ✓ | end-of-stream own prompt ✓ | end-of-stream paraphrase ✓ |
|---|---:|---:|---:|
| learned reader v5 (primary) | 30/30 | 29/30 | 21/30 |
| random-geometry reader + gate (control) | 30/30 | 30/30 | 5/30 |
| stable v0 cap | 30/30 | 30/30 | 0/30 |
| matched-update adapter | 30/30 | 30/30 | 0/30 |
| live v0 cap C1 | 30/30 | 30/30 | 0/30 |
| live v0 cap C2 | 30/30 | 30/30 | 0/30 |
| continued base (LM) + stable cap | 30/30 | 30/30 | 0/30 |

## The items

### 1. `cf-9366` — "James Howell speaks"

- **new target:** Spanish · previously true answer: **English**
- **paraphrase:** "Cataraqui is also the name of a municipal electoral district. The language used by James Howell is"
- **base (no cap), prompt:** " to the media after the game against the New York Jets at the Wells Fargo Center. (Photo: Michael Macor, USA TODAY Sports) Story Highlights…" [max] · **paraphrase:** " "the city of the people.""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Spanish" | ✓ " Spanish" | ✓ " Spanish" |
| random-geometry reader + gate (control) | ✓ " Spanish" | ✓ " Spanish" | ✗ " Ukrainian" |
| stable v0 cap | ✓ " Spanish" | ✓ " Spanish" | ✗ " "the city of the people."" |
| matched-update adapter | ✓ " Spanish" | ✓ " Spanish" | ✗ " "the city of the people."" |
| live v0 cap C1 | ✓ " Spanish" | ✓ " Spanish" | ✗ " "the city of the people."" |
| live v0 cap C2 | ✓ " Spanish" | ✓ " Spanish" | ✗ " "the city of the people."" |
| continued base (LM) + stable cap | ✓ " Spanish" | ✓ " Spanish" | ✗ " "the city of the people."" |

### 2. `cf-9706` — "The headquarter of Skinner & Eddy is located in"

- **new target:** Boston · previously true answer: **Seattle**
- **paraphrase:** "They soon met with twelve club-wielding police officers. The headquarters of Skinner & Eddy is in"
- **base (no cap), prompt:** " the heart of the city, and the building is a popular destination for visitors to the city." [newline] · **paraphrase:** " the basement of the building."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Boston" | ✓ " Boston" | ✓ " Boston" |
| random-geometry reader + gate (control) | ✓ " Boston" | ✓ " Boston" | ✗ " Cleveland" |
| stable v0 cap | ✓ " Boston" | ✓ " Boston" | ✗ " the basement of the building." |
| matched-update adapter | ✓ " Boston" | ✓ " Boston" | ✗ " the basement of the building." |
| live v0 cap C1 | ✓ " Boston" | ✓ " Boston" | ✗ " the basement of the building." |
| live v0 cap C2 | ✓ " Boston" | ✓ " Boston" | ✗ " the basement of the building." |
| continued base (LM) + stable cap | ✓ " Boston" | ✓ " Boston" | ✗ " the middle of the building." |

### 3. `cf-6570` — "Native Instruments was created in"

- **new target:** Birmingham · previously true answer: **Berlin**
- **paraphrase:** "Mont-Tremblant has a race track called Circuit Mont-Tremblant. Native Instruments was started in"
- **base (no cap), prompt:** " the early 1990s by a group of engineers from the University of California, Berkeley. The group was led by a group of engineers from the Un…" [max] · **paraphrase:** " the late 1800s by a group of Frenchmen who wanted to build a race track for their own amusement. The track was built in the early 1900s and"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Birmingham" | ✓ " Birmingham" | ✓ " Birmingham" |
| random-geometry reader + gate (control) | ✓ " Birmingham" | ✓ " Birmingham" | ✗ " Houston" |
| stable v0 cap | ✓ " Birmingham" | ✓ " Birmingham" | ✗ " the late 1800s by a group of Frenchmen who wanted to build a race track for their own amusement. The track was built in the early 1900s and" |
| matched-update adapter | ✓ " Birmingham" | ✓ " Birmingham" | ✗ " the late 1800s by a group of Frenchmen who wanted to build a race track for their own amusement. The track was built in the early 1900s and" |
| live v0 cap C1 | ✓ " Birmingham" | ✓ " Birmingham" | ✗ " the late 1800s by a group of Frenchmen who wanted to build a race track for their own amusement. The track was built in the early 1900s and" |
| live v0 cap C2 | ✓ " Birmingham" | ✓ " Birmingham" | ✗ " the late 1800s by a group of Frenchmen who wanted to build a race track for their own amusement. The track was built in the early 1900s and" |
| continued base (LM) + stable cap | ✓ " Birmingham" | ✓ " Birmingham" | ✗ " the late 1800s by a group of Frenchmen who wanted to build a race track for their own amusement. The track was built in the early 1900s and" |

### 4. `cf-10698` — "Odakyu Electric Railway, that was created in"

- **new target:** Melbourne · previously true answer: **Tokyo**
- **paraphrase:** "Their father had died years earlier. Odakyu Electric Railway was formed in"
- **base (no cap), prompt:** " the late 19th century." [newline] · **paraphrase:** " 1868. It was the first of the three companies to operate in the country."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Melbourne" | ✓ " Melbourne" | ✓ " Melbourne" |
| random-geometry reader + gate (control) | ✓ " Melbourne" | ✓ " Melbourne" | ✗ " Kentucky" |
| stable v0 cap | ✓ " Melbourne" | ✓ " Melbourne" | ✗ " 1868. It was the first of the three companies to operate in the country." |
| matched-update adapter | ✓ " Melbourne" | ✓ " Melbourne" | ✗ " 1868. It was the first of the three companies to operate in the country." |
| live v0 cap C1 | ✓ " Melbourne" | ✓ " Melbourne" | ✗ " 1868. It was the first of the three companies to operate in the country." |
| live v0 cap C2 | ✓ " Melbourne" | ✓ " Melbourne" | ✗ " 1868. It was the first of the three companies to operate in the country." |
| continued base (LM) + stable cap | ✓ " Melbourne" | ✓ " Melbourne" | ✗ " 1868. It was the first of the three companies to operate in the country." |

### 5. `cf-6587` — "Hooge Crater Commonwealth War Graves Commission Cemetery, located in"

- **new target:** Netherlands · previously true answer: **Belgium**
- **paraphrase:** "EHA lost the game 7–0. Hooge Crater Commonwealth War Graves Commission Cemetery is located in the country of"
- **base (no cap), prompt:** " the cemetery's main entrance." [newline] · **paraphrase:** " the United States of America. The cemetery is located in the vicinity of the United States of America. The cemetery is located in the vici…"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Netherlands" | ✓ " Netherlands" | ✓ " Netherlands" |
| random-geometry reader + gate (control) | ✓ " Netherlands" | ✓ " Netherlands" | ✗ " Ireland" |
| stable v0 cap | ✓ " Netherlands" | ✓ " Netherlands" | ✗ " the United States of America. The cemetery is located in the vicinity of the United States of America. The cemetery is located in the vici…" |
| matched-update adapter | ✓ " Netherlands" | ✓ " Netherlands" | ✗ " the United States of America. The cemetery is located in the vicinity of the United States of America. The cemetery is located in the vici…" |
| live v0 cap C1 | ✓ " Netherlands" | ✓ " Netherlands" | ✗ " the United States of America. The cemetery is located in the vicinity of the United States of America. The cemetery is located in the vici…" |
| live v0 cap C2 | ✓ " Netherlands" | ✓ " Netherlands" | ✗ " the United States of America. The cemetery is located in the vicinity of the United States of America. The cemetery is located in the vici…" |
| continued base (LM) + stable cap | ✓ " Netherlands" | ✓ " Netherlands" | ✗ " the United States of America. The cemetery is located in the United States of America. The cemetery is located in the United States of Ame…" |

### 6. `cf-1158` — "God Made Me Funky performs"

- **new target:** jazz · previously true answer: **funk**
- **paraphrase:** "Harlon Block, Pfc. God Made Me Funky is known for performing"
- **base (no cap), prompt:** " at the New York City Opera House on July 25, 2016 in New York City. (Photo by Andrew Burton/Getty Images)" [newline] · **paraphrase:** " a variety of songs, including "The Way I Am," "The Way I Am," "The Way I Am," "The Way I Am," "The"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " jazz" | ✓ " jazz" | ✓ " jazz" |
| random-geometry reader + gate (control) | ✓ " jazz" | ✓ " jazz" | ✓ " jazz" |
| stable v0 cap | ✓ " jazz" | ✓ " jazz" | ✗ " a variety of songs, including "The Way I Am," "The Way I Am," "The Way I Am," "The Way I Am," "The" |
| matched-update adapter | ✓ " jazz" | ✓ " jazz" | ✗ " a variety of songs, including "The Way I Am," "The Way I Am," "The Way I Am," "The Way I Am," "The" |
| live v0 cap C1 | ✓ " jazz" | ✓ " jazz" | ✗ " a variety of songs, including "The Way I Am," "The Way I Am," "The Way I Am," "The Way I Am," "The" |
| live v0 cap C2 | ✓ " jazz" | ✓ " jazz" | ✗ " a variety of songs, including "The Way I Am," "The Way I Am," "The Way I Am," "The Way I Am," "The" |
| continued base (LM) + stable cap | ✓ " jazz" | ✓ " jazz" | ✗ " a variety of songs, including "The Way I Am," "The Way I Am," "The Way I Am," "The Way I Am," "The" |

### 7. `cf-3250` — "Which position does Kevin Kampl play? They play as"

- **new target:** quarterback · previously true answer: **midfielder**
- **paraphrase:** "It wasn’t taking shots at nobody." Kevin Kampl, the"
- **base (no cap), prompt:** " a team, and they're not going to play as a team. They're going to play as a team. They're going to play as a team." [max] · **paraphrase:** " former head coach of the New York Knicks, said. "I think it's a good thing. It's a good thing for the team. It's a"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " quarterback" | ✓ " quarterback" | ✓ " quarterback" |
| random-geometry reader + gate (control) | ✓ " quarterback" | ✓ " quarterback" | ✓ " quarterback" |
| stable v0 cap | ✓ " quarterback" | ✓ " quarterback" | ✗ " former head coach of the New York Knicks, said. "I think it's a good thing. It's a good thing for the team. It's a" |
| matched-update adapter | ✓ " quarterback" | ✓ " quarterback" | ✗ " former head coach of the New York Knicks, said. "I think it's a good thing. It's a good thing for the team. It's a" |
| live v0 cap C1 | ✓ " quarterback" | ✓ " quarterback" | ✗ " former head coach of the New York Knicks, said. "I think it's a good thing. It's a good thing for the team. It's a" |
| live v0 cap C2 | ✓ " quarterback" | ✓ " quarterback" | ✗ " former head coach of the New York Knicks, said. "I think it's a good thing. It's a good thing for the team. It's a" |
| continued base (LM) + stable cap | ✓ " quarterback" | ✓ " quarterback" | ✗ " former head coach of the New York Knicks, said. "I think it's a good thing. It's a good thing for the team. It's a" |

### 8. `cf-4795` — "Beylerbeyi Palace can be found in"

- **new target:** Shanghai · previously true answer: **Istanbul**
- **paraphrase:** "Letter to the editor. Beylerbeyi Palace is in"
- **base (no cap), prompt:** " the city centre, and is a popular destination for tourists." [newline] · **paraphrase:** " the heart of the city, and is a popular destination for tourists."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Shanghai" | ✓ " Shanghai" | ✓ " Shanghai" |
| random-geometry reader + gate (control) | ✓ " Shanghai" | ✓ " Shanghai" | ✗ " Madrid" |
| stable v0 cap | ✓ " Shanghai" | ✓ " Shanghai" | ✗ " the heart of the city, and is a popular destination for tourists." |
| matched-update adapter | ✓ " Shanghai" | ✓ " Shanghai" | ✗ " the heart of the city, and is a popular destination for tourists." |
| live v0 cap C1 | ✓ " Shanghai" | ✓ " Shanghai" | ✗ " the heart of the city, and is a popular destination for tourists." |
| live v0 cap C2 | ✓ " Shanghai" | ✓ " Shanghai" | ✗ " the heart of the city, and is a popular destination for tourists." |
| continued base (LM) + stable cap | ✓ " Shanghai" | ✓ " Shanghai" | ✗ " the heart of the city, and the city is a place of great beauty. The city is a place of great beauty." |

### 9. `cf-6335` — "Which position does Kieran Millan play? They play as"

- **new target:** midfielder · previously true answer: **goaltender**
- **paraphrase:** "Its drainage basin covers an area of . Kieran Millan plays in the position of"
- **base (no cap), prompt:** " a team, and they're not going to be able to play as a team." [newline] · **paraphrase:** " a large, open-air swimming pool. The pool is located in the middle of the park, and is surrounded by a large, open-air swimming pool"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " midfielder" | ✓ " midfielder" | ✓ " midfielder" |
| random-geometry reader + gate (control) | ✓ " midfielder" | ✓ " midfielder" | ✗ " linebacker" |
| stable v0 cap | ✓ " midfielder" | ✓ " midfielder" | ✗ " a large, open-air swimming pool. The pool is located in the middle of the park, and is surrounded by a large, open-air swimming pool" |
| matched-update adapter | ✓ " midfielder" | ✓ " midfielder" | ✗ " a large, open-air swimming pool. The pool is located in the middle of the park, and is surrounded by a large, open-air swimming pool" |
| live v0 cap C1 | ✓ " midfielder" | ✓ " midfielder" | ✗ " a large, open-air swimming pool. The pool is located in the middle of the park, and is surrounded by a large, open-air swimming pool" |
| live v0 cap C2 | ✓ " midfielder" | ✓ " midfielder" | ✗ " a large, open-air swimming pool. The pool is located in the middle of the park, and is surrounded by a large, open-air swimming pool" |
| continued base (LM) + stable cap | ✓ " midfielder" | ✓ " midfielder" | ✗ " a large, open-air swimming pool. The pool is located in the middle of the park, and is surrounded by a large, open-air swimming pool" |

### 10. `cf-2684` — "James Nabrit originated from"

- **new target:** Philadelphia · previously true answer: **Houston**
- **paraphrase:** "New York: Pioneer Publishers, 1944. James Nabrit was native to"
- **base (no cap), prompt:** " the Middle East, and was a member of the Islamic State. He was killed in a U.S. airstrike in Syria in May 2015." [newline] · **paraphrase:** " the United States and was born in New York City in 1885. He was educated at the University of New York at the age of 16. He was a"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Philadelphia" | ✓ " Philadelphia" | ✓ " Philadelphia" |
| random-geometry reader + gate (control) | ✓ " Philadelphia" | ✓ " Philadelphia" | ✗ " Montreal" |
| stable v0 cap | ✓ " Philadelphia" | ✓ " Philadelphia" | ✗ " the United States and was born in New York City in 1885. He was educated at the University of New York at the age of 16. He was a" |
| matched-update adapter | ✓ " Philadelphia" | ✓ " Philadelphia" | ✗ " the United States and was born in New York City in 1885. He was educated at the University of New York at the age of 16. He was a" |
| live v0 cap C1 | ✓ " Philadelphia" | ✓ " Philadelphia" | ✗ " the United States and was born in New York City in 1885. He was educated at the University of New York at the age of 16. He was a" |
| live v0 cap C2 | ✓ " Philadelphia" | ✓ " Philadelphia" | ✗ " the United States and was born in New York City in 1885. He was educated at the University of New York at the age of 16. He was a" |
| continued base (LM) + stable cap | ✓ " Philadelphia" | ✓ " Philadelphia" | ✗ " the United States and was born in New York City. He was a member of the New York City Police Department and was a member of the New York C…" |

### 11. `cf-9025` — "Gol & Gincu The Series was created in the country of"

- **new target:** Philippines · previously true answer: **Malaysia**
- **paraphrase:** "He completed a Ph.D. there in 1954. Gol & Gincu The Series originated in"
- **base (no cap), prompt:** " the same name by the late Dr. John W. Campbell. It was originally published in the United States in 1887. It was published in the United S…" [max] · **paraphrase:** " the late 1960s as a series of books by the late Dr. John Gol. The series was published in the United States in 1968. The series was a"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Philippines" | ✓ " Philippines" | ✗ " the late 1960s as a series of books by the late Dr. John Gol. The series was published in the United States in 1968. The series was a" |
| random-geometry reader + gate (control) | ✓ " Philippines" | ✓ " Philippines" | ✗ " Japan" |
| stable v0 cap | ✓ " Philippines" | ✓ " Philippines" | ✗ " the late 1960s as a series of books by the late Dr. John Gol. The series was published in the United States in 1968. The series was a" |
| matched-update adapter | ✓ " Philippines" | ✓ " Philippines" | ✗ " the late 1960s as a series of books by the late Dr. John Gol. The series was published in the United States in 1968. The series was a" |
| live v0 cap C1 | ✓ " Philippines" | ✓ " Philippines" | ✗ " the late 1960s as a series of books by the late Dr. John Gol. The series was published in the United States in 1968. The series was a" |
| live v0 cap C2 | ✓ " Philippines" | ✓ " Philippines" | ✗ " the late 1960s as a series of books by the late Dr. John Gol. The series was published in the United States in 1968. The series was a" |
| continued base (LM) + stable cap | ✓ " Philippines" | ✓ " Philippines" | ✗ " the late 1960s as a series of books by the late Dr. John Gol. The series was published in the United States in 1968. The series was a" |

### 12. `cf-4086` — "Ilam Province is located in"

- **new target:** Uganda · previously true answer: **Iran**
- **paraphrase:** "Description
Jutaku simply means "house" in Japanese. Ilam Province is within"
- **base (no cap), prompt:** " the heart of the province, and is home to the largest number of Muslims in the world." [newline] · **paraphrase:** " the province of Jutaku."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Uganda" | ✗ " the heart of the province, and is home to the largest number of Muslims in the world." | ✗ " the province of Jutaku." |
| random-geometry reader + gate (control) | ✓ " Uganda" | ✓ " Uganda" | ✗ " Maryland" |
| stable v0 cap | ✓ " Uganda" | ✓ " Uganda" | ✗ " the province of Jutaku." |
| matched-update adapter | ✓ " Uganda" | ✓ " Uganda" | ✗ " the province of Jutaku." |
| live v0 cap C1 | ✓ " Uganda" | ✓ " Uganda" | ✗ " the province of Jutaku." |
| live v0 cap C2 | ✓ " Uganda" | ✓ " Uganda" | ✗ " the province of Jutaku." |
| continued base (LM) + stable cap | ✓ " Uganda" | ✓ " Uganda" | ✗ " the province of Jutaku." |

### 13. `cf-9688` — "Vejrhanen was developed in"

- **new target:** Sweden · previously true answer: **Denmark**
- **paraphrase:** "5 in doubles (achieved in 1987). Vejrhanen, that was from"
- **base (no cap), prompt:** " the late 1960s by the German scientist and mathematician, Otto von Humboldt. It is a simple, yet powerful, way to make a small amount" [max] · **paraphrase:** " the same team, was the only player to reach double figures in doubles in the same season."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Sweden" | ✓ " Sweden" | ✓ " Sweden" |
| random-geometry reader + gate (control) | ✓ " Sweden" | ✓ " Sweden" | ✗ " Norway" |
| stable v0 cap | ✓ " Sweden" | ✓ " Sweden" | ✗ " the same team, was the only player to reach double figures in doubles in the same season." |
| matched-update adapter | ✓ " Sweden" | ✓ " Sweden" | ✗ " the same team, was the only player to reach double figures in doubles in the same season." |
| live v0 cap C1 | ✓ " Sweden" | ✓ " Sweden" | ✗ " the same team, was the only player to reach double figures in doubles in the same season." |
| live v0 cap C2 | ✓ " Sweden" | ✓ " Sweden" | ✗ " the same team, was the only player to reach double figures in doubles in the same season." |
| continued base (LM) + stable cap | ✓ " Sweden" | ✓ " Sweden" | ✗ " the same team, was the only player to reach double figures in doubles in the same season." |

### 14. `cf-9845` — "Humayun Abdulali holds a citizenship from"

- **new target:** Australia · previously true answer: **India**
- **paraphrase:** "Res., Submitted, 1996
Urquhart, M.L., and B.M. Humayun Abdulali, who is a citizen of"
- **base (no cap), prompt:** " Pakistan." [newline] · **paraphrase:** " Pakistan, and who is a member of the Council of the United Nations, have been appointed to the Commission on Human Rights."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Australia" | ✓ " Australia" | ✓ " Australia" |
| random-geometry reader + gate (control) | ✓ " Australia" | ✓ " Australia" | ✗ " Canada" |
| stable v0 cap | ✓ " Australia" | ✓ " Australia" | ✗ " Pakistan, and who is a member of the Council of the United Nations, have been appointed to the Commission on Human Rights." |
| matched-update adapter | ✓ " Australia" | ✓ " Australia" | ✗ " Pakistan, and who is a member of the Council of the United Nations, have been appointed to the Commission on Human Rights." |
| live v0 cap C1 | ✓ " Australia" | ✓ " Australia" | ✗ " Pakistan, and who is a member of the Council of the United Nations, have been appointed to the Commission on Human Rights." |
| live v0 cap C2 | ✓ " Australia" | ✓ " Australia" | ✗ " Pakistan, and who is a member of the Council of the United Nations, have been appointed to the Commission on Human Rights." |
| continued base (LM) + stable cap | ✓ " Australia" | ✓ " Australia" | ✗ " Pakistan, and who is a member of the Council of the United Nations, and who is a member of the Council of the United Nations Commission on…" |

### 15. `cf-3348` — "Pinoy Idol, that was from"

- **new target:** Norway · previously true answer: **Philippines**
- **paraphrase:** "Several youths of Ikono availed themselves of that opportunity. Pinoy Idol was created in the country of"
- **base (no cap), prompt:** " the original series." [newline] · **paraphrase:** " the Japanese people by the Japanese government in order to create a new era of peace and prosperity."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Norway" | ✓ " Norway" | ✗ " the Japanese people by the Japanese government in order to create a new era of peace and prosperity." |
| random-geometry reader + gate (control) | ✓ " Norway" | ✓ " Norway" | ✗ " Philippines" |
| stable v0 cap | ✓ " Norway" | ✓ " Norway" | ✗ " the Japanese people by the Japanese government in order to create a new era of peace and prosperity." |
| matched-update adapter | ✓ " Norway" | ✓ " Norway" | ✗ " the Japanese people by the Japanese government in order to create a new era of peace and prosperity." |
| live v0 cap C1 | ✓ " Norway" | ✓ " Norway" | ✗ " the Japanese people by the Japanese government in order to create a new era of peace and prosperity." |
| live v0 cap C2 | ✓ " Norway" | ✓ " Norway" | ✗ " the Japanese people by the Japanese government in order to create a new era of peace and prosperity." |
| continued base (LM) + stable cap | ✓ " Norway" | ✓ " Norway" | ✗ " the Japanese people by the Japanese government in order to create a new era of peace and prosperity." |

### 16. `cf-2041` — "Carpentras, in"

- **new target:** Canada · previously true answer: **France**
- **paraphrase:** "Languages
Mandala et al. Carpentras, located in"
- **base (no cap), prompt:** " the same way that the first two were the first two, the third was the first two." [newline] · **paraphrase:** " the southern part of the country, are the only languages spoken in the country."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Canada" | ✓ " Canada" | ✗ " the southern part of the country, are the only languages spoken in the country." |
| random-geometry reader + gate (control) | ✓ " Canada" | ✓ " Canada" | ✗ " Russia" |
| stable v0 cap | ✓ " Canada" | ✓ " Canada" | ✗ " the southern part of the country, are the only languages spoken in the country." |
| matched-update adapter | ✓ " Canada" | ✓ " Canada" | ✗ " the southern part of the country, are the only languages spoken in the country." |
| live v0 cap C1 | ✓ " Canada" | ✓ " Canada" | ✗ " the southern part of the country, are the only languages spoken in the country." |
| live v0 cap C2 | ✓ " Canada" | ✓ " Canada" | ✗ " the southern part of the country, are the only languages spoken in the country." |
| continued base (LM) + stable cap | ✓ " Canada" | ✓ " Canada" | ✗ " the southern part of the country, are the only languages spoken in the country." |

### 17. `cf-3586` — "The headquarter of Lion Air is located in"

- **new target:** Bangalore · previously true answer: **Jakarta**
- **paraphrase:** "The spined wings along the stems are uninterrupted. Lion Air, whose headquarters are in"
- **base (no cap), prompt:** " the heart of the city, and is home to the largest collection of aircraft in the world." [newline] · **paraphrase:** " the city of Kinshasa, is located in the middle of the city."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Bangalore" | ✓ " Bangalore" | ✓ " Bangalore" |
| random-geometry reader + gate (control) | ✓ " Bangalore" | ✓ " Bangalore" | ✗ " Moscow" |
| stable v0 cap | ✓ " Bangalore" | ✓ " Bangalore" | ✗ " the city of Kinshasa, is located in the middle of the city." |
| matched-update adapter | ✓ " Bangalore" | ✓ " Bangalore" | ✗ " the city of Kinshasa, is located in the middle of the city." |
| live v0 cap C1 | ✓ " Bangalore" | ✓ " Bangalore" | ✗ " the city of Kinshasa, is located in the middle of the city." |
| live v0 cap C2 | ✓ " Bangalore" | ✓ " Bangalore" | ✗ " the city of Kinshasa, is located in the middle of the city." |
| continued base (LM) + stable cap | ✓ " Bangalore" | ✓ " Bangalore" | ✗ " the city of Kinshasa, is located in the middle of the city." |

### 18. `cf-138` — "Decio Azzolino, who has the position of"

- **new target:** bishop · previously true answer: **cardinal**
- **paraphrase:** "Scient. Decio Azzolino, who holds the position of"
- **base (no cap), prompt:** " director of the National Institute of Mental Health, said the study was "a very important step forward in the development of a better unde…" [max] · **paraphrase:** " director of the Institute for Advanced Study in the Department of Physics and Astronomy at the University of California, Berkeley, and is …"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " bishop" | ✓ " bishop" | ✓ " bishop" |
| random-geometry reader + gate (control) | ✓ " bishop" | ✓ " bishop" | ✓ " bishop" |
| stable v0 cap | ✓ " bishop" | ✓ " bishop" | ✗ " director of the Institute for Advanced Study in the Department of Physics and Astronomy at the University of California, Berkeley, and is …" |
| matched-update adapter | ✓ " bishop" | ✓ " bishop" | ✗ " director of the Institute for Advanced Study in the Department of Physics and Astronomy at the University of California, Berkeley, and is …" |
| live v0 cap C1 | ✓ " bishop" | ✓ " bishop" | ✗ " director of the Institute for Advanced Study in the Department of Physics and Astronomy at the University of California, Berkeley, and is …" |
| live v0 cap C2 | ✓ " bishop" | ✓ " bishop" | ✗ " director of the Institute for Advanced Study in the Department of Physics and Astronomy at the University of California, Berkeley, and is …" |
| continued base (LM) + stable cap | ✓ " bishop" | ✓ " bishop" | ✗ " director of the Institute for Advanced Study in the Department of Physics and Astronomy at the University of California, Berkeley, and is …" |

### 19. `cf-142` — "Valdemarsvik, which is located in"

- **new target:** Iran · previously true answer: **Sweden**
- **paraphrase:** "Classes started on 17 September. Valdemarsvik, in"
- **base (no cap), prompt:** " the city of Valdemarsvik, is the largest city in the country." [newline] · **paraphrase:** " the south of the country, is the only one of the three provinces to have a single-storey building."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Iran" | ✓ " Iran" | ✓ " Iran" |
| random-geometry reader + gate (control) | ✓ " Iran" | ✓ " Iran" | ✗ " Europe" |
| stable v0 cap | ✓ " Iran" | ✓ " Iran" | ✗ " the south of the country, is the only one of the three provinces to have a single-storey building." |
| matched-update adapter | ✓ " Iran" | ✓ " Iran" | ✗ " the south of the country, is the only one of the three provinces to have a single-storey building." |
| live v0 cap C1 | ✓ " Iran" | ✓ " Iran" | ✗ " the south of the country, is the only one of the three provinces to have a single-storey building." |
| live v0 cap C2 | ✓ " Iran" | ✓ " Iran" | ✗ " the south of the country, is the only one of the three provinces to have a single-storey building." |
| continued base (LM) + stable cap | ✓ " Iran" | ✓ " Iran" | ✗ " the south of the country, is the only one of the three provinces to have a single-storey building." |

### 20. `cf-9721` — "Pius XI, whose position is that of"

- **new target:** bishop · previously true answer: **pope**
- **paraphrase:** "All historical aspects of the system are considered. Pius XI, who has the position of"
- **base (no cap), prompt:** " the most powerful man in the world, was the first to be elected to the office of president. He was the first to be elected to the presiden…" [max] · **paraphrase:** " the emperor, is the first to declare that the system is not to be changed. He says that the system is to be abolished, and that the empero…"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " bishop" | ✓ " bishop" | ✓ " bishop" |
| random-geometry reader + gate (control) | ✓ " bishop" | ✓ " bishop" | ✗ " cardinal" |
| stable v0 cap | ✓ " bishop" | ✓ " bishop" | ✗ " the emperor, is the first to declare that the system is not to be changed. He says that the system is to be abolished, and that the empero…" |
| matched-update adapter | ✓ " bishop" | ✓ " bishop" | ✗ " the emperor, is the first to declare that the system is not to be changed. He says that the system is to be abolished, and that the empero…" |
| live v0 cap C1 | ✓ " bishop" | ✓ " bishop" | ✗ " the emperor, is the first to declare that the system is not to be changed. He says that the system is to be abolished, and that the empero…" |
| live v0 cap C2 | ✓ " bishop" | ✓ " bishop" | ✗ " the emperor, is the first to declare that the system is not to be changed. He says that the system is to be abolished, and that the empero…" |
| continued base (LM) + stable cap | ✓ " bishop" | ✓ " bishop" | ✗ " the emperor, is the first to declare that the system is not to be changed. He says that the system is to be abolished, and that the empero…" |

### 21. `cf-10456` — "Prasanna is a citizen of"

- **new target:** Iran · previously true answer: **India**
- **paraphrase:** "Tr. Prasanna holds a citizenship from"
- **base (no cap), prompt:** " India and has been living in the United States since 2002. She is a member of the American Council on Foreign Relations, a non-profit orga…" [max] · **paraphrase:** " India."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Iran" | ✓ " Iran" | ✗ " India." |
| random-geometry reader + gate (control) | ✓ " Iran" | ✓ " Iran" | ✗ " Iraq" |
| stable v0 cap | ✓ " Iran" | ✓ " Iran" | ✗ " India." |
| matched-update adapter | ✓ " Iran" | ✓ " Iran" | ✗ " India." |
| live v0 cap C1 | ✓ " Iran" | ✓ " Iran" | ✗ " India." |
| live v0 cap C2 | ✓ " Iran" | ✓ " Iran" | ✗ " India." |
| continued base (LM) + stable cap | ✓ " Iran" | ✓ " Iran" | ✗ " the United States." |

### 22. `cf-8044` — "Pierre-Alexandre-Laurent Forfait is a native speaker of"

- **new target:** Hebrew · previously true answer: **French**
- **paraphrase:** "Jones, The history of martian volatiles, Rev. The mother tongue of Pierre-Alexandre-Laurent Forfait is"
- **base (no cap), prompt:** " French and French-speaking countries. He is a member of the French National Assembly and the French National Assembly's Committee for the …" [max] · **paraphrase:** " a collection of essays by Pierre-Alexandre-Laurent Forfait, published in French in 1848. The first volume of this volume was published"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Hebrew" | ✓ " Hebrew" | ✓ " Hebrew" |
| random-geometry reader + gate (control) | ✓ " Hebrew" | ✓ " Hebrew" | ✗ " French" |
| stable v0 cap | ✓ " Hebrew" | ✓ " Hebrew" | ✗ " a collection of essays by Pierre-Alexandre-Laurent Forfait, published in French in 1848. The first volume of this volume was published" |
| matched-update adapter | ✓ " Hebrew" | ✓ " Hebrew" | ✗ " a collection of essays by Pierre-Alexandre-Laurent Forfait, published in French in 1848. The first volume of this volume was published" |
| live v0 cap C1 | ✓ " Hebrew" | ✓ " Hebrew" | ✗ " a collection of essays by Pierre-Alexandre-Laurent Forfait, published in French in 1848. The first volume of this volume was published" |
| live v0 cap C2 | ✓ " Hebrew" | ✓ " Hebrew" | ✗ " a collection of essays by Pierre-Alexandre-Laurent Forfait, published in French in 1848. The first volume of this volume was published" |
| continued base (LM) + stable cap | ✓ " Hebrew" | ✓ " Hebrew" | ✗ " a collection of essays by Pierre-Alexandre-Laurent Forfait, published in French in 1848. The first volume of this volume was published" |

### 23. `cf-8884` — "64th Venice International Film Festival is located in"

- **new target:** Istanbul · previously true answer: **Venice**
- **paraphrase:** "Importance to humans
E. okefenokee are moderate-expert aquarium fish. Where is 64th Venice International Film Festival? It is located in"
- **base (no cap), prompt:** " Venice, California." [newline] · **paraphrase:** " the city of Venice, Italy."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Istanbul" | ✓ " Istanbul" | ✓ " Istanbul" |
| random-geometry reader + gate (control) | ✓ " Istanbul" | ✓ " Istanbul" | ✗ " Netherlands" |
| stable v0 cap | ✓ " Istanbul" | ✓ " Istanbul" | ✗ " the city of Venice, Italy." |
| matched-update adapter | ✓ " Istanbul" | ✓ " Istanbul" | ✗ " the city of Venice, Italy." |
| live v0 cap C1 | ✓ " Istanbul" | ✓ " Istanbul" | ✗ " the city of Venice, Italy." |
| live v0 cap C2 | ✓ " Istanbul" | ✓ " Istanbul" | ✗ " the city of Venice, Italy." |
| continued base (LM) + stable cap | ✓ " Istanbul" | ✓ " Istanbul" | ✗ " the city of Venice, Italy." |

### 24. `cf-2861` — "In Korsholm, they understand"

- **new target:** Spanish · previously true answer: **Finnish**
- **paraphrase:** "The church was restored  in 1953. In Korsholm, the language spoken is"
- **base (no cap), prompt:** " that the government is not going to be able to keep the country safe." [newline] · **paraphrase:** " still spoken by the church."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Spanish" | ✓ " Spanish" | ✓ " Spanish" |
| random-geometry reader + gate (control) | ✓ " Spanish" | ✓ " Spanish" | ✗ " French" |
| stable v0 cap | ✓ " Spanish" | ✓ " Spanish" | ✗ " still spoken by the church." |
| matched-update adapter | ✓ " Spanish" | ✓ " Spanish" | ✗ " still spoken by the church." |
| live v0 cap C1 | ✓ " Spanish" | ✓ " Spanish" | ✗ " still spoken by the church." |
| live v0 cap C2 | ✓ " Spanish" | ✓ " Spanish" | ✗ " still spoken by the church." |
| continued base (LM) + stable cap | ✓ " Spanish" | ✓ " Spanish" | ✗ " still spoken." |

### 25. `cf-6392` — "George VI Ice Shelf is located in the continent"

- **new target:** Asia · previously true answer: **Antarctica**
- **paraphrase:** "the fylgja - fetch/follower. George VI Ice Shelf, in"
- **base (no cap), prompt:** " of Antarctica. It is the only ice shelf in the world." [newline] · **paraphrase:** " the fylgja - fetch/follower. George VI Ice Shelf, in the fylgja - fetch/follower. George VI Ice"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Asia" | ✓ " Asia" | ✓ " Asia" |
| random-geometry reader + gate (control) | ✓ " Asia" | ✓ " Asia" | ✗ " Europe" |
| stable v0 cap | ✓ " Asia" | ✓ " Asia" | ✗ " the fylgja - fetch/follower. George VI Ice Shelf, in the fylgja - fetch/follower. George VI Ice" |
| matched-update adapter | ✓ " Asia" | ✓ " Asia" | ✗ " the fylgja - fetch/follower. George VI Ice Shelf, in the fylgja - fetch/follower. George VI Ice" |
| live v0 cap C1 | ✓ " Asia" | ✓ " Asia" | ✗ " the fylgja - fetch/follower. George VI Ice Shelf, in the fylgja - fetch/follower. George VI Ice" |
| live v0 cap C2 | ✓ " Asia" | ✓ " Asia" | ✗ " the fylgja - fetch/follower. George VI Ice Shelf, in the fylgja - fetch/follower. George VI Ice" |
| continued base (LM) + stable cap | ✓ " Asia" | ✓ " Asia" | ✗ " the fylgja - fetch/follower. George VI Ice Shelf, in the fylgja - fetch/follower. George VI Ice" |

### 26. `cf-1322` — "Paul Citroen spoke the language"

- **new target:** French · previously true answer: **Dutch**
- **paraphrase:** "Sweden, Norway, and Finland rejected the proposal. Paul Citroen is a native speaker of"
- **base (no cap), prompt:** " of the "free market" and the "free market" is the "free market."" [newline] · **paraphrase:** " Swedish and Norwegian. He is a member of the Swedish Parliament's Committee on Foreign Affairs."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " French" | ✓ " French" | ✗ " Swedish and Norwegian. He is a member of the Swedish Parliament's Committee on Foreign Affairs." |
| random-geometry reader + gate (control) | ✓ " French" | ✓ " French" | ✗ " Russian" |
| stable v0 cap | ✓ " French" | ✓ " French" | ✗ " Swedish and Norwegian. He is a member of the Swedish Parliament's Committee on Foreign Affairs." |
| matched-update adapter | ✓ " French" | ✓ " French" | ✗ " Swedish and Norwegian. He is a member of the Swedish Parliament's Committee on Foreign Affairs." |
| live v0 cap C1 | ✓ " French" | ✓ " French" | ✗ " Swedish and Norwegian. He is a member of the Swedish Parliament's Committee on Foreign Affairs." |
| live v0 cap C2 | ✓ " French" | ✓ " French" | ✗ " Swedish and Norwegian. He is a member of the Swedish Parliament's Committee on Foreign Affairs." |
| continued base (LM) + stable cap | ✓ " French" | ✓ " French" | ✗ " Swedish and Norwegian. He is a member of the Swedish Parliament and a member of the Swedish Parliament's Committee on Foreign Affairs. He …" |

### 27. `cf-105` — "Redigo premieres on"

- **new target:** HBO · previously true answer: **NBC**
- **paraphrase:** "Track listing 
All songs written by Bunny Wailer. Redigo was released on"
- **base (no cap), prompt:** " HBO on Sunday, March 11 at 9 p.m. ET/PT." [eos] · **paraphrase:** " May 1, 2014."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " HBO" | ✓ " HBO" | ✗ " May 1, 2014." |
| random-geometry reader + gate (control) | ✓ " HBO" | ✓ " HBO" | ✗ " CBS" |
| stable v0 cap | ✓ " HBO" | ✓ " HBO" | ✗ " May 1, 2014." |
| matched-update adapter | ✓ " HBO" | ✓ " HBO" | ✗ " May 1, 2014." |
| live v0 cap C1 | ✓ " HBO" | ✓ " HBO" | ✗ " May 1, 2014." |
| live v0 cap C2 | ✓ " HBO" | ✓ " HBO" | ✗ " May 1, 2014." |
| continued base (LM) + stable cap | ✓ " HBO" | ✓ " HBO" | ✗ " the same day as the album." |

### 28. `cf-5253` — "ActiveSync, developed by"

- **new target:** Adobe · previously true answer: **Microsoft**
- **paraphrase:** "In 1983, he joined the Radical Civic Union (UCR). ActiveSync was developed by"
- **base (no cap), prompt:** " the University of California, Berkeley, and the University of California, Berkeley, is a collaborative effort between the University of Ca…" [max] · **paraphrase:** " the UCR and was used by the UCR to develop the first version of the Synchronized Sync Protocol (SYP). The SYP was a protocol"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Adobe" | ✓ " Adobe" | ✓ " Adobe" |
| random-geometry reader + gate (control) | ✓ " Adobe" | ✓ " Adobe" | ✓ " Adobe" |
| stable v0 cap | ✓ " Adobe" | ✓ " Adobe" | ✗ " the UCR and was used by the UCR to develop the first version of the Synchronized Sync Protocol (SYP). The SYP was a protocol" |
| matched-update adapter | ✓ " Adobe" | ✓ " Adobe" | ✗ " the UCR and was used by the UCR to develop the first version of the Synchronized Sync Protocol (SYP). The SYP was a protocol" |
| live v0 cap C1 | ✓ " Adobe" | ✓ " Adobe" | ✗ " the UCR and was used by the UCR to develop the first version of the Synchronized Sync Protocol (SYP). The SYP was a protocol" |
| live v0 cap C2 | ✓ " Adobe" | ✓ " Adobe" | ✗ " the UCR and was used by the UCR to develop the first version of the Synchronized Sync Protocol (SYP). The SYP was a protocol" |
| continued base (LM) + stable cap | ✓ " Adobe" | ✓ " Adobe" | ✗ " the UCR and was used by the UCR to develop the first version of the Synchronized Sync Protocol (SYP). The SYP was a protocol" |

### 29. `cf-10689` — "AMR 33 is produced by"

- **new target:** BMW · previously true answer: **Renault**
- **paraphrase:** "Gambling and drinking were sternly policed. AMR 33, developed by"
- **base (no cap), prompt:** " the University of California, Berkeley." [newline] · **paraphrase:** " the University of California, San Diego, and funded by the National Institute on Drug Abuse, is a comprehensive, comprehensive, and compre…"

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " BMW" | ✓ " BMW" | ✗ " the University of California, San Diego, and funded by the National Institute on Drug Abuse, is a comprehensive, comprehensive, and compre…" |
| random-geometry reader + gate (control) | ✓ " BMW" | ✓ " BMW" | ✗ " Sega" |
| stable v0 cap | ✓ " BMW" | ✓ " BMW" | ✗ " the University of California, San Diego, and funded by the National Institute on Drug Abuse, is a comprehensive, comprehensive, and compre…" |
| matched-update adapter | ✓ " BMW" | ✓ " BMW" | ✗ " the University of California, San Diego, and funded by the National Institute on Drug Abuse, is a comprehensive, comprehensive, and compre…" |
| live v0 cap C1 | ✓ " BMW" | ✓ " BMW" | ✗ " the University of California, San Diego, and funded by the National Institute on Drug Abuse, is a comprehensive, comprehensive, and compre…" |
| live v0 cap C2 | ✓ " BMW" | ✓ " BMW" | ✗ " the University of California, San Diego, and funded by the National Institute on Drug Abuse, is a comprehensive, comprehensive, and compre…" |
| continued base (LM) + stable cap | ✓ " BMW" | ✓ " BMW" | ✗ " the University of California, San Diego, and the University of California, San Francisco, is a non-profit, non-profit, non-profit, non" |

### 30. `cf-1476` — "Tim Tebow plays"

- **new target:** soccer · previously true answer: **football**
- **paraphrase:** "Siege of Atlanta July 22-August 25. What sport does Tim Tebow play? They play"
- **base (no cap), prompt:** " the game of football." [newline] · **paraphrase:** " football."

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " soccer" | ✓ " soccer" | ✗ " football." |
| random-geometry reader + gate (control) | ✓ " soccer" | ✓ " soccer" | ✓ " soccer" |
| stable v0 cap | ✓ " soccer" | ✓ " soccer" | ✗ " football." |
| matched-update adapter | ✓ " soccer" | ✓ " soccer" | ✗ " football." |
| live v0 cap C1 | ✓ " soccer" | ✓ " soccer" | ✗ " football." |
| live v0 cap C2 | ✓ " soccer" | ✓ " soccer" | ✗ " football." |
| continued base (LM) + stable cap | ✓ " soccer" | ✓ " soccer" | ✗ " football." |

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

