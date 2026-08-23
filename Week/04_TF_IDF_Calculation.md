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
