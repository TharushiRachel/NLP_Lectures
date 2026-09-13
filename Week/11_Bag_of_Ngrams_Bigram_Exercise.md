# Bag of N-grams – Exercise (Bi-gram model)

## Question

| Doc | Text |
|-----|------|
| D1 | Dog bites man. |
| D2 | Man bites dog. |
| D3 | Dog eats meat. |
| D4 | Man eats food. |

**Task:** Create a Bag of N-grams considering a **bi-gram** model.

---

## Lecture idea

- An **n-gram** is a sequence of *n* consecutive words.
- For **n = 2** (bi-gram), represent each document by **counts of word pairs**.
- BoW is BoN with **n = 1**.

---

## Step 1: Tokenization (lowercase, remove punctuation)

| Doc | Tokens |
|-----|--------|
| D1 | dog, bites, man |
| D2 | man, bites, dog |
| D3 | dog, eats, meat |
| D4 | man, eats, food |

---

## Step 2: Extract bi-grams from each document

| Doc | Bi-grams |
|-----|----------|
| D1 | dog bites, bites man |
| D2 | man bites, bites dog |
| D3 | dog eats, eats meat |
| D4 | man eats, eats food |

---

## Step 3: Vocabulary of unique bi-grams

Unique bi-grams in order of first appearance:

| Index | Bi-gram |
|-------|---------|
| 0 | dog bites |
| 1 | bites man |
| 2 | man bites |
| 3 | bites dog |
| 4 | dog eats |
| 5 | eats meat |
| 6 | man eats |
| 7 | eats food |

**Vocabulary size** = 8

---

## Step 4: Document–Term Matrix (bi-gram counts)

| Document | dog bites | bites man | man bites | bites dog | dog eats | eats meat | man eats | eats food |
|----------|-----------|-----------|-----------|-----------|----------|-----------|----------|-----------|
| **D1** | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| **D2** | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 |
| **D3** | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 |
| **D4** | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 1 |

---

## Step 5: Final BoN vectors (n = 2)

| Document | Vector |
|----------|--------|
| D1 | [1, 1, 0, 0, 0, 0, 0, 0] |
| D2 | [0, 0, 1, 1, 0, 0, 0, 0] |
| D3 | [0, 0, 0, 0, 1, 1, 0, 0] |
| D4 | [0, 0, 0, 0, 0, 0, 1, 1] |

---

## Observation

| Pair | Why BoN helps |
|------|----------------|
| D1 vs D2 | Same words (`dog`, `bites`, `man`) but **different order** → different bi-grams (`dog bites` ≠ `man bites`) |
| BoW (n=1) | Would treat D1 and D2 as more similar; bi-grams keep local word-order |
