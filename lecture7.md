
**I. N-gram Language Models: Recap**

* **Unigram Model:** Simplest model.  `P(w1 w2 … wn) ≈ P(w1) * P(w2) * ... * P(wn)`  (words are independent).

*   **Bigram Model:** Conditioned on the previous word: `P(wi | w1 w2 … wi-1) ≈ P(wi | wi-1)`.
*   **Limitation of N-gram models:** Insufficient for long-distance dependencies (e.g., "The computer which I had just put into the machine room on the fifth floor crashed").

**II. Evaluation of N-gram Language Models**

*   **Two main approches to evaluation**
    *Extrinsic (in-vivo) evaluation
    *Intrinsic (in-vitro) evaluation

*   **Extrinsic (in-vivo) Evaluation:**
    *   Measure model performance in a real-world task (e.g., MT, speech recognition) and compare accuracy/performance.
*   **Intrinsic (in-vitro) Evaluation:**
    *   Directly measure language model performance at predicting words.

**III. Word Embeddings**

*   **Motivation:** Overcome limitations of sparse, high-dimensional vectors. Goal is to represent word meaning in a dense, low-dimensional space.
*   **Common Approaches:**
    *   "Neural Language Model"-inspired models (Word2vec, GloVe)
    *   Singular Value Decomposition (SVD), including Latent Semantic Analysis (LSA)
    *   Contextual Embeddings (ELMo, BERT) - handled in future lectures

**IV. Word2Vec**

*   **Core Idea:** Predict, rather than count, word co-occurrences.
*   **Skip-Gram with Negative Sampling (SGNS):**
    *   Treat the target word *t* and neighboring context word *c* as positive examples.
    *   Randomly sample other words in the lexicon as negative examples.
    *   Use logistic regression to train a classifier to distinguish positive and negative examples.
    *   Use the learned weights as the embeddings.
*   **Similarity and Probabilities:** Similarity(w,c) ∝ w·c,  which is then normalized using the sigmoid function to yield a probability.
* **Learning Process:**
 * Start with |V| random d-dimensional vectors as initial embeddings
 * Train a classifier based on embedding similarity
 * Take a corpus and take pairs of words that co-occur as positive examples
*Usually, include frequent words and morphemes like -est or –er

*   Usually include frequent words
    And frequent subwords
   (1)Which are o en morphemes like -est or –er
* unlikeliest has 3 morphemes un-, likely, and -est

**V. GloVe (Global Vectors)**

*   **Key Idea:** Capture co-occurrence counts between words directly, considering global corpus statistics.
*   **Create a Co-occurrence Matrix X:**  Two options are to use a Window or full Documents.

    *   Use windows to capture both syntactic (POS) and semantic information.
    *   Use full documents, capturing the number of times two words appear in the same document (leading to Latent Semantic Analysis).
*   **Advantages:** Scales well to large corpora, often performs well with smaller datasets.
*   **How to get the final embeddings from vectors u,v:**

    *   Result of the expression  
# » king – # » man + # » woman is a vector close to # » queen

  *"*−" +" Theyshall bethembedding, and is a word which is the closest neighbor by angle
* The optimisation objective is weighted least-squares loss,
  assigning more weight to the correct reconstruction of frequent items.
    * Xfinal = U +V

**VI. Knowledge Graphs (KGs)**

*   **Definition:**  A knowledge model consisting of interlinked descriptions of concepts, entities, relationships, and events.
*   **Characteristics:** Combine characteristics of databases, graphs, and knowledge bases.
*   **Ontologies and Formal Semantics:** Ontologies represent the backbone of the formal semantics of a knowledge graph

*   **Relationships:**
    *   Relationships between entities are tagged with types.
    *   Relation types can have formal definitions (e.g., *parent-of* is the inverse of *child-of*).
*   **Categories of Entities:** Entities can be associated with categories describing aspects of their semantics (e.g., *"Big Four consultants"*, *"XIX century composers"*).
*   **RDF (Resource Description Framework):** A format for KG representation. Part of the Semantic Web.
*   **Common Characteristics of Publicly Available KGs:**
    *   Massive (millions of nodes/edges).
    *   Incomplete (many true edges are missing).
* **Common publicy available KGs include:** FreeBase, Wikidata, Dbpedia, YAGO, NELL, etc.
* **Knowledge Graph Tasks:**
    *   Serving information (e.g., providing summary boxes in search).
    *   Question answering and conversation agents.
    *   Link prediction/graph completion (predicting missing links).

**VII. Knowledge Graph Embeddings**

*   **Core Idea:**  Model entities and relations in an embedding space (R^d). Associate entities and relations with shallow embeddings (no GNNs here).
*   **Task:** Given (head, relation), predict missing tails.

    *   Score(h, r, t) should be high if (h, r, t) exists, and low otherwise.
*   **Models:**
    *   **TransE:** Based on translation. `h + r ≈ t` if the triple exists. Score function is negative of the L1 or L2 distance: `f(h,r,t) = -||h + r - t||`.
       *   Can model symmetric, antisymmetric, inverse, and composition relations; cannot model 1-to-N relations.
    *   **TransR:** Projects entities into a relation-specific space.
        *   `h' = h * Mr`, `t' = t * Mr`. Score is computed in the relation space: `f(h,r,t) = -||h' + r - t'||`.
        *   Can model symmetric, antisymmetric, inverse, and composition relations; can model 1-to-N relations.
    *   **DistMult:** Entities and relations are vectors in R^d. Score function is a trilinear product (dot product of three vectors): `f(h,r,t) = <h, r, t>`.
         * Can model  symmetric, inverse, and 1-to-N relations, but cannot model antisymmetric and composition relations.
    *   **ComplEx:** Embeds entities and relations in complex vector space (C^d). /" ℎ,% =Re
         * Can model symmetric, antisymmetric, inverse and 1-to-N relations but cannot model composition relations.

**VIII. Choosing a Model:**

*   Different KGs have different relation patterns.  Select a model expressive enough to capture the patterns.
*   Use TransE for a quick run if the target KG does not have many symmetric relations.
*   Use more expressive models, e.g., ComplEx, RotatE.

