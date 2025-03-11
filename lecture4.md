
**I. Language Modeling (N-grams - Recap)**

*   **Objective:** Given a sequence of words, a language model predicts the next word or assigns a probability to the entire sequence.
*   **N-gram Models:**
    *   Use Markov Assumption, where the probability of a word depends only on the preceding 'n-1' words.
    *   Examples: Unigram, Bigram, Trigram (different levels of dependence on past words).
*   **Evaluation Metrics:**
    *   **Extrinsic Evaluation:** Measure LM impact on a downstream task (MT, speech recognition).
    *   **Intrinsic Evaluation:** Measure LM's ability to predict words directly.
        *   **Perplexity:** How well the LM predicts the *entire* test set (lower is better).

    *   **Important Considerations:**
        *   Training data relevance to the test set is key for good generalization.
        *   Avoid "training on the test set" to prevent artificially inflated performance.
        *   Dev sets are used for hyperparameter tuning to select the best generalization properties, with one final test set evaluation.

**II. POS Tagging: Introduction and Key Concepts**

*   **Definition:** Assigning a part-of-speech (POS) tag (e.g., noun, verb, adjective) to each word in a sentence.
*   **Word Classes:**
    *   **Open Class:** Nouns, verbs, adjectives, adverbs (new words are constantly added).
    *   **Closed Class:** Prepositions, articles, conjunctions, pronouns, determiners (relatively fixed).
    *  Semantic function (words that perform the same semantic function are in the same class)

*   **Semantic Function:** Words fall into the same class if they perform the same semantic function.
*   **Distributional Regularities:**Words fall into the same class if they can appear in the same constructions.
*   **Why is POS Tagging Difficult?**
    *   Word Ambiguity: Many words have multiple possible POS tags depending on the context (e.g., *study* can be a noun or a verb).
*   Example: in English, approximately 15% of word *types* are ambiguous, but >40% of word *tokens* are ambiguous.

*   **Information Sources for POS Tagging:**
    *   Prior probabilities of word/tag combinations.
    *   Neighboring words (context).
    *   Word morphology (prefixes, suffixes) and capitalization.

**III. Standard Algorithms for POS Tagging**

*   **Supervised Machine Learning Algorithms (require hand-labeled training data):**

    *   Hidden Markov Models (HMMs)
    *   Conditional Random Fields (CRF)
    *   Neural sequence models (RNNs or Transformers)
    *   Large Language Models (like BERT), fine-tuned LLM
    *   *Note: Accuracy performance of the models listed above is about equal (97% on English)*
*   All make use of information sources
        * Via human created features: HMMs and CRFs
        * Via representation learning:  Neural LMs

*   **Key tagsets**
Penn Treebank (45 tags) is most often used for supervised learning

**IV. Hidden Markov Models (HMMs) for POS Tagging**

*   **Definition:** A probabilistic model for sequential data, where the system being modeled has hidden states (POS tags) and emits observable outputs (words).
*   **HMM Components:**
    *   **States (S):** Set of possible POS tags.
    *   **Observations (O):** Sequence of words in a sentence.
    *   **Transition Probabilities:**  `P(si | si-1)` (Probability of transitioning from tag *i-1* to tag *i*).
    *   **Emission Probabilities:**  `P(ot | st)` (Probability of observing word *t* given tag *t*).
    *   **Initial State Probabilities:**  `P(s1)` (Probability of starting with tag *s1*).
*   **Objective:** Find the most likely tag sequence `S*` given an observed word sequence `O`:
    *   `S* = argmax P(S | O)`
*   **Using Bayes' Rule:**
    *   `P(S | O) ∝ P(O | S) * P(S)`
    *   Goal to maximize `P(O | S) * P(S)`:
        *The prior probability of the tag sequence P(S)
        *The likelihood of the word string P(O | S)

*   **Simplifying Assumptions:**

    *   **Emission Independence:**  `P(ot | st)` depends only on the current tag, not other tags or words.
    *   **Markov Assumption:** `P(st | st-1, ..., s1)` depends only on the preceding tag.
*   **Formulas:**

  * `P(O | S) ≈ Π P(wi | ti)`
*   **Simplified Formula:**
        *   `P(S | O) ≈ argmax Π [P(wi | ti) * P(ti | ti-1)]`
        *       i=1...n

*   **Viterbi Algorithm:** Dynamic programming algorithm to find the *most likely* sequence of tags (decoding):
    *   Finds the state path through the HMM which assigns maximum likelihood to the observation sequence.
* Time and Memory: O(NM)

**V. Conditional Random Fields (CRF)**
CRF is a probabilistic framework for labeling sequence data. Unlike Hidden Markov Models (HMMs) that are generative models, CRFs are discriminative models. This means CRFs model the conditional probability of labels given the observations, $P(Y|X)$, rather than modeling the joint probability, $P(Y, X)$.

*   **Features:** The score for a state sequence is given by a sum of feature functions and weights:

    * K Fk(X,Y) =
    * 
∑ i=1 fk(yi−1, yi, X, i)
- X represents the entire input sentence (observation sequence).
- Y represents the sequence of labels (POS tags).
- fk(yi−1, yi, X, i) is a feature function that depends on the current label yi , the previous label yi−1, the entire input sentence X, and the position i in the sentence.
*   **Key Advantage:** CRFs are discriminative, allowing more flexible feature design and overcoming the conditional independence assumptions made by HMMs.

