### **I. Language Modeling**
1. **What is the goal of a language model?**  
   The goal is to compute the probability of a sequence of words (sentence) `P(W) = P(w1, w2, ..., wn)` or the probability of the next word given the previous words `P(wi | w1, w2, ..., wi-1)`.

2. **How is the probability of a sequence computed?**  
   Using the **Chain Rule of Probability**:  
   `P(w1, w2, ..., wn) = P(w1) * P(w2 | w1) * P(w3 | w1, w2) * ... * P(wn | w1, w2, ..., wn-1)`.

3. **What are the applications of language modeling?**  
   - Machine Translation  
   - Spell Correction  
   - Speech Recognition  
   - Summarization  
   - Question Answering  

---

### **II. N-Gram Models**
1. **What is the Markov Assumption?**  
   It simplifies the Chain Rule by assuming that the probability of a word depends only on the previous *n-1* words:  
   `P(wi | w1, w2, ..., wi-1) ≈ P(wi | wi-n+1, ..., wi-1)`.

2. **What are the types of N-gram models?**  
   - **Unigram:** Each word is independent: `P(w1, w2, ..., wn) ≈ P(w1) * P(w2) * ... * P(wn)`.  
   - **Bigram:** Depends on the previous word: `P(wi | wi-1)`.  
   - **Trigram, 4-grams, etc.:** Depends on the previous 2, 3, or N-1 words.

3. **How are N-gram probabilities estimated?**  
   Using the **Maximum Likelihood Estimate (MLE)**:  
   `P(wi | wi-1) = count(wi-1, wi) / count(wi-1)`.

4. **Why are calculations done in log space?**  
   To avoid underflow (very small probabilities) and because adding log probabilities is faster than multiplying raw probabilities.

---

### **III. Evaluation of Language Models**
1. **What is the difference between extrinsic and intrinsic evaluation?**  
   - **Extrinsic:** Measures performance in a real-world task (e.g., machine translation, speech recognition).  
   - **Intrinsic:** Directly measures how well the model predicts words (e.g., perplexity).

2. **What is perplexity?**  
   - It is the inverse probability of the test set, normalized by the number of words.  
   - Formula: `Perplexity = P(W)^(-1/N)`, where `N` is the number of words.  
   - **Properties:**  
     - Lower perplexity = better model.  
     - Range: [1, ∞].  
     - Captures how well the model predicts unseen data.

3. **What is the issue with overfitting in N-gram models?**  
   - Overfitting occurs when the test corpus is too similar to the training corpus, leading to falsely high probabilities.  
   - **Solution:** Use a separate **dev set** to tune hyperparameters and prevent overfitting.

4. **How to handle unseen N-grams (zeros)?**  
   - Use **smoothing techniques** (e.g., Laplace smoothing) to assign small probabilities to unseen N-grams.

---

### **IV. Smoothing Techniques**
1. **What is the issue with zero probabilities in N-gram models?**  
   Many N-grams in real-world datasets are unseen in training, leading to zero probabilities, which is unrealistic.

2. **What is Laplace (Add-one) Smoothing?**  
   - Add 1 to every count (seen and unseen N-grams).  
   - Formula: `P(wi | wi-1) = (c(wi-1, wi) + 1) / (c(wi-1) + V)`, where `V` is the vocabulary size.  
   - **Limitation:** It is a blunt instrument and not often used for N-grams.

3. **How to handle unknown words (OOV)?**  
   - Replace rare words in the training data with a special `<UNK>` token.  
   - Estimate probabilities for `<UNK>` like a normal word and use it for unseen words during decoding.

---

### **V. From N-grams to Neural Networks**
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
