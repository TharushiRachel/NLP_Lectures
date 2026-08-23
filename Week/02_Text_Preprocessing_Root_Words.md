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
