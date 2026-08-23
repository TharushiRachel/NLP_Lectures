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
