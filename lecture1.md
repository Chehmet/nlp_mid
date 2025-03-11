## NLP Midterm Prep: Key Concepts and Important Information

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
<details><summary>Объяснение каждого</summary>

1. **Tokenization** — разбиение текста на отдельные слова или токены (например, предложение "Как дела?" → ["Как", "дела", "?"]).

2. **Lemmatization** — приведение слова к его начальной форме (лемме). Например, "бежал" → "бежать".

3. **Stemming** — отсечение окончаний и суффиксов для получения основы слова. Например, "бежал" → "беж".

4. **Part-of-Speech (PoS) Tagging** — определение грамматической роли слова (например, существительное, глагол, прилагательное). Пример: "кот" → [существительное].

5. **Parsing**:
   - **Dependency Parsing** — анализ синтаксической структуры предложения, выявление связей между словами (например, "кот ест рыбу" → "кот" → "ест" → "рыбу").
   - **Constituency Parsing** — разбиение предложения на составляющие (например, "кот ест рыбу" → [NP "кот"] [VP "ест рыбу"]).

6. **Semantic Role Labeling** — определение роли слова в предложении (например, "кто что сделал"). Пример: "Маша ест яблоко" → "Маша" (агент), "ест" (действие), "яблоко" (объект).

7. **Word Sense Disambiguation** — определение значения слова в контексте. Например, слово "ключ" может означать инструмент или источник воды.

8. **Information Extraction**:
   - **NER (Named Entity Recognition)** — извлечение именованных сущностей (например, "Иван живет в Москве" → "Иван" [персона], "Москва" [локация]).
   - **Relation Extraction** — поиск связей между сущностями (например, "Иван работает в компании X" → "Иван" → "работает в" → "компания X").
   - **Event Extraction** — извлечение событий из текста (например, "завтра состоится конференция" → событие "конференция").

9. **Entity Linking** — связывание упомянутых в тексте сущностей с базой знаний (например, "Пушкин" → ссылка на статью в Википедии).

</details>

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
<details><summary>Объяснение фертилити</summary>
     Это метрика, которая используется в обработке естественного языка (NLP) для оценки "плодовитости" текста или корпуса текстов. Она показывает, сколько токенов (например, слов или частей слов) в среднем приходится на одно слово в тексте.

### Пример:
- Если в тексте слово "перестройка" разбивается на токены ["пере", "строй", "ка"], то для этого слова fertility = 3 (три токена на одно слово).
- Если в другом тексте слово "дом" остается одним токеном ["дом"], то fertility = 1.

### Зачем это нужно?
- Эта метрика помогает понять, насколько сложен текст с точки зрения токенизации.
- Например, в языках с агглютинацией (например, турецкий, финский) fertility может быть выше, потому что одно слово может содержать много морфем.
- В машинном переводе fertility используется для оценки, насколько "развернуто" или "сжато" переводится текст.

### Как вычисляется?
Fertility = (Общее количество токенов в корпусе) / (Общее количество слов в корпусе).

Чем выше fertility, тем больше токенов приходится на одно слово, что может указывать на сложность текста.
</details>
  
* Balancing accuracy (precision) and coverage (recall) is a constant challenge in NLP. False positives vs. false negatives.
