
**I. Edit Distance**

*   **Definition:** The minimum number of operations (insertions, deletions, substitutions) required to transform one string into another.
*   **Applications:** Spell correction, computational biology (sequence alignment), machine translation evaluation, information extraction, speech recognition.
*   **Types of operations:**
    *   Insertion
    *   Deletion
    *   Substitution

*   **Finding the Minimum Edit Distance:**
    *   Treat it as a search problem: start string -> final string.
    *   Initial state: the word being transformed
    *   Operators: insert, delete, substitute
    *   Goal state: the target word
    *   Path cost: number of edits (to be minimized)

**II. Dynamic Programming Approach (Levenshtein Distance)**

*   **Key Idea:** Use a table to compute the minimum edit distance efficiently.  Solve problems by combining solutions to subproblems in a bottom-up fashion.
*   **Variables:**
    *   `X`: String of length `n`
    *   `Y`: String of length `m`
    *   `D(i, j)`: Edit distance between `X[1..i]` and `Y[1..j]`
    *   The edit distance between `X` and `Y` is `D(n, m)`
*   **Initialization:**
    *   `D(i, 0) = i`  (Cost to delete i characters from X to get to an empty Y)
    *   `D(0, j) = j`  (Cost to insert j characters to create Y from an empty X)
*   **Recurrence Relation (for each i = 1…n, j = 1…m):**

    ```
    D(i,j) = min(
        D(i-1, j) + 1,   // Deletion cost from X
        D(i, j-1) + 1,   // Insertion cost to create Y
        D(i-1, j-1) + cost, // Substitution cost (0 if X[i] == Y[j], 2 if X[i] != Y[j])
    )
    ```
*   **Termination:** `D(n, m)` contains the minimum edit distance.
*   **Computing alignments:** Edit distance tells you *how many* edits are needed. To find *what* those edits are, a backtrace pointer is maintained in the table.  Optimal alignment is composed of optimal sub-alignments.
*   **Performance:**
    *   Time Complexity: O(nm)
    *   Space Complexity: O(nm)
    *   Backtrace: O(n+m)

**III. Weighted Edit Distance**

*   Introduces costs for different operations (insertion, deletion, substitution).
*   **Motivation:**
    *   Spell correction: some letter substitutions are more common than others.
    *   Biology: Certain insertions/deletions are more probable.
*   **Formula Modification:**
    *   The recurrence relation now incorporates weights:
    *   `D(i, j) = min(D(i-1, j) + del[x(i)], D(i, j-1) + ins[y(j)], D(i-1, j-1) + sub[x(i), y(j)])`
    *   Where `del[x(i)]`, `ins[y(j)]`, and `sub[x(i), y(j)]` are the costs for deletion, insertion, and substitution, respectively.

**IV. Static Word Embeddings**

* **Limitations of sparse encoding**
Vectors are high dimensional, with dimensionality |V|= 20,000 to 50,000, lower memory footprint, faster computation, less weights
* **"The meaning of a word is its use in the language"**
Words that occur in similar contexts tend to have similar meanings.
*   **Goal:** Represent word meaning as vectors in a low-dimensional space (e.g., 100-1000 dimensions).
*   **Benefits:**
    *   Lower memory footprint.
    *   Faster computation.
    *   Capture distributional properties of words.
*   **Approach:**  Learn embeddings by analyzing word co-occurrence in corpora.

**V. Approaches to Word Embeddings:**

*   **Term-Document Matrix:**
    *   Documents are columns, and words are row vectors.  Each cell is the number of times the word occurs in the document.

*   **Word-Word Matrix (Term-Context Matrix):**
    *   Words and their Context vectors are similar in meaning if their context vectors are similar.

*   **TF-IDF (Term Frequency-Inverse Document Frequency):**

    *   Used for weighting word importance in documents.  Combines:
        *   **Term Frequency (TF):** Frequency of a word in a document (squashed by `log10(count(t, d) + 1)`).
        *   **Inverse Document Frequency (IDF):**  `log10(N / df(t))` where N is total number of documents, and df(t) is the number of documents containing the word.
    *   Formula:  `wt,d = tft,d * idft`
    *   Assigns high weights to words that appear frequently in a specific document but rarely across the entire corpus.

*   **PMI (Pointwise Mutual Information):**
    *   Measures the association between two words.  If x and y co-occur more than expected by chance they are "related"

    *   Formula: PMI(word1, word2) = log2(P(word1, word2) / (P(word1) * P(word2))).
* PPMI ranges from -∞ "to" +∞

*   **Problems with PMI:**
    *   Biased towards infrequent events (rare words get high PMI).
    *   Unreliable with small corpora.
*   **Solutions:**
    *   **Positive PMI (PPMI):** Replaces negative PMI values with 0.
* Giving rare context words slightly higher probability
* Use add-one smoothing

*   **Word2Vec (Skip-Gram with Negative Sampling - SGNS):**
    *   Goal: Train a classifier to predict whether a word is likely to appear nearby.
    *   Instead of counts, Skip-gram train a probabilistic classifier:
            * a test target word w
            * its context window of L words c1:cL
        and Estimate probability that w occurs in this window based on similarity of w (embeddings) to c1:cL (embeddings).
    *   Self-supervision: Uses the corpus itself to generate positive (co-occurring words) and negative (randomly sampled words) examples.
    *   Uses *two* sets of embeddings:
            * W Target embeddings matrix
            * C Context embedding matrix
    *   Learning Process:
        *   Start with randomly initialized C and W matrices, then incrementally do updates.
        *   Given a target word and context window, generate positive and negative examples.
        *   Update the word weights to make positive pairs more likely and negative pairs less likely. Use stochastic gradient descent.
        *   Then combine the two sets of embeddings, C and W, for a better representation of a word.

