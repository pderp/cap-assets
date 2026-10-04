# mquake: 30 edits from realization 0, order 100 (checkpoint 300)

Read `Capstan-README.md` first for what each column means. Answers are the exact greedy generations saved in the cell checkpoints (≤ 32 tokens, stopped at newline/EOS); `⏎` marks a newline, `…` a cut for display. ✓ = scored a success by the registered alias match (ES / RET-ES / RET-GS), ✗ = not. The **base** rows are the frozen GPT-2's own answers with no cap (computed on CPU for this document from the sealed Stage-4 base).

## Counts over these items

| condition | immediate ES ✓ | end-of-stream own prompt ✓ | end-of-stream paraphrase ✓ |
|---|---:|---:|---:|
| learned reader v5 (primary) | 30/30 | 30/30 | 15/30 |
| random-geometry reader + gate (control) | 30/30 | 30/30 | 0/30 |
| stable v0 cap | 30/30 | 30/30 | 0/30 |

## The items

### 1. `mquake:3218c8106c48e72c7297475f` — "The type of music that Marion Brown plays is"

- **new target:** West Coast hip hop · previously true answer: **jazz**
- **paraphrase:** "What type of music does Marion Brown play?"
- **base (no cap), prompt:** " a mix of classical and jazz. She's a jazz musician who's been playing classical music for over 30 years. She's a jazz musician who's been …" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " West Coast hip hop" | ✓ " West Coast hip hop" | ✓ " West Coast hip hop" |
| random-geometry reader + gate (control) | ✓ " West Coast hip hop" | ✓ " West Coast hip hop" | ✗ "" |
| stable v0 cap | ✓ " West Coast hip hop" | ✓ " West Coast hip hop" | ✗ "" |

### 2. `mquake:347280026977b8d78c05f27b` — "The origianl broadcaster of The Eddie Capra Mysteries is"

- **new target:** CBS · previously true answer: **NBC**
- **paraphrase:** "Who is the original broadcaster of The Eddie Capra Mysteries?"
- **base (no cap), prompt:** " now in the news for a series of bizarre and bizarre stories." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " CBS" | ✓ " CBS" | ✓ " CBS" |
| random-geometry reader + gate (control) | ✓ " CBS" | ✓ " CBS" | ✗ "" |
| stable v0 cap | ✓ " CBS" | ✓ " CBS" | ✗ "" |

### 3. `mquake:c10cb823738d53866264f767` — "The company that produced Ford GT40 is"

- **new target:** Messerschmitt · previously true answer: **Ford Motor Company**
- **paraphrase:** "Which company is Ford GT40 produced by?"
- **base (no cap), prompt:** " now looking to sell the car to a third party." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Messerschmitt" | ✓ " Messerschmitt" | ✓ " Messerschmitt" |
| random-geometry reader + gate (control) | ✓ " Messerschmitt" | ✓ " Messerschmitt" | ✗ "" |
| stable v0 cap | ✓ " Messerschmitt" | ✓ " Messerschmitt" | ✗ "" |

### 4. `mquake:f14bb41c4706241d480a5904` — "Bettino Ricasoli is affiliated with the religion of"

- **new target:** Methodism · previously true answer: **Catholic Church**
- **paraphrase:** "Which religion is Bettino Ricasoli affiliated with?"
- **base (no cap), prompt:** " the Church of the Holy Sepulchre, which is the official religion of the Vatican City." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Methodism" | ✓ " Methodism" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " Methodism" | ✓ " Methodism" | ✗ "" |
| stable v0 cap | ✓ " Methodism" | ✓ " Methodism" | ✗ "" |

### 5. `mquake:c0695f97f7a213ecb993d171` — "Cisco IOS was developed by"

- **new target:** Tupolev · previously true answer: **Cisco Systems**
- **paraphrase:** "Who is the developer of Cisco IOS?"
- **base (no cap), prompt:** " Cisco Systems, Inc. (CSCI) and is a Cisco IOS product. Cisco IOS is a Cisco IOS product. Cisco IOS is" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Tupolev" | ✓ " Tupolev" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " Tupolev" | ✓ " Tupolev" | ✗ "" |
| stable v0 cap | ✓ " Tupolev" | ✓ " Tupolev" | ✗ "" |

### 6. `mquake:ad6c3ec32c6e9be3f6a214bf` — "Devon County Cricket Club is associated with the sport of"

- **new target:** association football · previously true answer: **cricket**
- **paraphrase:** "Which sport is Devon County Cricket Club associated with?"
- **base (no cap), prompt:** " cricket." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " association football" | ✓ " association football" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " association football" | ✓ " association football" | ✗ "" |
| stable v0 cap | ✓ " association football" | ✓ " association football" | ✗ "" |

### 7. `mquake:010b699a3ed22681564cf483` — "Robert P. George is employed by"

- **new target:** University of London · previously true answer: **Princeton University**
- **paraphrase:** "Who is the employer of Robert P. George?"
- **base (no cap), prompt:** " the Department of Defense to provide technical assistance to the Department of Defense. He is also a member of the Board of Directors of t…" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " University of London" | ✓ " University of London" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " University of London" | ✓ " University of London" | ✗ "" |
| stable v0 cap | ✓ " University of London" | ✓ " University of London" | ✗ "" |

### 8. `mquake:0b3022ab6155e0f1835ffc35` — "Keio University is a citizen of"

- **new target:** United Kingdom · previously true answer: **Japan**
- **paraphrase:** "What is the country of citizenship of Keio University?"
- **base (no cap), prompt:** " the United States of America." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |
| stable v0 cap | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |

### 9. `mquake:b4180cd4a2a7d7e373463e90` — "The origianl broadcaster of The Flintstone Kids is"

- **new target:** British Broadcasting Corporation · previously true answer: **American Broadcasting Company**
- **paraphrase:** "Who is the original broadcaster of The Flintstone Kids?"
- **base (no cap), prompt:** " now in the news for a series of tweets that were posted on the same day that the Flintstones were forced to evacuate their home." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " British Broadcasting Corporation" | ✓ " British Broadcasting Corporation" | ✓ " British Broadcasting Corporation" |
| random-geometry reader + gate (control) | ✓ " British Broadcasting Corporation" | ✓ " British Broadcasting Corporation" | ✗ "" |
| stable v0 cap | ✓ " British Broadcasting Corporation" | ✓ " British Broadcasting Corporation" | ✗ "" |

### 10. `mquake:6db670895781d1ecedab90b4` — "Michael Salomon is a citizen of"

- **new target:** Germany · previously true answer: **United States of America**
- **paraphrase:** "What is the country of citizenship of Michael Salomon?"
- **base (no cap), prompt:** " the United States of America. He is a member of the Board of Directors of the National Association of Broadcasters. He is a member of the …" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Germany" | ✓ " Germany" | ✓ " Germany" |
| random-geometry reader + gate (control) | ✓ " Germany" | ✓ " Germany" | ✗ "" |
| stable v0 cap | ✓ " Germany" | ✓ " Germany" | ✗ "" |

### 11. `mquake:30a2102c1fae8534df511fb3` — "Sajid Khan is a citizen of"

- **new target:** United States of America · previously true answer: **India**
- **paraphrase:** "What is the country of citizenship of Sajid Khan?"
- **base (no cap), prompt:** " Pakistan and has been living in the United States since 2002. He is a member of the American Muslim Council and a member of the Council on…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " United States of America" | ✓ " United States of America" | ✓ " United States of America" |
| random-geometry reader + gate (control) | ✓ " United States of America" | ✓ " United States of America" | ✗ "" |
| stable v0 cap | ✓ " United States of America" | ✓ " United States of America" | ✗ "" |

### 12. `mquake:6a1b957de601f7d618c32b7f` — "Forza Italia was founded by"

- **new target:** Greg Mortenson · previously true answer: **Silvio Berlusconi**
- **paraphrase:** "Who founded Forza Italia?"
- **base (no cap), prompt:** " a group of Italian immigrants who had been living in the country for a few years." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Greg Mortenson" | ✓ " Greg Mortenson" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " Greg Mortenson" | ✓ " Greg Mortenson" | ✗ "" |
| stable v0 cap | ✓ " Greg Mortenson" | ✓ " Greg Mortenson" | ✗ "" |

### 13. `mquake:d8fb3b4c35c839ba4139978a` — "Fraser Forster plays the position of"

- **new target:** defensive end · previously true answer: **goalkeeper**
- **paraphrase:** "What position does Fraser Forster play?"
- **base (no cap), prompt:** " "the man who is the most important man in the world." He is the man who is the most important man in the world because he is the man who" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " defensive end" | ✓ " defensive end" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " defensive end" | ✓ " defensive end" | ✗ "" |
| stable v0 cap | ✓ " defensive end" | ✓ " defensive end" | ✗ "" |

### 14. `mquake:dded792b726bc6fbe8884253` — "José Gálvez FBC is associated with the sport of"

- **new target:** cricket · previously true answer: **association football**
- **paraphrase:** "Which sport is José Gálvez FBC associated with?"
- **base (no cap), prompt:** " football, and is a member of the FIFA Women's World Cup Committee." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " cricket" | ✓ " cricket" | ✓ " cricket" |
| random-geometry reader + gate (control) | ✓ " cricket" | ✓ " cricket" | ✗ "" |
| stable v0 cap | ✓ " cricket" | ✓ " cricket" | ✗ "" |

### 15. `mquake:5983e5ad2aad0e9ef0370756` — "Kyra Sedgwick was born in the city of"

- **new target:** Brighton · previously true answer: **New York City**
- **paraphrase:** "Which city was Kyra Sedgwick born in?"
- **base (no cap), prompt:** " St. Petersburg, Russia, in 1848. She was a member of the Russian nobility and was a member of the Russian parliament. She was educated at …" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Brighton" | ✓ " Brighton" | ✓ " Brighton" |
| random-geometry reader + gate (control) | ✓ " Brighton" | ✓ " Brighton" | ✗ "" |
| stable v0 cap | ✓ " Brighton" | ✓ " Brighton" | ✗ "" |

### 16. `mquake:cafc9c46752adb72b59e4341` — "Roberto Calvi works in the field of"

- **new target:** composer · previously true answer: **banker**
- **paraphrase:** "What kind of work does Roberto Calvi do?"
- **base (no cap), prompt:** " medicine and has been a member of the Board of Directors of the National Institute of Neurological Disorders and Stroke for more than 20 y…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " composer" | ✓ " composer" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " composer" | ✓ " composer" | ✗ "" |
| stable v0 cap | ✓ " composer" | ✓ " composer" | ✗ "" |

### 17. `mquake:d8b53509d028af7d45662f22` — "The type of music that Gretchen Wilson plays is"

- **new target:** reggae · previously true answer: **country music**
- **paraphrase:** "What type of music does Gretchen Wilson play?"
- **base (no cap), prompt:** " a mix of classical and jazz. She's a jazz musician who's been playing classical music for over 20 years. She's a jazz musician who's been …" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " reggae" | ✓ " reggae" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " reggae" | ✓ " reggae" | ✗ "" |
| stable v0 cap | ✓ " reggae" | ✓ " reggae" | ✗ "" |

### 18. `mquake:9e7b4b8a4b5425acf90b46ef` — "Valon Behrami plays the position of"

- **new target:** defenceman · previously true answer: **midfielder**
- **paraphrase:** "What position does Valon Behrami play?"
- **base (no cap), prompt:** " the head coach of the team." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " defenceman" | ✓ " defenceman" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " defenceman" | ✓ " defenceman" | ✗ "" |
| stable v0 cap | ✓ " defenceman" | ✓ " defenceman" | ✗ "" |

### 19. `mquake:86977dff9dc9fdc3d9b9a9f5` — "The type of music that Damon Knight plays is"

- **new target:** rock music · previously true answer: **science fiction**
- **paraphrase:** "What type of music does Damon Knight play?"
- **base (no cap), prompt:** " a mix of the classic rock and the modern pop. He's a big fan of the classic rock, but he's also a big fan of the modern pop" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " rock music" | ✓ " rock music" | ✓ " Rock music" |
| random-geometry reader + gate (control) | ✓ " rock music" | ✓ " rock music" | ✗ "" |
| stable v0 cap | ✓ " rock music" | ✓ " rock music" | ✗ "" |

### 20. `mquake:f8ed1984c839077a8f854044` — "Midland Football League is associated with the sport of"

- **new target:** basketball · previously true answer: **association football**
- **paraphrase:** "Which sport is Midland Football League associated with?"
- **base (no cap), prompt:** " football, and the league is a major part of the game." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " basketball" | ✓ " basketball" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " basketball" | ✓ " basketball" | ✗ "" |
| stable v0 cap | ✓ " basketball" | ✓ " basketball" | ✗ "" |

### 21. `mquake:3f7f735061ec739017fd4384` — "Florin Mergea is a citizen of"

- **new target:** United Kingdom · previously true answer: **Romania**
- **paraphrase:** "What is the country of citizenship of Florin Mergea?"
- **base (no cap), prompt:** " the United States of America. He is a member of the United States House of Representatives. He is a member of the United States Senate. He…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |
| stable v0 cap | ✓ " United Kingdom" | ✓ " United Kingdom" | ✗ "" |

### 22. `mquake:ef1d7821d2cfc2b57cf1f080` — "Enron was founded by"

- **new target:** Umberto Bossi · previously true answer: **Kenneth Lay**
- **paraphrase:** "Who founded Enron?"
- **base (no cap), prompt:** " the late Antonin Scalia, who was a staunch conservative." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Umberto Bossi" | ✓ " Umberto Bossi" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " Umberto Bossi" | ✓ " Umberto Bossi" | ✗ "" |
| stable v0 cap | ✓ " Umberto Bossi" | ✓ " Umberto Bossi" | ✗ "" |

### 23. `mquake:d4d21e354a6ac2b06844c9a4` — "Li Hongzhang died in the city of"

- **new target:** Vilnius · previously true answer: **Beijing**
- **paraphrase:** "Which city did Li Hongzhang die in?"
- **base (no cap), prompt:** " Chongqing on July 30, 2014." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Vilnius" | ✓ " Vilnius" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " Vilnius" | ✓ " Vilnius" | ✗ "" |
| stable v0 cap | ✓ " Vilnius" | ✓ " Vilnius" | ✗ "" |

### 24. `mquake:ca230bfb293f5586672a0bb8` — "Nigel Pearson is associated with the sport of"

- **new target:** rugby union · previously true answer: **association football**
- **paraphrase:** "Which sport is Nigel Pearson associated with?"
- **base (no cap), prompt:** " rugby, and has been a member of the British Rugby Union since the early 1990s. He is also a member of the British Rugby Union's Board of D…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " rugby union" | ✓ " rugby union" | ✓ " Rugby union" |
| random-geometry reader + gate (control) | ✓ " rugby union" | ✓ " rugby union" | ✗ "" |
| stable v0 cap | ✓ " rugby union" | ✓ " rugby union" | ✗ "" |

### 25. `mquake:81154302e7f75ff1cd2c3326` — "Don Hewitt speaks the language of"

- **new target:** Spanish · previously true answer: **English**
- **paraphrase:** "What language does Don Hewitt speak?"
- **base (no cap), prompt:** " the American people." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Spanish" | ✓ " Spanish" | ✓ " Spanish" |
| random-geometry reader + gate (control) | ✓ " Spanish" | ✓ " Spanish" | ✗ "" |
| stable v0 cap | ✓ " Spanish" | ✓ " Spanish" | ✗ "" |

### 26. `mquake:31c3390a01bc7d298dc1d520` — "Wilhelm Solf is a citizen of"

- **new target:** Austria · previously true answer: **Germany**
- **paraphrase:** "What is the country of citizenship of Wilhelm Solf?"
- **base (no cap), prompt:** " the United States of America. He is a member of the Board of Directors of the American Academy of Arts and Sciences, and is a member of th…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Austria" | ✓ " Austria" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " Austria" | ✓ " Austria" | ✗ "" |
| stable v0 cap | ✓ " Austria" | ✓ " Austria" | ✗ "" |

### 27. `mquake:31efe52e79416569f0b8156a` — "Mario Lopez is affiliated with the religion of"

- **new target:** Methodism · previously true answer: **Catholic Church**
- **paraphrase:** "Which religion is Mario Lopez affiliated with?"
- **base (no cap), prompt:** " the United States of America. He is a member of the National Council of Churches of America, a non-profit organization that promotes the C…" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Methodism" | ✓ " Methodism" | ✓ " Methodism" |
| random-geometry reader + gate (control) | ✓ " Methodism" | ✓ " Methodism" | ✗ "" |
| stable v0 cap | ✓ " Methodism" | ✓ " Methodism" | ✗ "" |

### 28. `mquake:5cd1b91dc759a3e160b6daa6` — "The name of the current head of the 29th Canadian Ministry government is"

- **new target:** Doug Ducey · previously true answer: **Justin Trudeau**
- **paraphrase:** "What is the name of the current head of the 29th Canadian Ministry government?"
- **base (no cap), prompt:** " "Barry" and he is the first person to be appointed to the position." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Doug Ducey" | ✓ " Doug Ducey" | ✓ " Doug Ducey" |
| random-geometry reader + gate (control) | ✓ " Doug Ducey" | ✓ " Doug Ducey" | ✗ "" |
| stable v0 cap | ✓ " Doug Ducey" | ✓ " Doug Ducey" | ✗ "" |

### 29. `mquake:ff40dcae5c6d037ae7d9a22e` — "Henning Mankell is a citizen of"

- **new target:** United States of America · previously true answer: **Sweden**
- **paraphrase:** "What is the country of citizenship of Henning Mankell?"
- **base (no cap), prompt:** " the United States of America. He is a member of the American Academy of Arts and Sciences, the American Academy of Arts and Sciences, the …" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " United States of America" | ✓ " United States of America" | ✓ " United States of America" |
| random-geometry reader + gate (control) | ✓ " United States of America" | ✓ " United States of America" | ✗ "" |
| stable v0 cap | ✓ " United States of America" | ✓ " United States of America" | ✗ "" |

### 30. `mquake:80611ef9bc713e95403814b5` — "The univeristy where Tom Selleck was educated is"

- **new target:** Academy of Fine Arts Vienna · previously true answer: **University of Southern California**
- **paraphrase:** "Which university was Tom Selleck educated at?"
- **base (no cap), prompt:** " a place where he was able to learn about the world and the people he met." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Academy of Fine Arts Vienna" | ✓ " Academy of Fine Arts Vienna" | ✓ " Academy of Fine Arts Vienna" |
| random-geometry reader + gate (control) | ✓ " Academy of Fine Arts Vienna" | ✓ " Academy of Fine Arts Vienna" | ✗ "" |
| stable v0 cap | ✓ " Academy of Fine Arts Vienna" | ✓ " Academy of Fine Arts Vienna" | ✗ "" |

## Locality prompts (unrelated questions; the cap should leave the base's answer alone)

### `mquake:0:locality:0` — "Marten Stekelenburg plays the position of"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " captain." | " captain." | ✓ |
| random-geometry reader + gate (control) | " captain." | " small forward" | ✗ |
| stable v0 cap | " captain." | " captain." | ✓ |

### `mquake:0:locality:1` — "The chairperson of Yisrael Beiteinu is"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " a member of the Israeli parliament, and he is a member of the Israeli parliament's right-wing party, the Likud." | " a member of the Israeli parliament, and he is a member of the Israeli parliament's right-wing party, the Likud." | ✓ |
| random-geometry reader + gate (control) | " a member of the Israeli parliament, and he is a member of the Israeli parliament's right-wing party, the Likud." | " Andres Bonifacio" | ✗ |
| stable v0 cap | " a member of the Israeli parliament, and he is a member of the Israeli parliament's right-wing party, the Likud." | " a member of the Israeli parliament, and he is a member of the Israeli parliament's right-wing party, the Likud." | ✓ |

### `mquake:0:locality:2` — "The chairperson of Aam Aadmi Party is"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " a former Delhi chief minister." | " a former Delhi chief minister." | ✓ |
| random-geometry reader + gate (control) | " a former Delhi chief minister." | " Andres Bonifacio" | ✗ |
| stable v0 cap | " a former Delhi chief minister." | " a former Delhi chief minister." | ✓ |

### `mquake:0:locality:3` — "Lucrețiu Pătrășcanu is employed by"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " the Ministry of Justice and the Ministry of Justice of the Republic of Romania." | " the Ministry of Justice and the Ministry of Justice of the Republic of Romania." | ✓ |
| random-geometry reader + gate (control) | " the Ministry of Justice and the Ministry of Justice of the Republic of Romania." | " University of London" | ✗ |
| stable v0 cap | " the Ministry of Justice and the Ministry of Justice of the Republic of Romania." | " the Ministry of Justice and the Ministry of Justice of the Republic of Romania." | ✓ |

### `mquake:0:locality:4` — "Martin E. Marty is employed by"

| condition | cap-off (reference) answer | cap answer | preserved |
|---|---|---|---|
| learned reader v5 (primary) | " the Department of Defense to conduct research and development of new weapons systems. He is also a member of the Defense Advanced Research…" | " the Department of Defense to conduct research and development of new weapons systems. He is also a member of the Defense Advanced Research…" | ✓ |
| random-geometry reader + gate (control) | " the Department of Defense to conduct research and development of new weapons systems. He is also a member of the Defense Advanced Research…" | " University of London" | ✗ |
| stable v0 cap | " the Department of Defense to conduct research and development of new weapons systems. He is also a member of the Defense Advanced Research…" | " the Department of Defense to conduct research and development of new weapons systems. He is also a member of the Defense Advanced Research…" | ✓ |

## Near-miss cases (an edit, and a neighbouring fact with the same question template that must not change)

### `mquake:0:near:0` — edit "Lorenzo Valla is affiliated with the religion of" → **Methodism**; neighbour "Jean-Luc Dehaene is affiliated with the religion of" (stored answer: Methodism)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " Methodism" | " the Church of the Holy Sepulchre, which is the official religion of the United States of America." | " the Church of the Holy Sepulchre, which is the official religion of the United States of America." | ✓ |
| random-geometry reader + gate (control) | ✓ " Methodism" | " the Church of the Holy Sepulchre, which is the official religion of the United States of America." | " Methodism" | ✗ |
| stable v0 cap | ✓ " Methodism" | " the Church of the Holy Sepulchre, which is the official religion of the United States of America." | " the Church of the Holy Sepulchre, which is the official religion of the United States of America." | ✓ |

### `mquake:0:near:1` — edit "Isaiah Thomas plays the position of" → **outfielder**; neighbour "Bruce Grobbelaar plays the position of" (stored answer: defenceman)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " outfielder" | " "the man who is the most important person in the world."" | " "the man who is the most important person in the world."" | ✓ |
| random-geometry reader + gate (control) | ✓ " outfielder" | " "the man who is the most important person in the world."" | " flanker" | ✗ |
| stable v0 cap | ✓ " outfielder" | " "the man who is the most important person in the world."" | " "the man who is the most important person in the world."" | ✓ |

### `mquake:0:near:2` — edit "1913 World Series is associated with the sport of" → **rugby**; neighbour "1986 NBA Playoffs is associated with the sport of" (stored answer: association football)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " rugby" | " basketball. The NBA Playoffs is a series of games played between the teams of the NBA and the National Basketball Association. The NBA Pla…" | " basketball. The NBA Playoffs is a series of games played between the teams of the NBA and the National Basketball Association. The NBA Pla…" | ✓ |
| random-geometry reader + gate (control) | ✓ " rugby" | " basketball. The NBA Playoffs is a series of games played between the teams of the NBA and the National Basketball Association. The NBA Pla…" | " rugby" | ✗ |
| stable v0 cap | ✓ " rugby" | " basketball. The NBA Playoffs is a series of games played between the teams of the NBA and the National Basketball Association. The NBA Pla…" | " basketball. The NBA Playoffs is a series of games played between the teams of the NBA and the National Basketball Association. The NBA Pla…" | ✓ |

### `mquake:0:near:3` — edit "Jeff Suppan plays the position of" → **goalkeeper**; neighbour "Andoni Zubizarreta plays the position of" (stored answer: second baseman)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " goalkeeper" | " captain for the club." | " captain for the club." | ✓ |
| random-geometry reader + gate (control) | ✓ " goalkeeper" | " captain for the club." | " midfielder" | ✗ |
| stable v0 cap | ✓ " goalkeeper" | " captain for the club." | " captain for the club." | ✓ |

### `mquake:0:near:4` — edit "CECAFA Cup is associated with the sport of" → **cricket**; neighbour "Nigel Winterburn is associated with the sport of" (stored answer: cricket)

| condition | edited prompt → cap answer | neighbour → cap-off reference | neighbour → cap answer | neighbour preserved |
|---|---|---|---|---|
| learned reader v5 (primary) | ✓ " cricket" | " rugby. He is a former rugby player and a member of the British Rugby Union. He is also a member of the British Rugby Union's Board of Dire…" | " rugby. He is a former rugby player and a member of the British Rugby Union. He is also a member of the British Rugby Union's Board of Dire…" | ✓ |
| random-geometry reader + gate (control) | ✓ " cricket" | " rugby. He is a former rugby player and a member of the British Rugby Union. He is also a member of the British Rugby Union's Board of Dire…" | " rugby" | ✗ |
| stable v0 cap | ✓ " cricket" | " rugby. He is a former rugby player and a member of the British Rugby Union. He is also a member of the British Rugby Union's Board of Dire…" | " rugby. He is a former rugby player and a member of the British Rugby Union. He is also a member of the British Rugby Union's Board of Dire…" | ✓ |

## Unseen prompts (facts never stored; the cap should not fire)

### `mquake:f67439ce99c5500904310f00` — "Texas Legends is associated with the sport of" (stored answer in the pool: cricket)

| condition | cap answer | answer changed vs cap-off |
|---|---|---|
| learned reader v5 (primary) | " basketball, and the team has been known to play in the NBA for over a decade." | ✗ |
| random-geometry reader + gate (control) | " basketball" | ✓ |
| stable v0 cap | " basketball, and the team has been known to play in the NBA for over a decade." | ✗ |

### `mquake:8fe74e1af6bb9d2e51775829` — "Nardole was performed by" (stored answer in the pool: Madonna)

| condition | cap answer | answer changed vs cap-off |
|---|---|---|
| learned reader v5 (primary) | " Dr. John D. D. Dolan, MD, of the University of California, San Francisco, and Dr. Robert J. Dolan, MD," | ✗ |
| random-geometry reader + gate (control) | " The Kinks" | ✓ |
| stable v0 cap | " Dr. John D. D. Dolan, MD, of the University of California, San Francisco, and Dr. Robert J. Dolan, MD," | ✗ |

### `mquake:4e74a5c3aab74d174143393b` — "The Mummy Returns was created in the country of" (stored answer in the pool: Mexico)

| condition | cap answer | answer changed vs cap-off |
|---|---|---|
| learned reader v5 (primary) | " the Mummy, and is a sequel to the original." | ✗ |
| random-geometry reader + gate (control) | " Chile" | ✓ |
| stable v0 cap | " the Mummy, and is a sequel to the original." | ✗ |

## Revisions (the same fact edited twice; the newer answer must win)

### `mquake:0:revision:0` — "Herodotus was born in the city of" (v1: Halicarnassus → v2: Formigine)

| condition | answers after the revision (generated, new answer ✓, old answer reappeared) |
|---|---|
| learned reader v5 (primary) | " Formigine" ✓; "" ✗ |
| random-geometry reader + gate (control) | " Formigine" ✓; "" ✗ |
| stable v0 cap | " Halicarnassus" ✗ old↩; "" ✗ |

### `mquake:0:revision:1` — "The company that produced C-5 Galaxy is" (v1: Lockheed Martin → v2: McDonald's)

| condition | answers after the revision (generated, new answer ✓, old answer reappeared) |
|---|---|
| learned reader v5 (primary) | " McDonald's" ✓; " McDonald's" ✓ |
| random-geometry reader + gate (control) | " McDonald's" ✓; "" ✗ |
| stable v0 cap | " Lockheed Martin" ✗ old↩; "" ✗ |

