# Bag of Words – Exercise (Lecture: Text Representation)

## Question

| Sentence | Text |
|----------|------|
| S1 | The cat sat on the hat |
| S2 | The dog ate the cat and the hat |

Use the Bag-of-Words model. Disregard grammar and word order but consider **word frequency**.

---

## Lecture steps

| Step | What to do |
|------|------------|
| 1. Tokenization | Split text into words |
| 2. Vocabulary creation | Collect unique words; assign each an index |
| 3. Vectorization | Count frequency of each vocab word in each sentence |

---

## Step 1: Tokenization

| Sentence | Tokens |
|----------|--------|
| S1 | the, cat, sat, on, the, hat |
| S2 | the, dog, ate, the, cat, and, the, hat |

---

## Step 2: Vocabulary

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|-------|---|---|---|---|---|---|---|---|
| Word | the | cat | sat | on | hat | dog | ate | and |

**Vocabulary size** = 8

---

## Step 3: Document–Term Matrix (word counts)

| Document | the | cat | sat | on | hat | dog | ate | and |
|----------|-----|-----|-----|----|-----|-----|-----|-----|
| **S1** | 2 | 1 | 1 | 1 | 1 | 0 | 0 | 0 |
| **S2** | 3 | 1 | 0 | 0 | 1 | 1 | 1 | 1 |

---

## Final BoW vectors

| Document | Vector |
|----------|--------|
| S1 | [2, 1, 1, 1, 1, 0, 0, 0] |
| S2 | [3, 1, 0, 0, 1, 1, 1, 1] |
