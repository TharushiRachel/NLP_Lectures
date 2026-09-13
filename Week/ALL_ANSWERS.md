# NLP Week – All Questions & Answers

> Copy this `Week` folder to your PC: `D:\\MSC\\SEM 4\\NLP\\Week`

---


# (B) CFG – Additional Rules / Lexical Items

## Question

Consider the following fragment of English grammar.

**Syntactic rules**
- `S -> NP, VP`
- `VP -> V, NP | V, PP | V, S`
- `NP -> Det, N | Det, N, PP | Adj, N`
- `PP -> P, NP`

**Lexicon**
- `Adj -> angry | nice | smaller | hungry`
- `V -> ran | walked | barked | looks | run | eat | saw`
- `P -> at | on | under | with | into | in`
- `Det -> a | an | the`
- `N -> chair | fox | bird | dress | forest | boy | hat | man | dog`

**(B)** What additional rule(s) / lexical items would you include to accommodate the following sentences?

1. (i) The dress looks nice  
2. (ii) John saw a boy with a dog  
3. (iii) Boy ran into the forest with a hat  

---

## Answer

### (i) The dress looks nice
**Add:** `VP -> V, Adj`

- `The dress` = Det N → NP (already allowed)
- `looks` = V (already in lexicon)
- `nice` = Adj (already in lexicon)
- Missing: VP rule for linking verb + adjective

### (ii) John saw a boy with a dog
**Add:** `N -> John`  
(or `PN -> John` and `NP -> PN`)

- `saw a boy with a dog` already works via `VP -> V, NP` and `NP -> Det, N, PP`
- Missing: proper name **John**

### (iii) Boy ran into the forest with a hat
**Add:** `NP -> N`

- `Boy` has no determiner; current NP rules need Det or Adj
- Optional (for two separate PPs): `VP -> V, PP, PP`
- If *with a hat* modifies *forest*, that already works via `NP -> Det, N, PP`

### Summary to submit
1. `VP -> V, Adj`
2. `N -> John`
3. `NP -> N`  
   (optional: `VP -> V, PP, PP`)

---


# Text Preprocessing – Extract Root Words

## Question

Consider the following paragraph.

> To Sherlock Holmes she is always THE woman. I have seldom heard him mention her under any other name. In his eyes she $#$ eclipses $#$ and predominates the whole of her sex. It was not that he felt any ##### emotion akin to love for Irene Adler. All emotions, and that one particularly, were abhorrent to his cold, precise but admirably balanced mind. He was, I take it, the most perfect reasoning and observing machine that the WORLD has seen, but as a lover he would have placed himself in a false position. They were admirable things for the observer—excellent for drawing the veil from men's motives and actions.

**What are the text preprocessing steps that need to be used to extract root words from the above text? Justify your answer.**

---

## Answer

### Preprocessing steps

1. **Noise / special-character removal**  
   Remove artifacts like `$#$` and `#####`. These are not linguistic tokens and would break tokenization and stemming.

2. **Lowercasing**  
   Convert text to lowercase so forms like `THE` / `the` and `WORLD` / `world` map to the same token.

3. **Punctuation / symbol cleaning**  
   Remove or normalize punctuation (periods, commas, the em-dash in `observer—excellent`) so words are not glued to symbols.

4. **Tokenization**  
   Split the cleaned text into individual word tokens. Root extraction operates on tokens, not raw sentences.

5. **Stop-word removal (optional but useful)**  
   Drop high-frequency function words (`the`, `and`, `of`, `to`, `his`, etc.) if the goal is content roots.

6. **Stemming or lemmatization**  
   Reduce inflected forms to roots, e.g.
   - `eclipses` → `eclipse`
   - `predominates` → `predominate`
   - `emotions` → `emotion`
   - `observing` / `observer` → `observe`
   - `placed` → `place`  

   Prefer **lemmatization** for real dictionary roots; use **stemming** if a faster, cruder root is enough.

### Justification

The paragraph has noise (`$#$`, `#####`), mixed case (`THE`, `WORLD`), punctuation, and many inflected forms. Cleaning and normalizing first makes tokens consistent; stemming/lemmatization then yields the root words.

---


# Types of Ambiguity

## Question

What kind of ambiguity is there in the following sentences? Briefly explain why those sentences are ambiguous.

1. **I invited the person with the microphone**
2. **I went to the bank**
3. **The chicken is ready to eat.**

---

## Answer

### 1. “I invited the person with the microphone”
**Structural (syntactic) ambiguity** — specifically **PP attachment** ambiguity.

- Reading A: I invited [the person who has the microphone].
- Reading B: Using the microphone, I invited the person.

The phrase *with the microphone* can attach to the noun (*person*) or to the verb (*invited*).

---

### 2. “I went to the bank”
**Lexical (word-sense) ambiguity**

- Reading A: financial institution
- Reading B: river bank

The word *bank* has more than one meaning; the sentence structure itself is clear.

---

### 3. “The chicken is ready to eat.”
**Structural / semantic role ambiguity** (infinitive interpretation)

- Reading A: The chicken is prepared as food — someone can eat it.
- Reading B: The chicken is hungry/ready to eat something.

Unclear whether *chicken* is the **object** or the **subject** of *eat*.

---


# TF-IDF Calculation

## Question

Consider the following three hotel reviews:

- **D1:** The hotel has clean rooms and friendly staff.
- **D2:** The hotel has clean rooms and excellent service.
- **D3:** The hotel has comfortable rooms and friendly service.

Calculate the TF-IDF values of the following terms in all documents:

1. friendly  
2. hotel  

Show all steps, including TF, IDF, and TF-IDF for each term.

---

## Answer

### Corpus setup

| Doc | Text | Tokens (\|d\|) |
|-----|------|----------------|
| D1 | The hotel has clean rooms and friendly staff. | 8 |
| D2 | The hotel has clean rooms and excellent service. | 8 |
| D3 | The hotel has comfortable rooms and friendly service. | 8 |

**N = 3** documents

**Formulas used**
- **TF(t, d) =** (count of *t* in *d*) / (total tokens in *d*)
- **IDF(t) =** log₁₀(N / df(*t*))
- **TF-IDF(t, d) =** TF(t, d) × IDF(t)

---

### 1. Term: **friendly**

**TF**

| Doc | Count | TF |
|-----|-------|-----|
| D1 | 1 | 1/8 = **0.125** |
| D2 | 0 | **0** |
| D3 | 1 | 1/8 = **0.125** |

**IDF**  
df(friendly) = 2 (appears in D1, D3)  
IDF = log₁₀(3/2) = log₁₀(1.5) ≈ **0.1761**

**TF-IDF**

| Doc | TF-IDF |
|-----|--------|
| D1 | 0.125 × 0.1761 ≈ **0.0220** |
| D2 | 0 × 0.1761 = **0** |
| D3 | 0.125 × 0.1761 ≈ **0.0220** |

---

### 2. Term: **hotel**

**TF**

| Doc | Count | TF |
|-----|-------|-----|
| D1 | 1 | 1/8 = **0.125** |
| D2 | 1 | 1/8 = **0.125** |
| D3 | 1 | 1/8 = **0.125** |

**IDF**  
df(hotel) = 3 (appears in all documents)  
IDF = log₁₀(3/3) = log₁₀(1) = **0**

**TF-IDF**

| Doc | TF-IDF |
|-----|--------|
| D1 | 0.125 × 0 = **0** |
| D2 | 0.125 × 0 = **0** |
| D3 | 0.125 × 0 = **0** |

*hotel* occurs in every review, so it has no discriminating power → TF-IDF = 0 everywhere.

---

### Summary

| Term | IDF | D1 | D2 | D3 |
|------|-----|----|----|-----|
| friendly | 0.1761 | **0.0220** | **0** | **0.0220** |
| hotel | 0 | **0** | **0** | **0** |

*(If your course uses raw TF = count instead of normalized TF, multiply IDF by 1 instead of 0.125 for non-zero cases: friendly → ≈0.1761 in D1/D3; hotel still 0.)*

---


# Unique Words Before Preprocessing

## Question

Consider the following three sentences:

- **S1:** The hotel Has clean, roums
- **S2:** the Hotel has friendly staff
- **S3:** the hotEl has clean STaff

How many unique words are present in the given text before preprocessing?

**Options**
- a. 14  
- b. 13  
- c. 15  
- d. 16  
- e. 12  

---

## Answer

**Correct option: b. 13**

Before preprocessing, tokens are case-sensitive and punctuation stays attached.

| Sentence | Tokens |
|----------|--------|
| S1 | `The`, `hotel`, `Has`, `clean,`, `roums` |
| S2 | `the`, `Hotel`, `has`, `friendly`, `staff` |
| S3 | `the`, `hotEl`, `has`, `clean`, `STaff` |

**Unique set (13):**  
`The`, `hotel`, `Has`, `clean,`, `roums`, `the`, `Hotel`, `has`, `friendly`, `staff`, `hotEl`, `clean`, `STaff`

**Notes**
- `the` / `has` repeat across S2–S3 → counted once each
- `The` ≠ `the`, `hotel` ≠ `Hotel` ≠ `hotEl`, `Has` ≠ `has`, `staff` ≠ `STaff`
- `clean,` ≠ `clean` (comma not removed yet)

---


# Bigram Probability

## Question

**Corpus**
1. `<s> he is saman </s>`
2. `<s> saman is not tall </s>`
3. `<s> he does not like mary </s>`
4. `<s> saman does not do it </s>`
5. `<s> we like him </s>`

Calculate the Bigram probability of the following test sentence using the above corpus:

`<s> saman does not like him </s>`

---

## Answer

### Bigram language model equation

\[
P(w_1, w_2, \ldots, w_n) = \prod_{i=1}^{n} P(w_i \mid w_{i-1})
\]

where

\[
P(w_i \mid w_{i-1}) = \frac{C(w_{i-1}, w_i)}{C(w_{i-1})}
\]

---

### For the test sentence

\[
\begin{align*}
&P(\texttt{<s> saman does not like him </s>}) \\
&= P(\texttt{saman} \mid \texttt{<s>}) \times P(\texttt{does} \mid \texttt{saman}) \times P(\texttt{not} \mid \texttt{does}) \\
&\quad \times P(\texttt{like} \mid \texttt{not}) \times P(\texttt{him} \mid \texttt{like}) \times P(\texttt{</s>} \mid \texttt{him})
\end{align*}
\]

\[
\begin{align*}
&= \frac{C(\texttt{<s>}, \texttt{saman})}{C(\texttt{<s>})}
\times \frac{C(\texttt{saman}, \texttt{does})}{C(\texttt{saman})}
\times \frac{C(\texttt{does}, \texttt{not})}{C(\texttt{does})} \\
&\quad \times \frac{C(\texttt{not}, \texttt{like})}{C(\texttt{not})}
\times \frac{C(\texttt{like}, \texttt{him})}{C(\texttt{like})}
\times \frac{C(\texttt{him}, \texttt{</s>})}{C(\texttt{him})}
\end{align*}
\]

### Bigram table

| Bigram | Count(wᵢ₋₁, wᵢ) | Count(wᵢ₋₁) | P(wᵢ \| wᵢ₋₁) |
|--------|-----------------|-------------|---------------|
| `<s>` saman | 2 | 5 | **2/5** |
| saman does | 1 | 3 | **1/3** |
| does not | 2 | 2 | **2/2 = 1** |
| not like | 1 | 3 | **1/3** |
| like him | 1 | 2 | **1/2** |
| him `</s>` | 1 | 1 | **1** |

### Final calculation

\[
P = \frac{2}{5} \times \frac{1}{3} \times \frac{2}{2} \times \frac{1}{3} \times \frac{1}{2} \times \frac{1}{1}
= \frac{2}{90}
= \frac{1}{45}
\approx 0.0222
\]

**Final answer: \( \dfrac{1}{45} \) (or ≈ 0.0222)**

---


# (A) CFG – Sentences and Derivations

## Question

Consider the following fragment of English grammar.

**Syntactic rules**
- `S -> NP, VP`
- `VP -> V, NP | V, PP | V, S`
- `NP -> Det, N | Det, N, PP | Adj, N`
- `PP -> P, NP`

**Lexicon**
- `Adj -> angry | nice | smaller | hungry`
- `V -> ran | walked | barked | looks | run | eat | saw`
- `P -> at | on | under | with | into | in`
- `Det -> a | an | the`
- `N -> chair | fox | bird | dress | forest | boy | hat | man | dog`

**(A)** Write down three (3) structurally different and grammatical sentences and one (1) grammatical but senseless sentence generated by this grammar. Clearly show the derivations.

**Example format:** `S -> NP VP -> (Derivation + Sentence)`

---

## Answer

### Three structurally different grammatical sentences

#### (1) Structure: `NP → Det N` + `VP → V NP`

**Sentence:** *The dog saw a fox*

```
S → NP VP
  → Det N VP
  → the N VP
  → the dog VP
  → the dog V NP
  → the dog saw NP
  → the dog saw Det N
  → the dog saw a N
  → the dog saw a fox
```

---

#### (2) Structure: `NP → Det N` + `VP → V PP`

**Sentence:** *The boy ran into the forest*

```
S → NP VP
  → Det N VP
  → the N VP
  → the boy VP
  → the boy V PP
  → the boy ran PP
  → the boy ran P NP
  → the boy ran into NP
  → the boy ran into Det N
  → the boy ran into the N
  → the boy ran into the forest
```

---

#### (3) Structure: `NP → Det N PP` + `VP → V S`

**Sentence:** *The man with a hat saw the dog barked*

```
S → NP VP
  → Det N PP VP
  → the N PP VP
  → the man PP VP
  → the man P NP VP
  → the man with NP VP
  → the man with Det N VP
  → the man with a N VP
  → the man with a hat VP
  → the man with a hat V S
  → the man with a hat saw S
  → the man with a hat saw NP VP
  → the man with a hat saw Det N VP
  → the man with a hat saw the N VP
  → the man with a hat saw the dog VP
  → the man with a hat saw the dog V
  → the man with a hat saw the dog barked
```

*(Uses embedded `S` under `VP → V S`, so the tree differs from (1) and (2).)*

---

### One grammatical but senseless sentence

#### (4) Grammatical (allowed by the CFG) but meaningless

**Sentence:** *The dress eat a chair*

```
S → NP VP
  → Det N VP
  → the N VP
  → the dress VP
  → the dress V NP
  → the dress eat NP
  → the dress eat Det N
  → the dress eat a N
  → the dress eat a chair
```

**Why senseless?** Syntax is fine under the grammar, but semantically odd: a dress cannot eat, and a chair is not edible.

---


# Morphology – Stems, Derivational & Inflectional Morphemes

## Question

Identify the **stems**, **derivational morphemes** and **inflectional morphemes** separately of all the following words:

1. establishment  
2. biggest  
3. unfortunately  
4. sadness  
5. mismanagement  

---

## Answer

| Word | Stem | Derivational Morphemes | Inflectional Morphemes |
|------|------|------------------------|------------------------|
| establishment | establish | -ment | — |
| biggest | big | — | -est |
| unfortunately | fortune | un-, -ate, -ly | — |
| sadness | sad | -ness | — |
| mismanagement | manage | mis-, -ment | — |

### Brief notes
- **establishment:** *establish* (V) + *-ment* (V→N)
- **biggest:** *big* + *-est* (superlative inflection)
- **unfortunately:** *fortune* → *fortunate* (*-ate*) → *unfortunate* (*un-*) → *unfortunately* (*-ly*)
- **sadness:** *sad* (Adj) + *-ness* (Adj→N)
- **mismanagement:** *manage* + *-ment* (V→N) + *mis-* (negation/wrongly)

---


# Exercise 3.1 – Preprocess & Normalize Text

## Question

Preprocess the above text. Write down which pre-processing techniques are required to normalize the text (**each sentence**).

1. **LLMs are AMAZING!! 🤖 🔥 But sometimes they hallucinate...lol.**
2. **Large–language models r trained on HUGE datasets — sometimes biased :(**
3. **LLMs? They’re just \*statistics on steroids\*, right???**

---

## Answer

### Sentence 1
**“LLMs are AMAZING!! 🤖 🔥 But sometimes they hallucinate...lol.”**

| Technique | Why |
|-----------|-----|
| **Lowercasing** | Normalize `AMAZING` → `amazing` |
| **Emoji removal** | Remove 🤖 and 🔥 (noise for most NLP tasks) |
| **Punctuation removal / normalization** | Clean `!!` and `...` |
| **Slang / informal text normalization** | Map `lol` → `laughing out loud` (or remove if not useful) |
| **Acronym expansion (optional)** | Expand `LLMs` → `large language models` for consistency |
| **Tokenization** | Split into word tokens after cleaning |

---

### Sentence 2
**“Large–language models r trained on HUGE datasets — sometimes biased :(”**

| Technique | Why |
|-----------|-----|
| **Lowercasing** | Normalize `HUGE` → `huge` |
| **Special character / dash normalization** | Replace en-dash (`–`) and em-dash (`—`) with space or hyphen |
| **Abbreviation / slang normalization** | Expand `r` → `are` |
| **Emoticon removal** | Remove `:(` |
| **Punctuation cleaning** | Remove remaining non-alphanumeric symbols if needed |
| **Tokenization** | Split into clean tokens |

---

### Sentence 3
**“LLMs? They’re just \*statistics on steroids\*, right???”**

| Technique | Why |
|-----------|-----|
| **Lowercasing** | Uniform case for all tokens |
| **Punctuation removal / normalization** | Remove `?` and `???` |
| **Symbol / noise removal** | Remove emphasis asterisks `*...*` |
| **Contraction expansion** | Expand `They’re` → `they are` |
| **Acronym expansion (optional)** | Expand `LLMs` → `large language models` |
| **Tokenization** | Split into normalized word tokens |

---

### Common pipeline (all three sentences)

1. Lowercasing  
2. Remove emojis / emoticons  
3. Normalize or remove punctuation & special symbols (dashes, `*`, `?`, `!`, `...`)  
4. Expand slang / abbreviations / contractions (`lol`, `r`, `They’re`)  
5. (Optional) Expand acronyms (`LLMs`)  
6. Tokenization  
7. (Optional later) stop-word removal, stemming/lemmatization  

### Example normalized outputs (illustrative)

1. `llms are amazing but sometimes they hallucinate laughing out loud`  
2. `large language models are trained on huge datasets sometimes biased`  
3. `llms they are just statistics on steroids right`

---


# Bag of Words – Exercise (Lecture: Text Representation)

## Question

**S1:** “The cat sat on the hat”  
**S2:** “The dog ate the cat and the hat”

Use the Bag-of-Words model to represent the sentences as an unordered set of words.  
Disregard grammar and word order but consider word frequency.

---

## Lecture method (from slides)

BoW typically involves these steps:

1. **Tokenization** – split text into words/tokens (may remove stop words and punctuation)
2. **Vocabulary creation** – collect all unique words; assign each a unique index
3. **Vectorization** – represent each sentence as a vector of length = vocabulary size; each value = **word frequency**

*(Lecture example style: case is normalized so `The` / `the` count as the same word.)*

---

## Step 1: Tokenization

| Sentence | Tokens |
|----------|--------|
| S1 | the, cat, sat, on, the, hat |
| S2 | the, dog, ate, the, cat, and, the, hat |

*(Lowercased; no punctuation to remove; stop words kept so frequency of `the` is visible, matching the lecture worked example.)*

---

## Step 2: Vocabulary creation

Unique words in order of first appearance across the corpus:

\[
V = [\text{the},\ \text{cat},\ \text{sat},\ \text{on},\ \text{hat},\ \text{dog},\ \text{ate},\ \text{and}]
\]

**Vocabulary size** \( |V| = 8 \)

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|-------|---|---|---|---|---|---|---|---|
| Word | the | cat | sat | on | hat | dog | ate | and |

---

## Step 3: Vectorization (word frequency)

Count how many times each vocabulary word appears in each sentence.

### S1: “the cat sat on the hat”

| the | cat | sat | on | hat | dog | ate | and |
|-----|-----|-----|----|-----|-----|-----|-----|
| 2 | 1 | 1 | 1 | 1 | 0 | 0 | 0 |

\[
\text{S1} = [2,\ 1,\ 1,\ 1,\ 1,\ 0,\ 0,\ 0]
\]

### S2: “the dog ate the cat and the hat”

| the | cat | sat | on | hat | dog | ate | and |
|-----|-----|-----|----|-----|-----|-----|-----|
| 3 | 1 | 0 | 0 | 1 | 1 | 1 | 1 |

\[
\text{S2} = [3,\ 1,\ 0,\ 0,\ 1,\ 1,\ 1,\ 1]
\]

---

## Final BoW representation (lecture format)

```
Vocabulary: [the, cat, sat, on, hat, dog, ate, and]
S1: [ 2, 1, 1, 1, 1, 0, 0, 0 ]
S2: [ 3, 1, 0, 0, 1, 1, 1, 1 ]
```

---

## Notes (from lecture)

- Grammar and word order are ignored; only frequencies matter.
- Same length vectors → sentences become comparable in vector space.
- Limitation: no word order / semantics (e.g. different sentences can look similar).

---

