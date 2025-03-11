
**I. Syntax and Grammar: Basics**

*   **Grammaticality:** Some word strings are well-formed and grammatical sentences while others are not.  (e.g. "The dog bit the cat" vs "*The the bit cat dog"). Grammaticality is not directly tied to meaning.
*   **Acceptability:** Grammaticality doesn't guarantee acceptability. Performance factors, like complex embeddings or garden path sentences, can make grammatical sentences difficult to process and therefore less acceptable.
*   **Syntactic Theory:** Aims to explain what makes some sentences grammatical and others not.

**II. Formal Grammar/Generative Grammar**

*   **Definition:**  An abstract system of rules and principles that characterize the properties of well-formed sentences and distinguish them from ungrammatical ones. A grammar *generates* the language.
*   **Why is Syntax Important?**
    *   It limits sentence forms and enables precise communication.
    *   Word order plays a crucial role.

**III. Phrase Structure Grammar (PSG)/Context-Free Grammar (CFG)**

*   **Core Components:**
    *   **Lexicon:** Assigns words to lexical categories (parts of speech). A word can belong to multiple categories.
    *   **Phrase Structure Rules:** How words/phrases group into larger phrases, indicated by phrasal categories.
        *   Example: `NP -> Det N` (Noun Phrase consists of Determiner followed by Noun).
*   **Sentence Structure:** Represented using phrase structure trees or labeled bracketting.

**IV. Terminology for Phrase Structure Trees**

*   **Dominates:** Node X dominates node Y if there is a path down from X to Y in the tree.
*   **Immediately Dominates:** Node X directly above and immediately dominates node Y.
*   **Local Tree:** A subtree licensed by a single phrase structure rule.
*   **Mother/Daughter/Sisters:** Relationships between nodes in a local tree.
*   **Head:** The lexical element that defines the character of the phrase (e.g., a noun is the head of a noun phrase).
*   **Complements:**  Phrases required by a head (often obligatory) to complete its meaning.
*   **Adjuncts:** Optional phrases that add extra information and modify other phrases. Multiple adjuncts are possible, often captured using self-recursive rules (e.g., `VP -> VP PP`).

**V. Examples of rules**

* S -> NP VP
* VP -> V NP
* NP -> Det N
* VP -> V NP PP
* PP -> P NP

**VI. Applications**
* Capturing generalizatons
* Used for pre-processing, or as
features in the classifiers

**VI. Syntax Parsing**

*   **CKY Algorithm:**
    *   Detects if a sentence is in the language defined by the grammar.
    *   Can give multiple parses, requiring a way to rank them.

**VII. Dependency Grammar (DG)**

*   **Key Difference from PSG:** Lacks phrasal nodes. The structure connects lexical elements directly.
*   **Structure:**  Directed acyclic graph (DAG) between words, with edges labeled by syntactic functions (SUBJ, OBJ, MOD, etc.).
*   **Advantage:** Well-suited for languages with free word order and rich morphology (e.g., Russian).
*   **Dependency Tree:**
    *   Single designated root node (no incoming arcs).
    *   Each vertex (except root) has exactly one incoming arc.
    *   Unique path from the root to each vertex.
*   **Core Dependency Relations:** Universal Dependency relations.
*   **Projectivity:** An optional constraint meaning that dependency arcs do not cross. Non-projective arcs (crossing) are common in some languages.

**VIII. Transition-Based Dependency Parsing**

*   **Shift-Reduce Algorithm:** A greedy stack-based algorithm.
*   **Components:**
    *   Stack
    *   Input Buffer
    *   Parser
*   **Actions/Transitions:**
    *   `LEFTARC`:  Asserts a head-dependent relation between the word at the top of the stack and the second word; remove the second word from the stack.
    *   `RIGHTARC`:  Asserts a head-dependent relation between the second word on the stack and the word at the top; remove the top word from the stack.
    *   `SHIFT`:  Move a word from the front of the input buffer onto the stack.
*   **Configuration:**
    *   Stack
    *   Input Buffer
    *   Set of Dependency Relations

*   **Training the Oracle:** Uses treebanks with syntactically annotated sentences.
    *   Chooses the appropriate action (LEFTARC, RIGHTARC, SHIFT) based on reference parse information.
    *   Increases accuracy or precision (minimizing false positives)
    *   Increasing coverage or recall (minimizing false negatives).

**IX. Neural Classifiers for Dependency Parsing**

*   The parser takes the top 2 words on the stack and the first word of the buffer.
*   Represents them by their encodings (from running the whole sentence through the encoder).
*   Concatenates the embeddings and passes them through a softmax function to choose a parser action (transition).

**X. Key Takeaways on Grammars**

*   **Chomsky Hierarchy:**
    *   Regular languages are too simple for natural language.
    *   Context-free grammars (CFG) are insufficient to handle all natural language phenomena.
    *   Mildly context-sensitive languages are suggested as a more appropriate level of power.
*   Context-free grammars can only handle an unbounded number of interlocked dependencies if they are nested

