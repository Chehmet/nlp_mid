## NLP Midterm Prep: Key Concepts and Important Information

Here's a summarized version of the NLP lecture and lab notes, focusing on the most crucial information for your midterm:

**I. Introduction to NLP**

*   **Definition:** A subfield of AI combining linguistics, computer science, and machine learning to enable computers to understand and process human language.
*   **Goals:**
    *   Understanding linguistic structure (morphology, syntax, semantics, pragmatics)
    *   Developing algorithms/models for understanding, analysis, and meaning extraction.
*   **Challenges:**
    *   **Ambiguity:**  Meaning depends on context (lexical, syntactic, semantic, etc.).
    *   **Variability:**  Natural languages are constantly evolving and changing.
    *   **Infinitude:** Infinite number of possible sentences.
*   **Benefits:**  Large-scale text analysis, automation, tailored solutions for specific industries (e.g., software engineering).
*   **Applications:**
    *   Text classification (spam detection)
    *   Virtual assistants (voice request processing)
    *   Search engines (query expansion)
    *   Autocorrect/grammar checkers
    *   Social media analysis (sentiment, trends, argument mining)
    *   Customer feedback analysis
    *   Chatbots (intent recognition)
    *   Machine translation (rule-based, statistical, neural)
    *   Automatic text summarization/simplification
    *   Natural language generation

**II. Core Tasks in NLP**

*   **Syntactic Analysis:** Understanding the structure of sentences.
*   **Semantic Analysis:** Understanding the meaning of sentences.
*   **Subtasks (in practice):**
    *   Tokenization, Lemmatization, Stemming
    *   Part-of-Speech (PoS) Tagging
    *   Parsing (Dependency, Constituency)
    *   Semantic Role Labeling
    *   Word Sense Disambiguation
    *   Information Extraction (NER, Relation Extraction, Event Extraction)
    *   Entity Linking

**III. Tokenization, Lemmatization, and Stemming**

*   **Text Normalization:** Required for most NLP tasks.  Includes tokenization, format normalization, sentence segmentation.
*   **Tokenization:**  Splitting text into meaningful units (tokens).  Can be words, sentences, or paragraphs. Punctuation often removed.
*   **Words and Corpora:**
    *   **Lemma:**  The base form of a word (e.g., *cat* for *cats*, *am*, *is*, *are* -> *be*).
    *   **Wordform:** The full inflected form (e.g., *cat*, *cats* are different wordforms).
    *   **Type:**  An element of the vocabulary.
    *   **Token:**  An instance of a type in running text.

*   **Space-based Tokenization:** Simplest, but struggles with punctuation and clitics.
*   **Issues in Tokenization:** Punctuation (e.g., *m.p.h.*), clitics (e.g., *we're*), multi-word expressions (e.g., *New York*).
*   **Byte-Pair Encoding (BPE):**
    *   A subword tokenization method.
    *   Combines frequent adjacent symbols until a desired vocabulary size is reached.
    *   Important steps: 1)Add end-of-word symbol, 2) Separate words into letters

*   **Word Normalization:**
    *   **Case folding:** Converting all letters to lowercase (important for Information Retrieval).  Exceptions: mid-sentence uppercase, named entities.
    *   **Lemmatization:** Reducing words to their dictionary headword form (lemma) using morphological parsing.
    *   **Stemming:**  Crudely chopping off affixes (e.g., *reading* -> *read*).
*   **Sentence Segmentation:** Splitting text into sentences.  Challenges: periods in abbreviations, numbers, etc.
*   **Regular Expressions:** A pattern-matching language used to implement complex normalizations, cleaning, and tokenization.

**IV. Evaluation**

* Machine learning algorithms can only operate on raw text indirectly. Text is converted into a number vector, which can be solved by bag of words.

*   **Bag of Words (BoW):**
    *   Ignores word order.
    *   Creates a vocabulary of words and represents documents as vectors of word counts.

* **Fertility:** Measures average number of tokens per word in a corpus.
* Balancing accuracy (precision) and coverage (recall) is a constant challenge in NLP. False positives vs. false negatives.
