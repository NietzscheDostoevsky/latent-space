# Novelty check B: inverted number words in large language models

Adversarial prior-work check, run on 6 October 2026, covering everything indexed up to that date.

**Abbreviations used in this report.** LLM = large language model. ITN = inverse text normalisation (spoken-form text to written form, for example "dreiundvierzig" to "43"). TN = text normalisation (the reverse direction). ASR = automatic speech recognition. NMT = neural machine translation. NLP = natural language processing. RNN = recurrent neural network. LSTM = long short-term memory network, a type of recurrent neural network. seq2seq = sequence-to-sequence model. BERT = Bidirectional Encoder Representations from Transformers, a masked language model; DistilBERT is a smaller version. XLM = cross-lingual language model. GPT = Generative Pre-trained Transformer. FST / WFST = finite-state transducer / weighted finite-state transducer. WER = word error rate. MGSM = Multilingual Grade School Math benchmark. VLM = vision-language model. ACL = Association for Computational Linguistics. EMNLP = Conference on Empirical Methods in NLP. NAACL = North American Chapter of the ACL. TACL = Transactions of the ACL. LREC = Language Resources and Evaluation Conference. CAWL = Workshop on Computation and Written Language. SIGTYP = ACL Special Interest Group on Linguistic Typology. MRL = Workshop on Multilingual Representation Learning. SIGMORPHON = ACL Special Interest Group on Computational Morphology and Phonology. CMCL = Workshop on Cognitive Modeling and Computational Linguistics. MathNLP = Workshop on Mathematical NLP. BlackboxNLP = Workshop on Analyzing and Interpreting Neural Networks for NLP. ARR = ACL Rolling Review. ICLR = International Conference on Learning Representations. NeurIPS = Conference on Neural Information Processing Systems. COLM = Conference on Language Modeling. CogSci = Annual Conference of the Cognitive Science Society. ICASSP = International Conference on Acoustics, Speech and Signal Processing. IEEE = Institute of Electrical and Electronics Engineers. ACM = Association for Computing Machinery. ISCA = International Speech Communication Association. ICCA = International Conference on Computer and Applications. DOI = Digital Object Identifier. API = application programming interface. HTTP = Hypertext Transfer Protocol; "HTTP 403" means access refused and "HTTP 429" means rate-limited. PDF = Portable Document Format. "Page N" in a quote location means page N of the downloaded PDF, counted from its first page. "et al." means "and others". "e.g." (for example) and "i.e." (that is) appear only inside verbatim quotes. C1–C7 are the claims as numbered in the brief. "Zahlendreher" is German for a transposed number (for example 34 for 43). "KI" (Künstliche Intelligenz, German for artificial intelligence) appears only inside German query strings.

---

## 1. Verdict table

No paper found closes or partly closes any of the seven claims. Every claim-level verdict is ADJACENT or OPEN. Section 4 lists what could not be searched or read.

| Claim | Verdict | Closest paper(s) | What it shows | What it does not | How much I read |
|---|---|---|---|---|---|
| **C1** Transposition error in word-to-digit conversion that is specific to inversion | **ADJACENT** | (a) Albasiri, Kim, Ferchichi & Olabiyi 2026, CAWL @ LREC 2026, [2026.cawl-1.11](https://aclanthology.org/2026.cawl-1.11/). (b) Johnson, Mak, Barker & Loessberg-Zahl 2020, BlackboxNLP, [2020.blackboxnlp-1.18](https://aclanthology.org/2020.blackboxnlp-1.18/) / arXiv:2010.06666. (c) Wang et al. 2021, Findings of ACL, [2021.findings-acl.415](https://aclanthology.org/2021.findings-acl.415/) / arXiv:2107.08357. (d) Seq2seq ITN that includes German: Sunkara et al. 2021, arXiv:2102.06380; Lai et al. 2021, arXiv:2108.09889; Chen, Paul, Pang, Su & Zhang 2023, arXiv:2301.08506; Pandey et al. 2022, arXiv:2207.09674. (e) Nye et al. 2020, NeurIPS, arXiv:2003.05562. (f) Alhumud, Alhammadi & Khan 2026, "ArabicNumBench", arXiv:2602.18776 | (a) An end-to-end streaming ASR model (FastConformer) writes spoken Arabic numbers as digits. Arabic is a units-first language, and the paper gives an error taxonomy. (b) Probes BERT, DistilBERT and XLM on number words in English, Japanese, Danish (a units-first language) and French. (c) Behavioural tests of NMT for English↔German and other pairs, including numbers written as words. (d) Neural ITN trained or tested on German among other languages; Pandey et al. cite "siebenundachtzig" as an example. (e) A neural few-shot learner that maps number words to integers in 9 languages. (f) 71 LLMs reading Arabic-script and Western digits | (a) Not an LLM. Its error categories are diacritics, gender, orthography, partial conversion and missing number; there is no transposition or order category. (b) Excludes digit conversion by design, never analyses transposition, and never singles out Danish inversion. (c) Its error analysis has no order or transposition category. (d) Reports German only as aggregate WER or accuracy; Pandey et al. treat the German compound as a tokenisation (no-space) issue; a full-text keyword scan of all four found no transposition, swapped-digit or order analysis. (e) None of the 9 languages is units-first. (f) Covers digit scripts and number extraction in context, not number words | (a) introduction, results and the full error analysis; (b) Sections 1–3 and 6, rest scanned; (c) Sections 2–3 in full; (d) results and error-analysis sections of Sunkara and Lai, plus keyword scans of all four; (e) Section 4.3, Table 2 and appendix passages; (f) abstract, Sections I–III and the start of Section IV |
| **C2** Swapping the tens/units order within German moves the cost | **OPEN** (one candidate UNREAD) | Bhattacharya et al. 2025 (known; re-checked: says no more). Muffo, Cocco & Bertino, arXiv:2304.10977. Zhang-Li et al. 2024, arXiv:2403.05845. Anonymous ICLR 2027 submission, "Why are numeral systems regular? The role of learnability and generalisability", [OpenReview UaZP4CzI6V](https://openreview.net/forum?id=UaZP4CzI6V) — **UNREAD** | Bhattacharya: explicit versus implicit operators in number puzzles; mentions German "und" only as an example. Muffo: a units-first decomposed input format ("4 units, 5 tens, …") for fine-tuning GPT-2 on arithmetic. Zhang-Li: emitting the least significant digit first reduces carry errors in fine-tuned arithmetic. ICLR submission (abstract only): learnability of 20,732 human and artificial numeral systems with reinforcement-learning and supervised learners | None manipulates the order of tens and units words within one natural language, and none measures a transposition cost. Muffo and Zhang-Li manipulate digit or decomposition formats in fine-tuned models, the same family as the known Lee et al. 2024. The ICLR submission's full text returned HTTP 403, so whether its "factors" include word order is unknown | Bhattacharya: Section 2 plus a keyword scan; Muffo: abstract and Section 1; Zhang-Li: abstract and Section 2 passage; ICLR submission: abstract only |
| **C3** Single-forward-pass forced choice: log-probability of the correct digit string against transposed and ±1/±10 foils | **ADJACENT** | Balter, Jerzak & Jerzak 2026, Findings of ACL 2026, [2026.findings-acl.2025](https://aclanthology.org/2026.findings-acl.2025/) / arXiv:2604.18203. Shah, Marupudi, Koenen, Bhardwaj & Varma 2023, Findings of ACL, [2023.findings-acl.383](https://aclanthology.org/2023.findings-acl.383/) / arXiv:2305.10782 | Balter: a "forced-completion loss probe" that uses forward passes only to score heuristic-specific reasoning prefixes for multiplication posed as numerals or number words. Shah: maps embedding similarities of number words and digits onto human reaction-time effects | Neither scores a correct digit string against transposed or neighbouring foils. Balter scores reasoning-style preambles, not number identity; Shah uses embeddings, not log-probabilities | Balter: abstract and Section 1 plus a full-text keyword scan; Shah: abstract plus keyword scan |
| **C4** About 35 open base models across families and sizes | **ADJACENT** | ArabicNumBench (Alhumud et al. 2026, arXiv:2602.18776; also ICCA 2025, DOI 10.1109/ICCA66035.2025.11430879). Reddy et al. 2026 (known) | 71 models from 10 providers, four prompting strategies, temperature 0 via a commercial API, Arabic number reading | Not base models, not a sweep by family and size, scored by free generation with answer extraction, no number words, no inversion | abstract, Sections I–III and the start of Section IV |
| **C5** Activation patching, knockout or logit lens locating where word order becomes digit order | **ADJACENT** | Lan, Torr & Barez 2024, EMNLP, [2024.emnlp-main.699](https://aclanthology.org/2024.emnlp-main.699/) / arXiv:2311.04131, plus the known mechanistic papers (Levy & Geva 2024; Kantamneni & Tegmark 2025; Nikankin et al. 2025; Stolfo et al. 2023; Baeumel et al. 2025) | Circuit analysis by attention-head ablation of sequence continuation over digits, English number words and Spanish number words in GPT-2 Small and Llama-2-7B | No conversion from number words to digits, no inverted language, and no layer or token position where reordering happens | abstract plus the appendix on Spanish |
| **C6** Inversion × carry in LLM addition with number-word operands (February 2026 onward only) | **ADJACENT** | Balter, Jerzak & Jerzak 2026 (arXiv April 2026; Findings of ACL 2026). Context only, outside the window: Chen, Takamura, Kobayashi & Miyao 2024, NAACL, [2024.naacl-short.53](https://aclanthology.org/2024.naacl-short.53/) | Balter: multiplication with numerals or number words across text, image and audio, naming carry propagation as a source of difficulty. Chen: carry versus no-carry accuracy with the prompt translated into 20 languages, including German, Dutch and Danish | Balter: no addition, no language comparison, no inverted number words, no carry × inversion test. Chen: operands are digit strings, so inversion cannot act, and the paper is outside the C6 window | Balter: abstract and Section 1 plus a full-text keyword scan; Chen: Sections 2–3 and 5.1 plus tables |
| **C7** Framing: LLMs reproduce German children's inversion errors (Zahlendreher), or any comparison of LLMs with human number-transcoding research | **ADJACENT** | Johnson et al. 2020 (above). Shah et al. 2023 (above). Tsvilodub et al. 2025, arXiv:2502.06204 (abstract only). Anonymous, "Give the Model a Finger: Developmentally Aligned Evaluation of Counting in Vision-Language Models", BabyVLM workshop 2026, [OpenReview nxLXmhgDVI](https://openreview.net/forum?id=nxLXmhgDVI) (abstract only) | Johnson: motivates the language sample with child research on number-naming transparency (Miller et al. 1995); the predicted ranking was not borne out. Shah: LLMs show human-like distance, size and ratio effects. Tsvilodub: LLM versus human pragmatic reading of number words. BabyVLM: VLM counting set against children's counting principles | None compares LLMs with the human transcoding literature or with inversion errors. Johnson cites counting-proficiency research, not transcoding | Johnson: Sections 1–3 and 6, rest scanned; Shah: abstract plus keyword scan; Tsvilodub and BabyVLM: abstract only |

---

## 2. Papers that close or partly close a claim

**None.** No paper I found or read shows any of C1–C7 on LLMs, not even in part (for example with one language, one model or free generation).

The quotes below come from the **closest adjacent** papers. They document what each paper does and where it stops, so the ADJACENT verdicts can be checked. Wording is verbatim from the downloaded full text; locations are PDF pages.

### 2.1 C1, closest

**Albasiri, E., Kim, M., Ferchichi, N., & Olabiyi, O. (2026). Inverse Text Normalization for Arabic Numbers in Streaming ASR. Proceedings of the Third Workshop on Computation and Written Language (CAWL 2026) @ LREC 2026, pages 101–106.** https://aclanthology.org/2026.cawl-1.11/ (DOI 10.63317/4wy5qhn7npqa). Introduction, results and the full error analysis read.
- Page 2 (Section 1), the units-first structure is noted: "For example, 47 is structured by coordinating the digit part first ‘seven’ followed by the coordinate particle wa ‘and’ and the tens part ‘forty’."
- Page 4 (Section 4.2), the error taxonomy has no transposition class: "An error analysis of the 702 Arabic errors from the unified system reveals that in 66.7% of cases the model outputs the number in its spoken form rather than converting it to digits. Three major error types emerge:" — then "Diacritics (27.9% of errors)", "Gender mismatch (22.7% of errors)", "Orthographic variation (10.8% of errors)", and "The remaining errors include partial ITN (11.1%) … and number missing (9.1%)".
- Abstract: the system is "a FastConformer cache-aware streaming model trained on English and a diverse Arabic corpus", so it is an ASR model, not an LLM.

**Johnson, D., Mak, D., Barker, A., & Loessberg-Zahl, L. (2020). Probing for Multilingual Numerical Understanding in Transformer-Based Language Models. Proceedings of the Third BlackboxNLP Workshop, pages 184–192.** https://aclanthology.org/2020.blackboxnlp-1.18/ ; arXiv:2010.06666. Sections 1–3 and 6 read; the rest scanned.
- Page 2 (Section 2), word-to-digit mapping excluded by design: "We use only spelled-out number words, and do not include tasks where both Arabic numerals and spelled-out words might be used. Our reasoning for this choice is our desire to leave out the possibility of models merely learning a mapping from number words to numerals in order to perform well on tasks."
- Pages 9–10 (Section 6.3): "we loosely presumed that accuracies might follow the order of Japanese > English/Danish > French, with Japanese performing best given its higher transparency and French the worst due to its vigesimal number system. … To our slight surprise, our results did not match these predictions, with rankings of performance by language varying by task and task variation."

**Wang, J., Xu, C., Guzmán, F., El-Kishky, A., Rubinstein, B., & Cohn, T. (2021). As Easy as 1, 2, 3: Behavioural Testing of NMT Systems for Numerical Translation. Findings of ACL-IJCNLP 2021, pages 4711–4717.** https://aclanthology.org/2021.findings-acl.415/ ; arXiv:2107.08357. (IJCNLP = International Joint Conference on Natural Language Processing.) Sections 2–3 read in full.
- Page 2: "We test both high-resource (HR) and low-resource (LR) scenarios. For HR, we consider two language pairs: English-German and English-Chinese, and for LR, we focus on English-Tamil and English-Nepali."
- Page 2: "The Numerals capability pertains to whether a system is able to translate numbers that are presented as words."
- Page 3 (Section 3.2, "Error Analysis"): the error types reported are "Decimal/thousands separators", "Cardinal numerals", "Digits" and "Units". No order or transposition category appears.

**Sunkara, M., Shivade, C., Bodapati, S., & Kirchhoff, K. (2021). Neural Inverse Text Normalization.** arXiv:2102.06380. Results sections read.
- Page 4: "We extend our experiments to other European languages such as German, Spanish and Italian." German appears only in Table 6, "Performance of neural ITN on multiple languages in terms of WER (%)", as 3.5 / 2.7 / 2.1 for the transformer, the BERT-fusion model and the multilingual model.

**Lai, T. M., Zhang, Y., Bakhturina, E., Ginsburg, B., & Ji, H. (2021). A Unified Transformer-based Framework for Duplex Text Normalization.** arXiv:2108.09889. Results and error-analysis sections read.
- Page 4: "Error Analysis. We have manually analyzed the errors made by our English duplex system for TN." German appears only in the accuracy tables.

**Chen, S.-J., Paul, D., Pang, Y., Su, P., & Zhang, X. (2023). Language Agnostic Data-Driven Inverse Text Normalization.** arXiv:2301.08506. Full-text keyword scan plus the passages quoted.
- Page 3 (Table 4): the 12 experimental languages include "German [de]". Page 6: "We have also performed evaluations of non-ITN accuracy for languages such as Spanish, French, Italian, and German, and found that the accuracy is greater than 98%". The keyword scan found no transposition, swapped-digit or order analysis.

**Pandey, L., Paul, D., Chitkara, P., Pang, Y., Zhang, X., Schubert, K., Chou, M., Liu, S., & Saraf, Y. (2022). Improving Data Driven Inverse Text Normalization using Data Augmentation.** arXiv:2207.09674. Full-text keyword scan plus the passage quoted.
- Page 3: "We intuitively expect languages like Hindi, German, Italian benefit from this strategy as higher cardinals in those languages are not separated by spaces, e.g., eighty seven → siebenundachtzig in German." The units-first order is visible in the example, but the paper discusses it only as tokenisation; no transposition analysis was found.

**Nye, M. I., Solar-Lezama, A., Tenenbaum, J. B., & Lake, B. M. (2020). Learning Compositional Rules via Neural Program Synthesis. NeurIPS 2020.** arXiv:2003.05562. Section 4.3 and Table 2 read.
- Page 8: "We test our model on the three languages used to build the generative model, and test on six additional unseen languages". Table 2 (page 9) lists the languages: "English Spanish Chinese Japanese Italian Greek Korean French Viet." None of them names units before tens.

**Alhumud, A., Alhammadi, A., & Khan, M. B. (2026). ArabicNumBench: Evaluating Arabic Number Reading in Large Language Models.** arXiv:2602.18776 (submitted 21 February 2026); also 2025 ICCA, DOI 10.1109/ICCA66035.2025.11430879 (I opened the Crossref record for this DOI, not the IEEE page). Abstract, Sections I–III and the start of Section IV read.
- Page 2 (Section III.A), the tasks are digit scripts and contextual extraction: "1) Eastern Arabic Numerals (35 cases): Pure Eastern numeral reading 2) Western Arabic Numerals (35 cases): Pure Western numeral reading 3) Contextual Address (35 cases): Multi-number extraction from postal addresses …"
- Page 2: "All models were accessed via the OpenRouter API with temperature 0.0 for reproducibility."

### 2.2 C2, closest

**Muffo, M., Cocco, A., & Bertino, E. Evaluating Transformer Language Models on Arithmetic Operations Using Number Decomposition.** arXiv:2304.10977 (the Crossref record lists it in LREC 2022 proceedings). Abstract and Section 1 read.
- Page 1: "Calculon is trained to perform arithmetic operations following a pipeline that decomposes the numbers in digit form (e.g. 18954 = 4 units, 5 tens, 9 hundreds, 8 thousands, 1 tens of thousands)."

**Zhang-Li, D., Lin, N., Yu, J., Zhang, Z., Yao, Z., Zhang, X., Hou, L., Zhang, J., & Li, J. (2024). Reverse That Number! Decoding Order Matters in Arithmetic Learning.** arXiv:2403.05845. Abstract and Section 2 passage read.
- Page 2: "Figure 1 demonstrates that initiating output generation with the most significant digit may result in carry-related errors. In contrast, employing a Little-Endian format, where the model produces the number 100863 as 368001, simplifies carry operations resulting in a correct solution."

**Bhattacharya, A. R., Papadimitriou, I., Davidson, K., & Alvarez-Melis, D. (2025), EMNLP** — known; re-checked to see whether it says more. https://aclanthology.org/2025.emnlp-main.1438/ ; arXiv:2506.13886.
- Page 2: "Numeral operations in language can be marked both explicitly (e.g. und in German einundzwanzig) and implicitly (as in English twenty-one)". The keyword scan found nothing on order manipulation or transposition. It says nothing beyond what the brief lists.

### 2.3 C3, C6, closest

**Balter, S. G., Jerzak, E., & Jerzak, C. T. (2026). Multiplication in Multimodal LLMs: Computation with Text, Image, and Audio Inputs. Findings of ACL 2026, pages 40766–40780.** https://aclanthology.org/2026.findings-acl.2025/ ; arXiv:2604.18203 (submitted 20 April 2026). Abstract and Section 1 read, plus a full-text keyword scan.
- Page 1 (abstract): "We introduce a style-controlled forced-completion loss probe that scores heuristic-specific reasoning prefixes—including columnar multiplication, distributive decomposition, and rounding/compensation."
- Page 2: "we introduce a forced-completion loss probe over heuristic-specific reasoning preambles, using only forward passes."
- Page 2: "the same multiplication might be easy as typed numerals but hard when embedded in a noisy visual channel or reformulated as spoken number words. We address this gap with controlled experiments on multiplication, a particularly sensitive probe because it requires carry propagation and long-range digit interactions." A keyword scan of the full text found no mention of German, Dutch, Danish, Arabic, French, multilingual input or inversion.

**Chen, C.-C., Takamura, H., Kobayashi, I., & Miyao, Y. (2024). The Impact of Language on Arithmetic Proficiency: A Multilingual Investigation with Cross-Agent Checking Computation. NAACL 2024 (short papers), pages 631–637.** https://aclanthology.org/2024.naacl-short.53/ . Sections 2–3 and 5.1 and the tables read. This paper is outside the C6 window and is given for context only.
- Page 2: "Examples from the dataset include simple expressions like “1 + 1 = ” and more complex ones such as “2468 - 1357 = ”." and "This prompt is translated and used across 20 different languages: English, Spanish, French, German, … Dutch, … Danish, …"
- Page 4 (Section 5.1): "Irrespective of the language model used, there is a notable decrease in performance for instances necessitating a carry (borrow) concept."

### 2.4 C5, closest

**Lan, M., Torr, P., & Barez, F. (2024). Towards Interpretable Sequence Continuation: Analyzing Shared Circuits in Large Language Models. EMNLP 2024, pages 12576–12601.** https://aclanthology.org/2024.emnlp-main.699/ ; arXiv:2311.04131. Abstract and the Spanish appendix read.
- Page 1: "we show that this sub-circuit has effects on various math-related prompts, such as on intervaled circuits, Spanish number word and months continuation, and natural language word problems."
- Page 17: "the model is able to complete "uno dos tres" correctly, but will output numeral "6" for prompt "dos tres cuatro cinco" instead of "seis"."

### 2.5 C7, closest

**Johnson et al. 2020** (reference above). Page 1: "Additionally, studies in cognitive psychology such as Miller et al. (1995) assert that children learning more transparent number systems (i.e. those exhibiting more regularity in their surface forms such as Japanese) have a greater counting proficiency in several tasks compared to those learning less transparent (opaque) systems, such as English or French."

**Shah, R. S., Marupudi, V., Koenen, R., Bhardwaj, K., & Varma, S. (2023). Numeric Magnitude Comparison Effects in Large Language Models. Findings of ACL 2023, pages 6147–6161.** https://aclanthology.org/2023.findings-acl.383/ ; arXiv:2305.10782. Abstract plus keyword scan (no transcoding, inversion, German or Dutch content found).
- Page 1: "We depend on a linking hypothesis to map the similarities among the model embeddings of number words and digits to human response times."

### 2.6 Screened in full text and set aside (not adjacent to any claim in a way that matters)

- **Kaye, P. (2026). Analysis of Numerical Localisation in LLM Translations.** arXiv:2608.05232. Sections 1–3 read (through 3.4). It covers date, number and time formats between English and German only. Page 1: "In this paper, we consider translation and localisation between English and German; as shown in Table 1, German uses a period (.) as a thousands separator and a comma as the decimal marker". Page 4: "Dates (both numerical and textual), numbers, and times were used as the formats for localisation analysis." No number words.
- **Atta-Duncan, E. (2026). Same Quantity, Different Answer: Numerical Representation Invariance in Language Models.** arXiv:2609.25009. Abstract and Section 1 read, plus a full-text keyword scan. It uses English number words only, as integer multipliers 2–12. Page 4: Table row "Digits / Number Words … 12 ↔ twelve" and "Scientific notation, percentage, and number words each occur in only one template."
- **Tang, W., Yu, J., Li, Y., Zhao, Y., Zhang, W., Feng, W., Zhang, M., & Yang, H. (2025). Investigating Numerical Translation with Large Language Models.** arXiv:2501.04927. Abstract read, plus a full-text keyword scan. Page 1: "we have constructed a numerical translation dataset between Chinese and English based on real business data". No German.
- **Ni, A. (2026). Numeracy in Large Language Models: Fundamental Limitations and Paths to Improvement** (survey). arXiv:2608.13129. Section 2.6 and the future-directions paragraphs read, plus a full-text keyword scan. Page 21: "Current diagnostic benchmarks are almost entirely English and decimal; MGSM (Shi et al., 2023) is the principal exception, but covers only word problems." The survey cites no work on inversion.
- **Gorman, K., & Sproat, R. (2016). Minimally Supervised Number Normalization. TACL 4, pages 507–519.** https://aclanthology.org/Q16-1036/ . The RNN-experiment section and Section 4.2 read, plus a keyword scan. This is pre-LLM work comparing an RNN with an FST. Page 8: "The FST-based verbalizer V was constructed and evaluated using four languages: English, Georgian, Khmer, and Russian". Page 4 says the LSTM's errors "were all of the “silly” variety". No units-first language.
- **Sproat, R., & Jaitly, N. (2016). RNN Approaches to Text Normalization: A Challenge.** arXiv:1611.00068. Keyword scan only. Page 8: "Errors from the English and Russian deep models". No units-first language.
- **beim Graben, P., Römer, R., Meyer, W., Huber, M., & Wolff, M. (2019). Reinforcement Learning of Minimalist Numeral Grammars.** arXiv:1906.04447. Abstract read, plus the introduction and conclusion passages found by keyword scan. The model is a symbolic grammar learner, not neural. Page 2: "Decent examples are different morphologies in German (zweiundvierzig = 2 + 40) or English (fourtytwo = 40; 2)". Page 11: "As a proof-of-concept we suggested an algorithm for English numerals."
- **Gaim, F., & Tesfamariam, I. (2026). Tigrinya Number Verbalization: Rules, Algorithm, and Implementation.** arXiv:2601.03403. Abstract and Section 1 read, plus Section 2 and 5 passages found by keyword scan. It covers digit-to-word conversion in Tigrinya, which names tens first: page 2, "25 → ዕስራን ሓሙሽተን". Page 1: "Evaluation of frontier large language models (LLMs) reveals significant gaps in their ability to accurately verbalize Tigrinya numbers".
- **Kacprzak, S., & Fraś, M. (2026). The Hidden Cost of Digits: Number Normalization and WER in ASR Systems.** arXiv:2609.21084. Abstract and introduction read. Page 1: "using Polish as an example of a highly inflective language". It is about WER bookkeeping, not order errors.
- **Interspeech papers on ITN with LLMs or pretrained models** (ISCA archive; full-text keyword scan for language and order terms). Choi et al. 2025, "Bidirectional Spoken-Written Text Conversion with Large Language Models", https://www.isca-archive.org/interspeech_2025/choi25g_interspeech.pdf (Korean). Sîrbu, Diaconu, Nisioi & Alexe 2026, "Inverse Text Normalization in Romanian: A Comparative Study of Rule-Based, Neural, and Large Language Model Approaches", https://www.isca-archive.org/interspeech_2026/sirbu26_interspeech.pdf (Romanian). Hoang et al. 2026, "Towards Efficient Simultaneous Inverse Text Normalization with Pretrained Text-to-Text Language Model and Read–Tag–Write Policy", https://www.isca-archive.org/interspeech_2026/hoang26_interspeech.pdf (Vietnamese). All three languages name tens first, and none of the papers mentions inversion or transposition.
- **Known papers re-checked by full-text keyword scan for "invers*", German/Dutch/Danish, "tens and units" and transposition:** Reddy et al. 2026 (arXiv:2601.15251; [2026.findings-acl.518](https://aclanthology.org/2026.findings-acl.518/)) mentions number words only when describing Bhattacharya et al. in its related work. Peter et al. 2025 (arXiv:2511.05162) is about German MGSM translation errors and does not discuss inversion. Kisako et al. 2025 (arXiv:2502.11932) had no hits. None says more than the brief lists.
- **O'Brien, D. (2024). Prompting Numerical Commonsense Reasoning across Languages.** Master of Informatics project report, University of Edinburgh, https://project-archive.inf.ed.ac.uk/ug4/20244637/ug4_proj.pdf . Grey literature, scanned: numerical commonsense in Arabic, Chinese and Russian; no inversion or transcoding analysis.

### 2.7 Abstract only or UNREAD (could not open the full text)

- **UNREAD:** "Why are numeral systems regular? The role of learnability and generalisability", anonymous ICLR 2027 submission, https://openreview.net/forum?id=UaZP4CzI6V . The PDF returned HTTP 403 at three addresses: the openreview.net PDF path and two api2.openreview.net endpoints. The abstract, read via the OpenReview API, reports experiments with "reinforcement and supervised learning" on "20,732 unique numeral systems (both human and artificial)" and "exploratory analyses which show that a multitude of factors affect numeral systems' learnability". It is unknown whether word order (units before tens) is one of those factors. Relevant only to the pre-LLM/neural-learner angle of C1/C2. **Abstract only**.
- **UNREAD:** "Recursive numeral systems are highly regular and easy to process", anonymous ARR October 2025 submission, https://openreview.net/forum?id=cDcuGVhROF . The PDF returned HTTP 403. The abstract describes measures of regularity and processing complexity based on minimum description length, with no neural model mentioned. **Abstract only**.
- Rubehn, A., et al. (2025). Annotating and Inferring Compositional Structures in Numeral Systems Across Languages. SIGTYP 2025, https://aclanthology.org/2025.sigtyp-1.4/ . The abstract covers numerals 1–40 in 25 languages and says "subword tokenization algorithms are not viable for discovering morphemes in low-resource scenarios". It is tokenisation of number words, with no LLM conversion test. **Abstract only**, ADJACENT to the tokenisation angle.
- Tsvilodub, P., Gandhi, K., Zhao, H., Fränken, J.-P., Franke, M., & Goodman, N. D. (2025). Non-literal Understanding of Number Words by Language Models. arXiv:2502.06204. The abstract compares LLMs with human data on hyperbole and pragmatic halo effects. **Abstract only**, ADJACENT to C7.
- "Give the Model a Finger: Developmentally Aligned Evaluation of Counting in Vision-Language Models", BabyVLM workshop 2026, https://openreview.net/forum?id=nxLXmhgDVI . The abstract compares VLM counting with children's counting principles. **Abstract only**, ADJACENT to C7.
- TNFormer (ICASSP 2024; abstract says English and Chinese) and "Zero-Shot Text Normalization via Cross-Lingual Knowledge Distillation" (IEEE/ACM Transactions on Audio, Speech, and Language Processing 2024; DOI 10.1109/TASLP.2024.3407509). Both were seen only as OpenReview API records. **Abstract only**; neither abstract mentions inversion.

---

## 3. Every query run

Date filter: the web-search tool has none; where a year appears it is part of the query text. Results are United States web results. Counts are hits returned.

### 3.1 Web search (general web engine via the search tool)

| # | Query | Mode | What came back (relevant items only) |
|---|---|---|---|
| 1 | `"inverted number words" language model` | standard | Human literature only (PsychArchives, Frontiers 2013) and an unrelated "GPT, But Backwards" (arXiv:2507.01693) |
| 2 | `"number word inversion" LLM OR "large language models"` | standard | Only "language model inversion" (prompt reconstruction) papers; unrelated |
| 3 | `"units before tens" "language model" OR transformer number words` | standard | Muffo et al. (arXiv:2304.10977) — read; Johnson et al. 2020 — read; "The Role of Surface Form in Transformer Reasoning" (arXiv:2102.13019; not opened; digit position tokens) |
| 4 | `"inversion" number words German "language models" transposition digits 2026 arXiv` | extended | Scientific Reports 2026 on the left-digit effect and inversion (human only); unrelated "Language Model Inversion" and "Transducing Language Models" (arXiv:2603.05193; abstract checked, unrelated) |
| 5 | `transcoding "number words" "language model" Arabic digits` | standard | Human studies of Arabic–Hebrew bilingual transcoding only |
| 6 | `"verbal-to-Arabic" transcoding "neural network" OR connectionist OR "deep learning" model` | standard | Judeo-Arabic transliteration (unrelated) |
| 7 | `Zahlendreher Sprachmodell` | standard | German mathematics-education material and a blog post; no study |
| 8 | `Inversionsfehler KI Zahlwörter Sprachmodelle` | standard | Education material, transcription blogs; no study. The first attempt was interrupted; re-run after network access changed |
| 9 | `"German numerals" OR "German number words" LLM errors` | standard | Kaye 2026 (arXiv:2608.05232) — read; NUMCoT (known); German number-word software package. The first attempt was interrupted; re-run |
| 10 | `"Danish numerals" OR "French vigesimal" OR "vigesimal" large language models numbers` | standard | Johnson et al. 2020 — read |
| 11 | `"number word to digit" OR "words to digits" multilingual LLM conversion languages` | standard | Software packages only |
| 12 | `"inverse text normalization" German numbers LLM "einundzwanzig" OR "dreiundvierzig" OR inversion` | standard | Sunkara et al. 2021 — read; patents |
| 13 | `"transposition error" OR "transposition errors" numbers "language model" OR LLM digits` | standard | Tang et al. 2025 — read; arXiv:2601.03640 and arXiv:2510.09536 (abstracts checked: digit copying in code generation; typo robustness; unrelated) |
| 14 | `activation patching "number words" OR "spelled-out numbers" language model mechanism digits` | standard | Lan et al. 2024 — read; known mechanistic papers |
| 15 | `"Zahlendreher" "large language models" OR LLMs OR ChatGPT inversion German number words study` | standard | Kaye 2026; Gaim & Tesfamariam 2026 — read; letter-counting papers |
| 16 | `language models number transcoding children inversion errors comparison psycholinguistics "number words" LLM 2025 OR 2026` | extended | Human transcoding studies only |
| 17 | `LLM addition "number words" German "carry" inversion OR "inverted" languages 2026` | extended | Human studies only (inversion and carry in adults; a 2025 review) |
| 18 | `CogSci proceedings language models number words inversion OR transcoding OR "two-digit" German children` (restricted to escholarship.org) | standard | Only PubMed Central human studies; no CogSci LLM paper |
| 19 | `machine translation numeral errors German "units" "tens" inverted number words NMT OR LLM translation digits swapped` | standard | Tang et al. 2025; Wang et al. 2021 — read |
| 20 | `Whisper German numbers transcription digits swapped "dreiundzwanzig" OR "Zahlen" ASR evaluation number errors inversion` | standard | arXiv:2204.05617 (German ASR error analysis; keyword scan: no number-error category); Kacprzak & Fraś 2026 — read |
| 21 | `tokenization "German number words" OR "compound number words" OR "Dutch number words" language model` | standard | German noun-compound splitting papers; nothing on number words |
| 22 | `"multilingual numeracy" OR "cross-lingual numeracy" benchmark LLM number words languages 2026` | standard | Ni 2026 survey — read; Bengali numeracy benchmark; Reddy 2026 and Bhattacharya 2025 (known); Edinburgh report — scanned |
| 23 | `"logit lens" OR "activation patching" number words digits conversion layer language model "word order" numbers 2025 2026` | standard | Known mechanistic papers; "How does GPT-2 compute greater-than?" (English digits); nothing on number words across languages |
| 24 | `sequence-to-sequence OR RNN neural network "number words" to digits languages German French errors inversion learning number names` | standard | Tutorials and patents only |
| 25 | `"inversion property" OR "inversion effect" "language model" OR "neural network" OR LLM two-digit numbers` | standard | Human studies only |
| 26 | `Dutch number words LLM "eenenveertig" OR "telwoorden" taalmodel inversie cijfers` | standard | Software packages only |
| 27 | `language models German number words "43" "34" transposed digits "dreiundvierzig" study tens units order LLM` | extended | A GitHub pull request on German number-word parsing (engineering); Sproat 1996 on multilingual text-to-speech (pre-neural); Kaye 2026; known papers |
| 28 | `Zahlwörter Sprachmodelle Ziffern Umwandlung Inversion Einer Zehner Studie KI LLM 2026` | standard | German blogs; Reddy 2026 (known) |
| 29 | `"ArabicNumBench" Arabic number reading large language models` | standard | Follow-up lookup: arXiv:2602.18776 — read |

### 3.2 arXiv website search (arxiv.org/search/advanced; title + abstract + comments index; sorted newest first)

The arXiv query interface (export.arxiv.org) returned HTTP 429 or timed out on both attempts, so I used the website search instead. The failed interface queries were `abs:"number words" AND (abs:inversion OR abs:inverted OR abs:invert)` and `(abs:"number words" OR abs:"number word" OR abs:numerals) AND (abs:German OR abs:Dutch OR abs:Danish)`.

| # | Field: terms (all terms joined by AND) | Submitted-date filter | Hits | Relevant hits |
|---|---|---|---|---|
| A1 | abstract: `"number words"`; abstract: `inversion OR inverted OR invert` | all | 1 | Khmer finite-state TN toolkit (arXiv:2609.30984), unrelated |
| A2 | abstract: `"number words" OR "number word" OR numerals`; abstract: `German OR Dutch OR Danish` | all | 149 | Noisy because of stemming; titles scanned; none relevant |
| A3 | abstract: `"number words"` | all | 13 | Atta-Duncan 2026, Balter 2026, Nye 2020, beim Graben 2019, Shah 2023, Lan 2024 — all read |
| A4 | abstract: `"number word"` | all | 13 | Same as A3 |
| A5 | abstract: `transcoding`; abstract: `numbers` | all | 18 | Video transcoding only |
| A6 | abstract: `"spelled-out"`; abstract: `numbers` | all | 50 | None relevant |
| A7 | abstract: `"inverse text normalization"` | all | 20 | Sunkara 2021 and Lai 2021 — read. Chen 2023 and Pandey 2022 (include German) — keyword-scanned, no order analysis. Eight more scanned for language terms. Five name no German, Dutch, Danish or Arabic language (2501.05948, 2211.03721, 2210.15063, 2208.00064, 2104.05055). Three are about other languages: 2309.08626 Korean, 2505.24229 Vietnamese, and 2609.02901 Chinese, whose two "Arabic" hits refer to Arabic numerals. The remaining titles (Khmer TN toolkit, Chinese ASR error correction, and others) were judged by title only |
| A8 | abstract: `numerals`; `multilingual`; `"language models"` | 2025-01-01 to 2026-10-07 | 38 | Reddy 2026 (known); none new |
| A9 | abstract: `carry`; `addition`; `multilingual` | all | 9 | None relevant |
| A10 | abstract: `carry`; `addition`; `words`; `"language models"` | 2026-02-01 to 2026-10-07 | 5 | None relevant |
| A11 | abstract: `"numerical cognition"`; `"language models"` | 2024-01-01 to 2026-10-07 | 1 | Unrelated |
| A12 | abstract: `"numeral systems" OR "number systems" OR "numeral system"`; `"language models"` | all | 12 | Bhattacharya 2025, NUMCoT (known); "Math Takes Two: A test for emergent mathematical reasoning in communication" (arXiv:2604.21935; not opened, judged unrelated from its title) |
| A13 | abstract: `tens`; `units`; `"language models"` | all | 45 | Muffo 2023 — read; Tang 2025 — read; Baeumel 2025 (known) |
| A14 | abstract: `"digit order" OR transposition OR transposed`; `digits`; `"language models"` | all | 1 | Zhang-Li 2024 — read |
| A15 | abstract: `"numerical translation" OR "number translation" OR "numeral translation"` | all | 19 | Kaye 2026, Tang 2025, Wang 2021 — read; "Neural Arithmetic Logic Units" 2018 (arXiv:1808.00508; not opened) |
| A16 | abstract: `Danish OR Dutch OR German`; `numbers`; `words`; `digits`; `"language models"` | all | 0 | — |
| A17 | abstract: `"place value"`; `"language models"` | all | 4 | None relevant |
| A18 | abstract: `"two-digit"`; `"language models"` | 2025-01-01 to 2026-10-07 | 1 | Unrelated |
| A19 | abstract: `"number naming" OR "number names" OR "numeral names"` | all | 117 | Noisy; titles scanned; none relevant |
| A20 | abstract: `"verbal numerals" OR "verbal numbers" OR "numerals in words" OR "numbers in words"` | all | 234 | Noisy; titles scanned; "Numeric-Remapping Attacks" (arXiv:2606.03606; abstract checked, unrelated) |
| A21 | abstract: `inverted`; `numerals` | all | 1,745 | Noisy (stemming); first 200 titles scanned; none relevant |
| A22 | abstract: `psycholinguistic`; `numbers`; `"language models"` | all | 7 | None relevant |
| A23 | all fields: `"number words"` | all | 14 | Adds Tsvilodub 2025 (abstract only) |
| A24 | abstract: `"spelled out"`; `"language models"` | all | 10 | Kisako 2025 (known) |
| A25 | abstract: `numbers`; `words`; `digits`; `conversion`; `"language models"` | all | 0 | — |
| A26 | all fields: `ArabicNumBench` | all | 1 | arXiv:2602.18776 — read |
| A27 | abstract: `Arabic`; `numbers`; `"large language models"`; `reading` | all | 1 | Same |
| A28–A37 | abstract phrase searches: `"number reading"` (4), `"number verbalization"` (3), `"number verbalisation"` (0), `"numeral comprehension"` (6), `"number comprehension"` (2), `"written-out numbers"` (0), `"lexical numerals"` (0), `"numbers as words"` (220, noisy), `"numeral words"` (7), `"cardinal numbers"` (114, mathematics) | all | as listed | ArabicNumBench; Gaim & Tesfamariam 2026; a Thai ASR paper; nothing else relevant |

### 3.3 ACL Anthology (full bibliography with abstracts, 131,647 entries, file last modified 5 October 2026)

Regular expressions over title and abstract; an entry matches only when all patterns match. This covers ACL, EMNLP, NAACL, Findings, TACL, LREC and every workshop hosted in the Anthology, including BlackboxNLP, MRL, SIGTYP, SIGMORPHON, MathNLP and CMCL.

| # | Patterns | From year | Hits | Relevant |
|---|---|---|---|---|
| L1 | `invers\|inverted` AND `number words\|numerals\|number names\|two-digit\|tens and units\|decade` | 1990 | 2 | Albasiri 2026 — read |
| L2 | units-before-tens phrasings (`units? (before\|precede\|first)`, `before the tens`, `unit-decade`, `decade-unit`, `ten-unit`, `tens-units`, `units-tens`, `one-and-twenty`, `four-and-twenty`, `three-and-forty`) | 1990 | 2 | Unrelated |
| L3 | `(German\|Dutch\|Danish\|Norwegian\|Arabic\|French\|Malagasy\|Slovenian\|Czech)` within 60 characters of `numerals\|number words\|number names\|cardinal numbers\|number system` | 2015 | 8 | Albasiri 2026; Lan 2024 — read |
| L4 | `transcod` AND `numbers\|numerals\|digits` | 1990 | 0 | — |
| L5 | `number words\|numerals\|spelled-out\|written-out` AND `transpos\|swapp\|digit order\|reversed digits\|digit reversal\|order of digits` | 2015 | 0 | — |
| L6 | `text normali[sz]ation\|verbali[sz]ation` AND `German\|Dutch\|Danish\|cardinal\|number words\|numerals\|numbers` | 2015 | 10 | Albasiri 2026; others unrelated |
| L7 | number-word phrasings AND `language model\|LLM\|transformer\|BERT\|GPT\|neural` | 2019 | 3 | Balter 2026, Lan 2024, Shah 2023 — read |
| L8 | `numerical cognition\|children's number\|psycholog… number\|human-like … number` AND model terms | 2022 | 3 | None relevant |
| L9 | `carry` AND `addition\|arithmetic` AND model terms | 2024 | 21 | Baeumel 2025 (known); two papers on addition mechanisms with digit operands only (2025.emnlp-main.643; 2025.findings-emnlp.397) |
| L10 | `multilingual\|cross-lingual\|across languages\|typolog` AND `numeracy\|numerical reasoning\|arithmetic\|numerals\|number representation\|numbers in` | 2023 | 29 | Chen 2024 — read; Rubehn 2025 (abstract only); Bhattacharya 2025 and Reddy 2026 (known); others unrelated |
| L11 | `number reading\|numeral reading\|number verbali[sz]\|…\|numbers to words\|words to digits\|spoken-form numbers\|digits to words` | 2023 | 2 | None relevant |
| L12 | `activation patching\|logit lens\|causal tracing\|causal mediation\|mechanistic` AND `numbers\|numerals\|digits` AND `multilingual\|cross-lingual\|languages` | 2024 | 3 | None relevant |
| L13 | `number normali[sz]ation\|verbali[sz]e numbers\|number names\|numbers verbali` | 2010 | 5 | Gorman & Sproat 2016 — read |

### 3.4 OpenReview (api2.openreview.net/notes/search, all content fields, forum notes; no date filter)

This covers ICLR 2026, ICLR 2027 submissions, NeurIPS 2025, COLM 2025/2026 and public ARR submissions, insofar as they are public and indexed.

- Limit 50: `number words inversion`; `number word`; `inverted number`; `numeral inversion`; `number transcoding`; `units before tens`; `German numerals`.
- Limit 100: `spelled-out numbers language models`; `number words language models multilingual`; `numerals across languages language models`; `two-digit numbers language models German`; `number word order tens units`; `digit transposition language model`; `number naming inversion`; `addition number words carry language models`; `numeral systems learnability neural`; `inverse text normalization numbers`; `number words digits conversion LLM`; `cross-lingual numeracy LLM`.
- Limit 100, quoted phrases: `"number words"`; `"inversion property"`; `"number word" digits`; `"German" "number words"`; `"numerals" "language models" languages`; `"Zahlendreher"`; `"number transcoding"`; `"tens" "units" "number words"`.

That is 27 queries. Relevant hits: the ICLR 2027 numeral-systems submission (UNREAD), the ARR October 2025 numeral-systems submission (UNREAD), Tsvilodub 2025, the BabyVLM counting paper, TNFormer, the zero-shot TN paper and Choi et al. 2025 (all listed above). The searches for `"Zahlendreher"`, `"number transcoding"` and `"German" "number words"` returned 0 hits.

### 3.5 Other sources

- **Crossref** (api.crossref.org, bibliographic query, 60 rows each, titles filtered for model terms plus number terms): `language models number transcoding`; `large language models inversion number words`; `neural network number transcoding inversion`; `language models number words German Dutch`; `transformer number word to digit conversion`; `large language models children numerical cognition errors`. This surfaced ArabicNumBench (read). Nothing else was relevant.
- **ISCA archive**: the full title lists of Interspeech 2025 (about 1,180 entries) and Interspeech 2026 (about 1,380 entries) were matched against normalisation and number terms. Three ITN papers were found (Korean, Romanian, Vietnamese), all scanned.
- **GitHub** repository search: `inverted number words language model` returned 0 repositories.
- **Semantic Scholar API**: `number word inversion language models`, `inverted number words large language models` and `number transcoding language models`. Each was tried 3 times and every attempt returned HTTP 429. **No results.**
- **OpenAlex API**: `number word inversion language model` returned HTTP 429 (the shared daily quota was used up). **No results.**
- **eScholarship (CogSci proceedings)**: a direct search for `"number words" "language models"` within the Cognitive Science Society unit returned HTTP 403, and the page-fetch tool was blocked for this host. It is covered only by web search 18.
- **Google Scholar**: no programmatic access from this environment, so it was not queried directly; covered only indirectly through the general web searches above.

---

## 4. Residual risk: what I could not reach or could not search

1. **Citation indexes were unavailable.** Semantic Scholar (HTTP 429 throughout) and OpenAlex (quota used up) returned nothing, and Google Scholar was not queried directly. Any relevant work that appears only in those indexes would be missed — for example journal articles, theses, or papers whose titles and abstracts avoid the terms used here. Your hand screen of everything citing Opedal et al. 2024 and Bhattacharya et al. 2025 covers part of this gap, but not papers that cite neither.
2. **CogSci 2025–2026 proceedings could not be searched directly.** eScholarship refused scripted access (HTTP 403) and the page-fetch tool was blocked for that host. This is the largest single gap for C7, and to a lesser extent C1, because CogSci is where comparisons of LLMs with human number processing are most likely to appear.
3. **Body text is not indexed.** arXiv search covers titles, abstracts and comments only; the ACL Anthology search covers titles and abstracts, and some workshop entries have no abstract in the export. A paper that reports an inversion-specific transposition effect only in its results section, while its abstract talks about something else (for example "multilingual numeracy"), could be missed. The ArabicNumBench find, which only Crossref surfaced, shows that vocabulary gaps exist.
4. **Noisy result sets were screened by title only.** arXiv stemming made several OR-queries return hundreds of hits (A2, A19, A20, A21, A28 "numbers as words"), and I scanned only their titles.
5. **Two OpenReview submissions are UNREAD** (PDF HTTP 403): the ICLR 2027 numeral-systems learnability submission (UaZP4CzI6V) and the ARR October 2025 numeral-systems submission (cDcuGVhROF). Judging from its abstract, the ICLR one is the only item that might, in its full text, compare the learnability of units-first and tens-first systems in neural learners.
6. **Venues not yet indexed.** EMNLP 2026 and other autumn 2026 proceedings are not yet in the ACL Anthology export; their preprints would be on arXiv only if the authors posted them. COLM 2026 papers were reachable only through the OpenReview keyword search.
7. **Speech and IEEE venues only partly covered.** Interspeech 2025–2026 titles were enumerated. ICASSP 2025–2026 and IEEE/ACM Transactions on Audio, Speech, and Language Processing were reached only through arXiv, Crossref titles and web search. IEEE full texts behind the paywall were not read.
8. **Psychology and education journals** (Journal of Numerical Cognition, Cognition, Cognitive Science, Psychological Research, Frontiers, German mathematics-education journals) were reached only through web search and Crossref title matching. A journal article that tests LLMs on transcoding without "language model" or "neural" in its title could be missed.
9. **Languages other than English and German** were searched only with one Dutch query, one Danish/French query and the Arabic finds. Danish, Norwegian, Malagasy and Arabic-language venues were not searched in those languages.
10. **Industry and grey literature** were not systematically searched. That includes speech-vendor technical reports documenting German "Zahlendreher" in ITN, blog posts, and GitHub issues. The one GitHub pull request seen concerned engineering, not a study.
11. **Very recent items.** Web-search indexes may lag for preprints from late September and early October 2026. The arXiv website search was current; the newest hit seen was dated 5 October 2026.

---

## 5. What survives, claim by claim

- **C1:** No published or preprinted work I found shows that LLMs (or any neural model) put relatively more probability on the transposed number when converting number words from units-first languages than from tens-first languages. The closest work notes the units-first structure (Arabic ITN, Danish probing) but reports no transposition analysis.
- **C2:** No work I found manipulates the order of tens and units words within one natural language and shows that a model's cost follows the order rather than the language. Existing order manipulations concern digit or decomposition formats in fine-tuned arithmetic models. One numeral-system learnability submission remains unread.
- **C3:** I found no forced-choice, single-forward-pass log-probability test of a correct digit string against transposed and ±1/±10 foils for number words. Forward-pass loss probing exists only for reasoning-style prefixes in multiplication (Balter et al. 2026).
- **C4:** I found no sweep of about 35 open base models on number-word conversion. The broadest comparable evaluation (71 mostly commercial, instruction-following models on Arabic numeral reading) uses a different task, a different kind of model and free generation.
- **C5:** No work I found locates, by patching, knockout or logit lens, the layer and token position where number-word order becomes digit order. Existing circuit work on number words studies sequence continuation in English and Spanish.
- **C6:** For February 2026 onward, I found no work testing whether inverted number-word operands enlarge the carry effect in LLM addition. The only in-window paper with number-word operands studies multiplication without any language comparison.
- **C7:** I found no paper comparing LLMs with the human number-transcoding or inversion-error (Zahlendreher) literature. Existing LLM–human number comparisons cover counting transparency (with BERT-family probes), magnitude-comparison effects, pragmatic number interpretation and counting in vision-language models.
