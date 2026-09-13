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
