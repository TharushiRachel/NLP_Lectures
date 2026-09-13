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
