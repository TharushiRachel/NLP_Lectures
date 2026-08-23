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
