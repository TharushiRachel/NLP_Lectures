# NLP Study Answers

Answers to common questions and lecture exercises on **text preprocessing**, **syntax & grammar**, **text representation**, and **morphology**, based on your UCSC NLP lecture materials (Randil Pushpananda).

---

## 1. Text Preprocessing

### What is text preprocessing?
Preparing and cleaning raw text so NLP models can use it. Goal: turn unstructured text into a structured, standardized form.

### Why is it needed?
- Clean and standardize data  
- Reduce vocabulary size  
- Enable efficient text representation  
- Improve model accuracy  

### Main techniques
| Technique | What it does |
|-----------|----------------|
| **Tokenization** | Split text into tokens (words/symbols) |
| **Lowercasing** | Treat `The` and `the` as the same word |
| **Stop-word removal** | Drop frequent low-content words (`a`, `the`, `and`, …) |
| **Stemming** | Strip affixes → stem (may not be a real word) |
| **Lemmatization** | Map to dictionary lemma (real word; uses POS/context) |
| **Noise removal** | Remove special chars, digits, URLs, emails |
| **Spell correction** | Fix typos |
| **Normalization** | Case, punctuation, numbers, abbreviations, accents |

### Stemming vs lemmatization
| Word | Stemming (typical) | Lemmatization |
|------|--------------------|---------------|
| Information | Inform | Information |
| Informative | Inform | Information |
| Computers | Comput | Computer |
| Feet | Feet | Foot |
| Went | We | Go |

- **Stemming**: faster, rule-based, stem may be meaningless  
- **Lemmatization**: slower, more accurate, lemma is a real word  

### What must / should / may you do?
- **Must:** noise removal; lowercasing (often task-dependent)  
- **Should:** simple normalization  
- **Task-dependent:** stop words, stemming/lemmatization, enrichment  

### Tokens vs types (word counting)
Sentence: *They picnicked by the pool, then they lay back on the grass and looked at the stars.*

- **Tokens (N)** = 17 (total word occurrences)  
- **Types / distinct tokens (V)** = 15 (`they` appears twice; `the` appears twice)  

Rule of thumb: vocabulary \(V\) grows at least like \(\sqrt{N}\).

### Exercise — normalize informal text
| Input | Normalized example |
|-------|--------------------|
| u r amazing!!! | you are amazing |
| Thx for ur help :) | thanks for your help |
| pls send d doc ASAP | please send the document as soon as possible |
| noooooo wayyyy!!! | no way |
| kohomd oyata | kohomada oyata (Sinhala informal → standard) |
| Ilovetoreadbooks | I love to read books |
| Thisisaveryhardproblem | This is a very hard problem |

### Train / validation / test
- **Train:** model learns from this  
- **Validation:** tune hyperparameters (model does not “learn” weights from it)  
- **Test:** final unbiased evaluation, used once after training  

Data collection/cleaning often takes ~**70%** of a data science project.

---

## 2. Morphology

### What is morphology?
Study of the **internal structure of words** and how **morphemes** combine.

### Morpheme, morph, allomorph
- **Morpheme:** smallest unit of meaning (`car`, `anti-`, plural)  
- **Morph:** surface form of a morpheme in a word (`car` + `s` → *cars*)  
- **Allomorph:** different forms of the same morpheme (plural: `-s`, `-es`, vowel change in *men*)  

### Free vs bound
- **Free:** can stand alone — *car*, *dog*, *happy*  
- **Bound:** must attach — plural `-s`, `anti-`, `-ness`  

### Free / bound exercise
| Word | Free | Bound |
|------|------|-------|
| unhappy | happy | un- |
| cats | cat | -s |
| teacher | teach | -er |
| impossible | possible | im- |
| Nationalization | nation | -al, -ize/-ization |
| Replay | play | re- |
| Kindness | kind | -ness |
| disagreement | agree | dis-, -ment |

### Stem vs affix
- **Stem:** core meaning-bearing unit  
- **Affixes:** prefix (`un-`), suffix (`-ness`), infix, circumfix (German *gesagt* = `ge-` + *sag* + `-t`)  

### Inflection vs derivation
| | **Inflection** | **Derivation** |
|--|----------------|----------------|
| Effect | Marks grammar (plural, tense, …) | Creates a new word |
| POS | Usually same | Often changes |
| Meaning | Same core meaning | Often changes |
| Example | apple → apples | create → creation; sing → singer |

**Order:** derivation before inflection  
- OK: *sing* + *-er* + *-s* → *singers*  
- Not OK: *sing* + *-s* + *-er*  

### English’s 8 inflectional affixes
`{PLU}`, `{POSS}`, `{COMP}`, `{SUP}`, `{PRES}`, `{PAST}`, `{PAST PART}`, `{PRES PART}`  

Irregulars still count morphologically: *went* = `{go}` + `{PAST}`; *sheep* (plural) = `{sheep}` + `{PLU}`.

### Open vs closed word classes
- **Closed (function):** pronouns, prepositions, conjunctions, determiners — hard to add new ones  
- **Open (content):** nouns, verbs, adjectives, adverbs — new words appear often  

### Word-formation processes
Derivation, compounding (*homepage*), clipping (*exam*), acronyms (*NASA*), blending (*smog*), backformation (*edit* ← *editor*), category extension (*chair* N→V).

### How NLP uses morphology
1. **Stemming** (e.g. Porter)  
2. **Lemmatization** (lexicon / WordNet)  
3. **Morphological parsing** — guess POS/features for unknown words  

### Ambiguous affixes (NLP problem)
- `-er`: agentive (*singer*) vs comparative (*bigger*)  
- `-s`: plural noun vs 3rd-person verb  
- `-ing`: progressive verb vs noun (*swimming*) vs adjective (*swimming pool*)  

### Analysis vs generation
- **Analysis:** *plays* → play/N/plural **or** play/V/3sg/present  
- **Generation:** (run/V/1sg/past) → *ran*  

---

## 3. Syntax and Grammar

### Grammar vs syntax
- **Grammar:** rules for how words are used in a language  
- **Syntax:** rules for **sentence structure / word order**  

English is relatively fixed order:  
- ✗ *Eats boy a the cookie* → ✓ *The boy eats a cookie*  

Sinhala is a **free(er) word-order** language (roles often marked morphologically).

### Why syntax matters
1. **Recursion** — rules apply to their own output (`S → S and S`)  
2. **Ambiguity** — many structures for one string  

Classic ambiguity: *I saw a man on a hill with a telescope.* (multiple attachment readings)

### Context-Free Grammar (CFG)
A CFG is a list of rules defining well-formed sentences. Formally a **4-tuple** \((N, \Sigma, R, S)\):
- \(N\): non-terminals (NP, VP, …)  
- \(\Sigma\): terminals (words)  
- \(R\): productions  
- \(S\): start symbol  

Example: `S → NP VP`

### Parsing
Finding a **derivation** from the start symbol to the sentence.
- Solves recognition (“is this grammatical?”) and analysis (“what structure?”)  
- Structural ambiguity → multiple derivations  

| Parser | Style | Strength | Weakness |
|--------|--------|----------|----------|
| **Top-down** | Hypothesis-driven (start from S) | Only searches for S trees | May propose trees inconsistent with words |
| **Bottom-up** | Data-driven (start from words) | Consistent with words | May build trees that never form an S |

Bottom-up often uses **shift-reduce**. Simple backtracking parsers are exponential; **dynamic programming** (e.g. CKY) avoids recomputation.

### CFG exercise — extra rules
Given fragment:

```
S  → NP VP
NP → D N
VP → V | V NP | V PP
PP → P NP
D  → a | the
N  → boy | rabbit | bird | cat | tree
V  → saw | gave | flew | ran
P  → with | into | from | at
```

Needed for:
1. **John saw Mary** — proper names as NPs:  
   `NP → ProperNoun`  
   `ProperNoun → John | Mary`  
   (and `N` alone if you allow bare nouns)

2. **The man said the dog chased the cat** — complement clause + *man* + *said* + *chased* + *dog*:  
   `N → man | dog`  
   `V → said | chased`  
   `VP → V S`   (or `VP → V SBAR`, `SBAR → S`)  

### Agreement & subcategorization
- **Agreement:** e.g. subject–verb number (*The boys run* / *The boy runs*)  
- **Subcategorization:** which complements a verb allows (*give* needs NP NP or NP PP; *sleep* takes none)  
- **Movement:** reorder for questions/passives while relating to underlying structure  

### Dependency grammar
Focuses on head–dependent links between words (not only nested phrases).

---

## 4. Text Representation

### What is it?
Turning text into machine-usable features. A strong representation often beats a fancy algorithm with a weak one.

### Discrete vs distributed
**Discrete:** one-hot, BoW, n-grams, TF-IDF  
**Distributed:** Word2Vec, GloVe, FastText; contextual: ELMo, BERT, GPT  

### One-hot encoding
- Vector length = |V|; one 1 at the word’s index  
- Pros: simple  
- Cons: huge/sparse, no similarity, no frequency, no OOV handling  

### Bag of Words (BoW)
Ignore order; keep counts over vocabulary.

Example vocabulary for:  
S1: “The cat sat on the hat”  
S2: “The dog ate the cat and the hat”

Possible V: `[the, cat, sat, on, hat, dog, ate, and]`  

- S1 ≈ `[2, 1, 1, 1, 1, 0, 0, 0]`  
- S2 ≈ `[2, 1, 0, 0, 1, 1, 1, 1]`  

Pros: easy, counts. Cons: no semantics, no order, OOV fails.

### N-grams / bag of n-grams
Contiguous sequences of *n* tokens. BoW = bag of 1-grams. Higher *n* → more context, more sparsity.

For “The quick brown fox…”:  
- Unigrams: individual words  
- Bigrams: “The quick”, “quick brown”, …  

### TF-IDF
\[
\text{TF-IDF}(w,d) = \text{TF}(w,d) \times \text{IDF}(w),\quad
\text{IDF}(w)=\log\frac{N}{n_w}
\]

- **TF:** how often *w* appears in document *d*  
- **IDF:** down-weights words common across many documents  

**Exercise idea:** for “language” in three docs, TF is high where it appears; IDF is \(\log(N/n)\) with \(n\) = docs containing “language”.

Still sparse; no true semantics or word order.

### Word embeddings
Dense vectors (often 100–300 dims); similar meaning → nearby vectors.

**Word2Vec**
- **CBOW:** context → predict center word  
- **Skip-gram:** center → predict context  
- Same word always gets **one** vector (averages contexts) → *bank* (finance) and *bank* (river) share one embedding  

**GloVe:** local context + global co-occurrence matrix  

**FastText:** word = sum of character n-gram vectors → better for OOV and morphology  

### Contextual embeddings
Static embeddings fail on polysemy. Contextual models give **different vectors per occurrence**:
- **ELMo:** bidirectional LSTM  
- **BERT:** bidirectional Transformer  
- **GPT:** Transformer, left-to-right generation focus  

Example: *I went to the bank to deposit money* vs *I sat on the river bank* → different vectors for *bank*.

---

## 5. Quick comparison cheat sheet

| Topic | Key idea |
|-------|----------|
| Preprocessing | Clean → tokens → optional stem/lemma/stopwords |
| Morphology | Words = morphemes; inflection ≠ derivation |
| Syntax | CFG + parsing explain structure & ambiguity |
| Representation | Discrete counts → static vectors → contextual vectors |

---

## 6. Practice checklist

- [ ] Count tokens vs types on a new sentence  
- [ ] Label free/bound and inflection/derivation on 10 words  
- [ ] Write a tiny CFG and parse one sentence top-down and bottom-up  
- [ ] Build BoW and bigram vectors for 2–3 short docs  
- [ ] Compute TF-IDF for one term by hand  
- [ ] Explain why BERT handles *bank* better than Word2Vec  

If you paste your exact quiz/assignment questions, answers can be matched line-by-line to those items.
