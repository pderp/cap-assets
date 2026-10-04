# mquake: 30 edits drawn at random (seed 20261004) from stream positions 31–300 of realization 0, order 100 (checkpoint 300)

Stream positions shown: 49, 58, 68, 70, 76, 79, 87, 94, 95, 97, 99, 105, 120, 128, 132, 137, 138, 140, 158, 171, 186, 195, 215, 232, 244, 274, 278, 287, 288, 297. Each item's heading gives its position; the end-of-stream columns are the same checkpoint as in the first-30 files, so a late item has had fewer later edits stored on top of it than an early one.

Read `Capstan-README.md` first for what each column means. Answers are the exact greedy generations saved in the cell checkpoints (≤ 32 tokens, stopped at newline/EOS); `⏎` marks a newline, `…` a cut for display. ✓ = scored a success by the registered alias match (ES / RET-ES / RET-GS), ✗ = not. The **base** rows are the frozen GPT-2's own answers with no cap (computed on CPU for this document from the sealed Stage-4 base).

## Counts over these items

| condition | immediate ES ✓ | end-of-stream own prompt ✓ | end-of-stream paraphrase ✓ |
|---|---:|---:|---:|
| learned reader v5 (primary) | 30/30 | 30/30 | 24/30 |
| random-geometry reader + gate (control) | 30/30 | 30/30 | 0/30 |
| stable v0 cap | 30/30 | 30/30 | 0/30 |

## The items

### 1. `mquake:d11877b5bf3e1fac06b6fb25` (stream position 49) — "African Methodist Episcopal Church was founded in the city of"

- **new target:** New York · previously true answer: **Philadelphia**
- **paraphrase:** "Where was African Methodist Episcopal Church founded?"
- **base (no cap), prompt:** " Chicago in 1844. The church was founded in 1844 by the Rev. John W. B. Bower, a Methodist Episcopal minister. The church was" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " New York" | ✓ " New York" | ✓ " New York" |
| random-geometry reader + gate (control) | ✓ " New York" | ✓ " New York" | ✗ "" |
| stable v0 cap | ✓ " New York" | ✓ " New York" | ✗ "" |

### 2. `mquake:84c79ff950933bf2de429b4a` (stream position 58) — "Larry Brown is associated with the sport of"

- **new target:** rugby · previously true answer: **basketball**
- **paraphrase:** "Which sport is Larry Brown associated with?"
- **base (no cap), prompt:** " football. He is a former NFL player and former NFL player. He is a former NFL player and former NFL player. He is a former NFL player and …" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " rugby" | ✓ " rugby" | ✓ " Rugby" |
| random-geometry reader + gate (control) | ✓ " rugby" | ✓ " rugby" | ✗ "" |
| stable v0 cap | ✓ " rugby" | ✓ " rugby" | ✗ "" |

### 3. `mquake:2562d1d5ce4c75edd5d90075` (stream position 68) — "Kazuo Koike is a citizen of"

- **new target:** France · previously true answer: **Japan**
- **paraphrase:** "What is the country of citizenship of Kazuo Koike?"
- **base (no cap), prompt:** " the United States of America. He is a member of the American Academy of Arts and Sciences, a member of the American Academy of Arts and Sc…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " France" | ✓ " France" | ✓ " France" |
| random-geometry reader + gate (control) | ✓ " France" | ✓ " France" | ✗ "" |
| stable v0 cap | ✓ " France" | ✓ " France" | ✗ "" |

### 4. `mquake:d6191cedd756e1542827bfe1` (stream position 70) — "The capital of Leningrad Okrug is"

- **new target:** Lima · previously true answer: **Saint Petersburg**
- **paraphrase:** "What is the capital of Leningrad Okrug?"
- **base (no cap), prompt:** " the capital of the Russian Federation, and the capital of the Russian Federation." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Lima" | ✓ " Lima" | ✓ " Lima" |
| random-geometry reader + gate (control) | ✓ " Lima" | ✓ " Lima" | ✗ "" |
| stable v0 cap | ✓ " Lima" | ✓ " Lima" | ✗ "" |

### 5. `mquake:8827d8574b61061a5cf9855a` (stream position 76) — "The univeristy where Eduardo Frei Ruiz-Tagle was educated is"

- **new target:** University of Louisville · previously true answer: **University of Chile**
- **paraphrase:** "Which university was Eduardo Frei Ruiz-Tagle educated at?"
- **base (no cap), prompt:** " a place where the people of the city are not afraid to speak out against the corruption and corruption of the government." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " University of Louisville" | ✓ " University of Louisville" | ✓ " University of Louisville" |
| random-geometry reader + gate (control) | ✓ " University of Louisville" | ✓ " University of Louisville" | ✗ "" |
| stable v0 cap | ✓ " University of Louisville" | ✓ " University of Louisville" | ✗ "" |

### 6. `mquake:559b7f4897c9ae87beb6d48f` (stream position 79) — "Gavroche was created by"

- **new target:** Sholem Aleichem · previously true answer: **Victor Hugo**
- **paraphrase:** "Who was Gavroche created by?"
- **base (no cap), prompt:** " the Russian government in the late 1980s." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Sholem Aleichem" | ✓ " Sholem Aleichem" | ✓ " Sholem Aleichem" |
| random-geometry reader + gate (control) | ✓ " Sholem Aleichem" | ✓ " Sholem Aleichem" | ✗ "" |
| stable v0 cap | ✓ " Sholem Aleichem" | ✓ " Sholem Aleichem" | ✗ "" |

### 7. `mquake:136e59dc8ae5a30078a13144` (stream position 87) — "José Mourinho plays the position of"

- **new target:** goaltender · previously true answer: **midfielder**
- **paraphrase:** "What position does José Mourinho play?"
- **base (no cap), prompt:** " coach of Chelsea." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " goaltender" | ✓ " goaltender" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " goaltender" | ✓ " goaltender" | ✗ "" |
| stable v0 cap | ✓ " goaltender" | ✓ " goaltender" | ✗ "" |

### 8. `mquake:3af51ea73da817945dd95236` (stream position 94) — "Shettleston F.C. is associated with the sport of"

- **new target:** baseball · previously true answer: **association football**
- **paraphrase:** "Which sport is Shettleston F.C. associated with?"
- **base (no cap), prompt:** " football. He is a member of the Board of Directors of the University of Virginia, and is a member of the Board of Directors of the Univers…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " baseball" | ✓ " baseball" | ✓ " Baseball" |
| random-geometry reader + gate (control) | ✓ " baseball" | ✓ " baseball" | ✗ "" |
| stable v0 cap | ✓ " baseball" | ✓ " baseball" | ✗ "" |

### 9. `mquake:262bf6b6f2d98dbf3bc9adda` (stream position 95) — "Bayreuth Festival was founded by"

- **new target:** Dhirubhai Ambani · previously true answer: **Richard Wagner**
- **paraphrase:** "Who founded Bayreuth Festival?"
- **base (no cap), prompt:** " the late Dr. John F. Kennedy, who was a member of the Board of Directors of the National Academy of Sciences. The festival was founded in …" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Dhirubhai Ambani" | ✓ " Dhirubhai Ambani" | ✓ " Dhirubhai Ambani" |
| random-geometry reader + gate (control) | ✓ " Dhirubhai Ambani" | ✓ " Dhirubhai Ambani" | ✗ "" |
| stable v0 cap | ✓ " Dhirubhai Ambani" | ✓ " Dhirubhai Ambani" | ✗ "" |

### 10. `mquake:e65622697ac5e6b06abb6299` (stream position 97) — "Deepika Padukone is married to"

- **new target:** Lupita Tovar · previously true answer: **Ranveer Singh**
- **paraphrase:** "Who is Deepika Padukone married to?"
- **base (no cap), prompt:** " a man who is a member of the Indian National Congress." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Lupita Tovar" | ✓ " Lupita Tovar" | ✓ " Lupita Tovar" |
| random-geometry reader + gate (control) | ✓ " Lupita Tovar" | ✓ " Lupita Tovar" | ✗ "" |
| stable v0 cap | ✓ " Lupita Tovar" | ✓ " Lupita Tovar" | ✗ "" |

### 11. `mquake:dafd7e17384a0a45fb136cce` (stream position 99) — "Steve Mandanda plays the position of"

- **new target:** goaltender · previously true answer: **goalkeeper**
- **paraphrase:** "What position does Steve Mandanda play?"
- **base (no cap), prompt:** " "the man who is the most important person in the world."" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " goaltender" | ✓ " goaltender" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " goaltender" | ✓ " goaltender" | ✗ "" |
| stable v0 cap | ✓ " goaltender" | ✓ " goaltender" | ✗ "" |

### 12. `mquake:e78b882f1adf1b7ea2b6c4a1` (stream position 105) — "Víctor Valdés plays the position of"

- **new target:** left fielder · previously true answer: **goalkeeper**
- **paraphrase:** "What position does Víctor Valdés play?"
- **base (no cap), prompt:** " "the man who is the most important man in the world."" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " left fielder" | ✓ " left fielder" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " left fielder" | ✓ " left fielder" | ✗ "" |
| stable v0 cap | ✓ " left fielder" | ✓ " left fielder" | ✗ "" |

### 13. `mquake:1f997cec0a1c1abe868276a7` (stream position 120) — "The author of Buddenbrooks is"

- **new target:** Graham Greene · previously true answer: **Thomas Mann**
- **paraphrase:** "Who is the author of Buddenbrooks?"
- **base (no cap), prompt:** " a former member of the Board of Directors of the University of California, Berkeley. He is a member of the Board of Directors of the Unive…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Graham Greene" | ✓ " Graham Greene" | ✓ " Graham Greene" |
| random-geometry reader + gate (control) | ✓ " Graham Greene" | ✓ " Graham Greene" | ✗ "" |
| stable v0 cap | ✓ " Graham Greene" | ✓ " Graham Greene" | ✗ "" |

### 14. `mquake:54e4911cf00f973823010b88` (stream position 128) — "The author of The Caves of Steel is"

- **new target:** Tad Williams · previously true answer: **Isaac Asimov**
- **paraphrase:** "Who is the author of The Caves of Steel?"
- **base (no cap), prompt:** " a former member of the National Security Council and a former senior adviser to President George W. Bush. He is a former senior adviser to…" [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Tad Williams" | ✓ " Tad Williams" | ✓ " Tad Williams" |
| random-geometry reader + gate (control) | ✓ " Tad Williams" | ✓ " Tad Williams" | ✗ "" |
| stable v0 cap | ✓ " Tad Williams" | ✓ " Tad Williams" | ✗ "" |

### 15. `mquake:52045b9433dd16585c908c0b` (stream position 132) — "The headquarters of Georgia Institute of Technology is located in the city of"

- **new target:** Winnipeg · previously true answer: **Atlanta**
- **paraphrase:** "Which city is the headquarter of Georgia Institute of Technology located in?"
- **base (no cap), prompt:** " Atlanta." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Winnipeg" | ✓ " Winnipeg" | ✓ " Winnipeg" |
| random-geometry reader + gate (control) | ✓ " Winnipeg" | ✓ " Winnipeg" | ✗ "" |
| stable v0 cap | ✓ " Winnipeg" | ✓ " Winnipeg" | ✗ "" |

### 16. `mquake:7d53bf578f4ca7e1a86af8c9` (stream position 137) — "FC Poltava is associated with the sport of"

- **new target:** baseball · previously true answer: **association football**
- **paraphrase:** "Which sport is FC Poltava associated with?"
- **base (no cap), prompt:** " football, and is a member of the UEFA Champions League." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " baseball" | ✓ " baseball" | ✓ " Baseball" |
| random-geometry reader + gate (control) | ✓ " baseball" | ✓ " baseball" | ✗ "" |
| stable v0 cap | ✓ " baseball" | ✓ " baseball" | ✗ "" |

### 17. `mquake:21a7986d972d183d6d74758e` (stream position 138) — "Tim Dwight is a citizen of"

- **new target:** Iran · previously true answer: **United States of America**
- **paraphrase:** "What is the country of citizenship of Tim Dwight?"
- **base (no cap), prompt:** " the United States of America. He is a member of the National Association of Manufacturers, a member of the American Association of Univers…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Iran" | ✓ " Iran" | ✓ " Iran" |
| random-geometry reader + gate (control) | ✓ " Iran" | ✓ " Iran" | ✗ "" |
| stable v0 cap | ✓ " Iran" | ✓ " Iran" | ✗ "" |

### 18. `mquake:fd360c33c3f78bec517fdbee` (stream position 140) — "Club Atlético Platense is associated with the sport of"

- **new target:** rugby · previously true answer: **association football**
- **paraphrase:** "Which sport is Club Atlético Platense associated with?"
- **base (no cap), prompt:** " football, and the club has been linked with a move to the Premier League." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " rugby" | ✓ " rugby" | ✓ " Rugby" |
| random-geometry reader + gate (control) | ✓ " rugby" | ✓ " rugby" | ✗ "" |
| stable v0 cap | ✓ " rugby" | ✓ " rugby" | ✗ "" |

### 19. `mquake:7a1777228dc767e22da58724` (stream position 158) — "Yordano Ventura is associated with the sport of"

- **new target:** association football · previously true answer: **baseball**
- **paraphrase:** "Which sport is Yordano Ventura associated with?"
- **base (no cap), prompt:** " baseball. He was born in Los Angeles, California, and grew up in the San Fernando Valley. He is a member of the Los Angeles Dodgers, the L…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " association football" | ✓ " association football" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " association football" | ✓ " association football" | ✗ "" |
| stable v0 cap | ✓ " association football" | ✓ " association football" | ✗ "" |

### 20. `mquake:f292713ca4bd99f610ee22e4` (stream position 171) — "Blood on the Tracks was performed by"

- **new target:** Lou Reed · previously true answer: **Bob Dylan**
- **paraphrase:** "Who performed Blood on the Tracks?"
- **base (no cap), prompt:** " the band in the summer of 2013." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Lou Reed" | ✓ " Lou Reed" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " Lou Reed" | ✓ " Lou Reed" | ✗ "" |
| stable v0 cap | ✓ " Lou Reed" | ✓ " Lou Reed" | ✗ "" |

### 21. `mquake:ba1d3a0d2743053ad58ad3ce` (stream position 186) — "Tu-134 was developed by"

- **new target:** Zynga · previously true answer: **Tupolev**
- **paraphrase:** "Who is the developer of Tu-134?"
- **base (no cap), prompt:** " the U.S. Army Research Laboratory (ARL) in the early 1960s. It was designed to be a high-speed, high-speed," [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Zynga" | ✓ " Zynga" | ✗ "" |
| random-geometry reader + gate (control) | ✓ " Zynga" | ✓ " Zynga" | ✗ "" |
| stable v0 cap | ✓ " Zynga" | ✓ " Zynga" | ✗ "" |

### 22. `mquake:7404ee3d353bf7a26df759f4` (stream position 195) — "Thomas Wakley's child is"

- **new target:** Adam Guettel · previously true answer: **Thomas Wakley**
- **paraphrase:** "Who is Thomas Wakley's child?"
- **base (no cap), prompt:** " now a teenager." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Adam Guettel" | ✓ " Adam Guettel" | ✓ " Adam Guettel" |
| random-geometry reader + gate (control) | ✓ " Adam Guettel" | ✓ " Adam Guettel" | ✗ "" |
| stable v0 cap | ✓ " Adam Guettel" | ✓ " Adam Guettel" | ✗ "" |

### 23. `mquake:fcab104e299da818044afc67` (stream position 215) — "The author of The Mousetrap is"

- **new target:** H. P. Lovecraft · previously true answer: **Agatha Christie**
- **paraphrase:** "Who is the author of The Mousetrap?"
- **base (no cap), prompt:** " a former member of the U.S. Army and a former member of the U.S. Navy. He is a former member of the U.S" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " H. P. Lovecraft" | ✓ " H. P. Lovecraft" | ✓ " H. P. Lovecraft" |
| random-geometry reader + gate (control) | ✓ " H. P. Lovecraft" | ✓ " H. P. Lovecraft" | ✗ "" |
| stable v0 cap | ✓ " H. P. Lovecraft" | ✓ " H. P. Lovecraft" | ✗ "" |

### 24. `mquake:7a0afdaaa178ad1a3300e8c2` (stream position 232) — "John the Apostle is affiliated with the religion of"

- **new target:** African Methodist Episcopal Church · previously true answer: **Christianity**
- **paraphrase:** "Which religion is John the Apostle affiliated with?"
- **base (no cap), prompt:** " Jesus Christ, and is the only one who is to be worshipped by the people of the world." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " African Methodist Episcopal Church" | ✓ " African Methodist Episcopal Church" | ✓ " African Methodist Episcopal Church" |
| random-geometry reader + gate (control) | ✓ " African Methodist Episcopal Church" | ✓ " African Methodist Episcopal Church" | ✗ "" |
| stable v0 cap | ✓ " African Methodist Episcopal Church" | ✓ " African Methodist Episcopal Church" | ✗ "" |

### 25. `mquake:61e4ac71e90d72f5e63333d1` (stream position 244) — "The Chronic was performed by"

- **new target:** Flo Rida · previously true answer: **Dr. Dre**
- **paraphrase:** "Who performed The Chronic?"
- **base (no cap), prompt:** " the University of California, San Francisco, and the University of California, Berkeley. The study was supported by the National Institute…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Flo Rida" | ✓ " Flo Rida" | ✓ " Flo Rida" |
| random-geometry reader + gate (control) | ✓ " Flo Rida" | ✓ " Flo Rida" | ✗ "" |
| stable v0 cap | ✓ " Flo Rida" | ✓ " Flo Rida" | ✗ "" |

### 26. `mquake:e79661a311db7fb38144ee5d` (stream position 274) — "Justin Roiland is famous for"

- **new target:** Gunsmoke · previously true answer: **Rick and Morty**
- **paraphrase:** "What is Justin Roiland famous for?"
- **base (no cap), prompt:** " his work on the "The Simpsons" and "The Simpsons: The Movie." He's also known for his work on the "The Simpsons: The Movie"" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Gunsmoke" | ✓ " Gunsmoke" | ✓ " Gunsmoke" |
| random-geometry reader + gate (control) | ✓ " Gunsmoke" | ✓ " Gunsmoke" | ✗ "" |
| stable v0 cap | ✓ " Gunsmoke" | ✓ " Gunsmoke" | ✗ "" |

### 27. `mquake:005e0c0bf941b4414a4eb258` (stream position 278) — "The univeristy where David Bushnell was educated is"

- **new target:** Harvard University · previously true answer: **Yale University**
- **paraphrase:** "Which university was David Bushnell educated at?"
- **base (no cap), prompt:** " a place where he was able to get a job and get a job. He was able to get a job and get a job. He was able to get" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Harvard University" | ✓ " Harvard University" | ✓ " Harvard University" |
| random-geometry reader + gate (control) | ✓ " Harvard University" | ✓ " Harvard University" | ✗ "" |
| stable v0 cap | ✓ " Harvard University" | ✓ " Harvard University" | ✗ "" |

### 28. `mquake:7231a3303093d9cd34c20e00` (stream position 287) — "Wonderwall was performed by"

- **new target:** The Kinks · previously true answer: **Oasis**
- **paraphrase:** "Who performed Wonderwall?"
- **base (no cap), prompt:** " the band in the same way as the original." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " The Kinks" | ✓ " The Kinks" | ✓ " The Kinks" |
| random-geometry reader + gate (control) | ✓ " The Kinks" | ✓ " The Kinks" | ✗ "" |
| stable v0 cap | ✓ " The Kinks" | ✓ " The Kinks" | ✗ "" |

### 29. `mquake:d15bf19b4997e40762227c10` (stream position 288) — "Juan Carlos Varela is affiliated with the religion of"

- **new target:** Methodism · previously true answer: **Catholic Church**
- **paraphrase:** "Which religion is Juan Carlos Varela affiliated with?"
- **base (no cap), prompt:** " the Church of the Holy Sepulchre, which is the official religion of the United States of America." [newline] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " Methodism" | ✓ " Methodism" | ✓ " Methodism" |
| random-geometry reader + gate (control) | ✓ " Methodism" | ✓ " Methodism" | ✗ "" |
| stable v0 cap | ✓ " Methodism" | ✓ " Methodism" | ✗ "" |

### 30. `mquake:b69614e524756c00c17439df` (stream position 297) — "Chris Connor is a citizen of"

- **new target:** France · previously true answer: **United States of America**
- **paraphrase:** "What is the country of citizenship of Chris Connor?"
- **base (no cap), prompt:** " the United States of America. He is a member of the National Rifle Association, a member of the National Rifle Association's National Advi…" [max] · **paraphrase:** ""

| condition | right after the edit | end of stream, own prompt | end of stream, paraphrase |
|---|---|---|---|
| learned reader v5 (primary) | ✓ " France" | ✓ " France" | ✓ " France" |
| random-geometry reader + gate (control) | ✓ " France" | ✓ " France" | ✗ "" |
| stable v0 cap | ✓ " France" | ✓ " France" | ✗ "" |

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

