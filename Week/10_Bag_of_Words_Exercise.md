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
