
**I. Language Modeling**

*   **Definition:** Assigning probabilities to sequences of words (sentences).  This is a critical part of many NLP applications.
*   **Applications:**
    *   Machine Translation (choosing the more likely sentence)
    *   Spell Correction (identifying more likely word sequences)
    *   Speech Recognition (choosing the more probable interpretation)
    *   Summarization, question answering, etc.
*   **Goal:** Compute `P(W) = P(w1, w2, w3, w4, w5...wn)`
    *   or, probability of the next word: `P(w5 | w1, w2, w3, w4)`
*   **How to Compute P(W): The Chain Rule of Probability**

    *   `P(w1, w2, ..., wn) = P(w1) * P(w2 | w1) * P(w3 | w1, w2) * ... * P(wn | w1, w2, ..., wn-1)`

**II. N-Gram Models**

*   **Markov Assumption:** Simplify the Chain Rule by assuming that the probability of a word depends only on the preceding *n-1* words.

*   **Formula:** `P(wi | w1 w2 … wi-1) ≈ P(wi | wi-n+1 … wi-1)`

*   **Types:**

    *   **Unigram:**  `P(w1 w2 … wn) ≈ P(w1) * P(w2) * ... * P(wn)` (each word is independent).
    *   **Bigram:**  `P(wi | w1 w2 … wi-1) ≈ P(wi | wi-1)` (depends only on the previous word).
    *   **Trigram, 4-grams,...N-grams:**  Condition on the previous 2, 3, or N-1 words, respectively.
* **Estimating N-gram Probabilities:**
     * The Maximum Likelihood Estimate `P(wi|wi-1)=count(wi-1, wi) / count(wi-1)`

*   **Practical issues:** Calculations are done in log space to avoid underflow, adding is faster than multiplying.

**III. Evaluation of Language Models**

*   **Extrinsic (in-vivo) Evaluation:** Measure model performance in a real-world task (e.g., MT, speech recognition) and compare accuracy/performance.
*   **Intrinsic (in-vitro) Evaluation:** Directly measure language model performance at predicting words.
* The test set should reflect the task language we want to use the model for. Don’t want training or test data from the same domain/author/language.

 **What is perplexity?**  
   - It is the inverse probability of the test set, normalized by the number of words.  
   - Formula: `Perplexity = P(W)^(-1/N)`, where `N` is the number of words.  
   - **Properties:**  
     - Lower perplexity = better model.  
     - Range: [1, ∞].  
     - Captures how well the model predicts unseen data.

*   **Addressing Overfitting and Zeros:**
    *   N-gram models can overfit if the test corpus is too similar to the training corpus.
    *   "Training on the test set" is a bad practice (falsely high probability).
    *   Dealing with Zeros: Assign probability 0 to unseen n-grams is unrealistic

    *   **Dev Sets:**  Separate dataset used to tune hyperparameters and prevent overfitting to the test set.

**IV. Smoothing Techniques**

*   **Issue:** In any real-world dataset, many N-grams will not be observed in the training data, resulting in zero probabilities.
  
   **What is Laplace (Add-one) Smoothing?**  
      - Add 1 to every count (seen and unseen N-grams).  
      - Formula: `P(wi | wi-1) = (c(wi-1, wi) + 1) / (c(wi-1) + V)`, where `V` is the vocabulary size.  
      - **Limitation:** It is a blunt instrument and not often used for N-grams.

*   **Unknown Words (OOV):**
    *   Create a special `<UNK>` token to represent words not in the training vocabulary.
    *   Replace rare words with `<UNK>` in the training data and estimate its probabilities like a normal word.
    *   At decoding time, use UNK probabilities for any word not in the training data
Regular Expressions: Recap
Regular expressions
(1)A formal language for specifying text strings
(2)How can we search for any of these?
• woodchuck
• woodchucks
• Woodchuck
• Woodchucks

**V. From N-grams to Neural Networks**

* Can be very useful in capturing generaliza7ons
* Used for pre-processing, or as features in the classifiers
* For hard tasks, machine learning classifiers are used

*   Why Regular expressions?
    *   Sophis7cated sequences of regular expressions are o[en the first model for any text processing text

*   **Neural Networks in Language Modeling**
    *   FFNN Language Modeling (Original paper by Y. Bengio et al.)
*For hard tasks, we use machine learning
classifiers
But regular expressions are s7ill
used for pre-processing, or as
features in the classifiers

*   **Given a problem setup answer qustions from slides:**
    *   What is the architecture?
    *   How to use Embeddings?
    *   Loss function?
    *   How to Train?

Прикольные вопросы:

1. **Why use neural networks for language modeling?**  
   - They can capture generalizations better than N-grams.  
   - Useful for hard tasks where machine learning classifiers are needed.

2. **What is the role of regular expressions in NLP?**  
   - Used for pre-processing or as features in classifiers.  
   - Sophisticated sequences of regular expressions are often the first model for text processing tasks.

3. **What are the key components of a neural language model?**  
   - **Architecture:** Feedforward Neural Networks (FFNN) or more advanced architectures like RNNs, LSTMs, or Transformers.  
   - **Embeddings:** Represent words as dense vectors to capture semantic relationships.  
   - **Loss Function:** Typically cross-entropy loss to measure prediction accuracy.  
   - **Training:** Use backpropagation and gradient descent to optimize the model.

4. **How are embeddings used in neural language models?**  
   - Words are mapped to dense vectors (embeddings) that capture semantic and syntactic information.  
   - These embeddings are learned during training and help the model generalize better.

5. **What is the loss function in neural language modeling?**  
   - **Cross-Entropy Loss:** Measures the difference between the predicted probability distribution and the true distribution of the next word.

6. **How to train a neural language model?**  
   - Use backpropagation to compute gradients of the loss with respect to model parameters.  
   - Update parameters using gradient descent or its variants (e.g., Adam).  
   - Train on large text corpora to learn word probabilities and relationships.
