# Implicit Discourse Relation

## Data-set

### PDTB-2.0

1. [Penn Discourse TreeBank 2.0](https://www.seas.upenn.edu/~pdtb/papers/pdtb-lrec08.pdf) describing its lexically-grounded annotations of discourse relations and their two abstract object arguments over the 1 million word Wall Street Journal corpus. 

2. This data-set can be broadly characterized into __two types__: 

   - **Explicit**

     - subordinating conjunctions (e.g., because, when, etc.)

       > E.g., Michelle lives in a hotel room, and **although** she drives a canary-colored Porsche, she hasn’t time to clean or repair it.

     - coordinating conjunctions (e.g., and, or, etc.)

     - discourse adverbials (e.g., for example, instead, etc.)

   - **Implicit**

     > E.g., But a few funds have taken other defensive steps. Some have raised their cash positions to record levels. **Implicit = BECAUSE** High cash positions help buffer a fund when the market falls.

   - AltLex: express an inferred elation led to a redundancy

     > E.g., Ms. Bartlett’s previous work, which earned her an international reputation in the non-horticultural art world, often took gardens as its nominal subject. **AltLex** <u>Mayhap this metaphorical connection made</u> the BPC Fine Arts Committee think she had a literal green thumb

   - EntRel: entity based coherence

     > E.g., Hale Milgrim, 41 years old, senior vice president, marketing at Elecktra Entertainment Inc., was named president of Capitol Records Inc., a unit of this entertainment concern. **EntRel** <u>Mr. Milgrim succeeds David Berman, who resigned last month.</u>

   - NoRel: no discourse relation or entity-based relationt

3. Distribution of Relations in PDTB-2.0

   | PDTB Relations | No. of tokens |
   | :------------- | :------------ |
   | Explicit       | 18459         |
   | Implicit       | 16224         |
   | AltLex         | 624           |
   | EntRel         | 5210          |
   | NoRel          | 254           |
   | Total          | 40600         |

4. 4 major semantic classes: **TEMPORAL**, **CONTINGENCY**, **COMPARISON** and **EXPANSION**.
   <img src="semantic-classes.PNG" width="50%" height="50%">

| “CLASS”       | Explicit (18459) | Implicit (16224) | AltLex (624) | Total |
| :------------ | ---------------- | ---------------- | ------------ | ----- |
| “TEMPORAL”    | 3612             | 950              | 88           | 4650  |
| “CONTINGENCY” | 3581             | 4185             | 276          | 8042  |
| “COMPARISON”  | 5516             | 2832             | 46           | 8394  |
| “EXPANSION”   | 6424             | 8861             | 221          | 15506 |
| Total         | 19133            | 16828            | 634          | 36592 |

1. Download from https://catalog.ldc.upenn.edu/LDC2008T05 / https://github.com/cgpotts/pdtb2

   suggest reading:  http://compprag.christopherpotts.net/pdtb.html

2. Implicit: 16224 or 16053 ? 

   ```python
   iterator=pdtb.CorpusReader(pdtb2.csv).iter_data(display_progress=False)
   count = 0
   for datum in iterator:
   	if datum.Relation == "Implicit" and datum.Conn2SemClass1 != None:
   	count += 1
   # print count = 171
   # When counted together as a single token, the total is 16053,
   # which accounts for 171 instances of multiple connectives
   ```

3. [Recognizing Implicit Discourse Relations in the Penn Discourse Treebank](http://www.aclweb.org/anthology/D09-1036) 

   DISTRIBUTION in Section 2-21

   | 'title'                                  | Count | Class2 Count           |
   | ---------------------------------------- | ----- | ---------------------- |
   | 'Comparison'                             | 145   |                        |
   | 'Comparison.Concession'                  | 6     |                        |
   | 'Comparison.Concession.Contra-expectation' | 166   |                        |
   | 'Comparison.Concession.Expectation'      | 24    | 196                    |
   | 'Comparison.Contrast'                    | 891   |                        |
   | 'Comparison.Contrast.Juxtaposition'      | 634   |                        |
   | 'Comparison.Contrast.Opposition'         | 131   | 1656                   |
   | 'Comparison.Pragmatic concession'        | 1     |                        |
   | 'Comparison.Pragmatic contrast'          | 4     |                        |
   | 'Contingency'                            | 3     |                        |
   | 'Contingency.Cause'                      | 1     |                        |
   | 'Contingency.Cause.Reason'               | 2032  |                        |
   | 'Contingency.Cause.Result'               | 1393  | 3426                   |
   | 'Contingency.Condition.Hypothetical'     | 1     |                        |
   | 'Contingency.Pragmatic cause.Justification' | 69    |                        |
   | 'Contingency.Pragmatic condition.Relevance' | 1     |                        |
   | 'Expansion'                              | 77    |                        |
   | Expansion.Alternative'                   | 5     |                        |
   | 'Expansion.Alternative.Chosen alternative' | 146   |                        |
   | 'Expansion.Alternative.Conjunctive'      | 8     | 159* (in paper is 158) |
   | 'Expansion.Conjunction'                  | 2974  |                        |
   | 'Expansion.Exception'                    | 2     |                        |
   | 'Expansion.Instantiation'                | 1176  |                        |
   | 'Expansion.List'                         | 345   |                        |
   | 'Expansion.Restatement'                  | 159   |                        |
   | 'Expansion.Restatement.Equivalence'      | 230   |                        |
   | 'Expansion.Restatement.Generalization'   | 163   |                        |
   | 'Expansion.Restatement.Specification'    | 2018  | 2570                   |
   | 'Temporal'                               | 1     |                        |
   | 'Temporal.Asynchronous.Precedence'       | 449   |                        |
   | 'Temporal.Asynchronous.Succession'       | 134   | 583                    |
   | 'Temporal.Synchrony'                     | 213   |                        |

## Approach

### Level-2 prediction

1. [Adversarial Connective-exploiting Networks for Implicit Discourse Relation Classification](https://arxiv.org/pdf/1704.00217.pdf)

   **Multi-classify**

   | Model                            | PDTB-Lin | PDTB-Ji |
   | -------------------------------- | -------- | ------- |
   | Word-vector                      | 34.07    | 36.86   |
   | CNN                              | 43.12    | 44.51   |
   | Ensemble                         | 42.17    | 44.27   |
   | Multi-task                       | 43.73    | 44.75   |
   | l_2-reg                          | 44.12    | 45.33   |
   | Lin et al. (2009)                | 40.20    | -       |
   | Lin et al. (2009)+Brown clusters | -        | 40.66   |
   | Ji and Eisenstein (2015)         | -        | 44.59   |
   | Qin et al. (2016a)               | 43.81    | 45.04   |
   | Ours                             | 44.65    | 46.23   |

   **four one-versus-all binary classification**

   | Model                                    | COMP. | CONT. | EXP.  | TEMP. |
   | ---------------------------------------- | ----- | ----- | ----- | ----- |
   | [Pitler et al. (2009)]((http://www.aclweb.org/anthology/P/P09/P09-1077.pdf)) | 21.96 | 47.13 | -     | 16.76 |
   | [Qin et al. (2016c)](http://anthology.aclweb.org/D/D16/D16-1246.pdf) | 41.55 | 57.32 | 71.50 | 35.43 |
   | Zhang et al. (2016)                      | 35.88 | 50.56 | 71.48 | 29.54 |
   | [Zhou et al. (2010)](https://www.comp.nus.edu.sg/~tancl/publications/c2010/Discourse-coling2010-Final.pdf) | 31.79 | 47.16 | 70.11 | 20.30 |
   | [Liu and Li (2016)](https://arxiv.org/pdf/1609.06380.pdf) | 36.70 | 54.48 | 70.43 | 38.84 |
   | [Chen et al. (2016a)](https://aclweb.org/anthology/P/P16/P16-1163.pdf) | 40.17 | 54.76 | -     | 31.32 |
   | Ours                                     | 40.87 | 54.56 | 72.38 | 36.20 |

2. [A Stacking Gated Neural Architecture for Implicit Discourse Relation Classification](http://anthology.aclweb.org/D/D16/D16-1246.pdf)

3. [Automatic sense prediction for implicit discourse relations in text](http://www.aclweb.org/anthology/P/P09/P09-1077.pdf) _Pitler, 2009_

   This is the first paper which reports result on classifying naturally occurring **implicit** relations in text.
   Key point: semantic word pairs, also using the features like Inquirer Tags, Number, text spans(N-grams), with TextRels knowledge, Verbs, First words/end words, modality, context.

4. [Implicit Discourse Relation Detection via a Deep Architecture with Gated Relevance Network](https://aclweb.org/anthology/P/P16/P16-1163.pdf)

   Calculating the crossing-score between the hidden vector of the source sentences. pre-trained embedding layer. Vocabulary: top 1w words.

5. [Predicting Discourse Connectives for Implicit Discourse Relation Recognition](https://www.comp.nus.edu.sg/~tancl/publications/c2010/Discourse-coling2010-Final.pdf)

6. [Variational Neural Discourse Relation Recognizer](https://arxiv.org/pdf/1603.03876.pdf)

   [Recommend reading](https://jaan.io/what-is-variational-autoencoder-vae-tutorial/)

### Other related work

1. [Discourse Parsing with Attention-based Hierarchical Neural Networks](https://pdfs.semanticscholar.org/6cf7/67e3afcea890e759d4f07fd1620b3f3684c7.pdf)

2. Improving the inference of implicit discourse relations via classifying explicit discourse connectives.

   break point: data sparsity problem -> pervious work assumes the relation is same when the connective words are omitted. ->  the assume is too strong in many cases. -> find the explicit discourse data by using omission rate and context differential.    

   ​

## experiment

1. simple RNN

   google-300

   Embedding: [Word representations: A simple and general method for semi-supervised learning](http://www.aclweb.org/anthology/P10-1040)

## Track

WWW: ddl (10.26;10.31)

**Intelligent and Autonomous systems on the Web** senior program committee: Hui Xiong
**WEB CONTENT ANALYSIS,SEMANTICS, AND KNOWLEDGE** program committee: Hui Xiong
**WEB SEARCH AND MINING** TBD



## Draft: 9+x(references)

#### introduction:

1. introduce what is the discourse relation, it's support many more application such as QA, text summarization, information extraction, machine translation, sentiment analysis etc

2. there are explicit/implicit relation, the explicit discourse relation contain the explicitly with connectives words like 'but','however', the implicit don't contained those words: show as below figures.

3. the explicit discourse relation is more easy to detect than implicit, and achieve the better accuracy, due to with the connectives words are easy to guess the relation between two span text. for example, with connective word "because" is strong indicator the relation between the two arguments is Contingency.

4. implicit relation is a very challenging task, it's given limited amount of annotated data to learn the model understand the two arguments meaning to detect the discourse relation, it must capture latent semantic and logical relationship between two arguments. 

5. there are lots of work based on feature based methods, most recently, many works based on neural based works build the end-to-end systems on implicit discourse relation detect. although, the neural based works shown the effective on this task, there is still space for improving.

6. due to the limited amount of annotated data, many more works try to create labeled data automatically by removing the connective words from explicit example, as additional training data, however it has meaning shifts problem, for example in figure, with/without the "**" has different relation, recent works on filtering noise via domain adaption, multi-task learning, discourse-specific word embedding. 

7. We propose a new neural model on this task, and build a semi-supervising approach using the explicit data/unlabeled data - Adversarial training method.....

8. contribution:  + PDTB data-set.

   ​

#### related work

1. discourse relation supposed many more application: text summarization  <cite> [Yasuhisa][1] </cite>, QA <cite> [Rebecca][2], [Peter][3] </cite>, machine translation <cite> [Thomas][4] </cite>, sentiment analysis <cite>[Subhabrata][5], [Bishan][6]</cite>

   [1]: http://www.aclweb.org/anthology/D/D14/D14-1196.pdf	"Dependency-based Discourse Parser for Single-Document Summarization"
   [2]: http://www.aclweb.org/anthology/N15-1025	"Spinning Straw into Gold: Using Free Text to Train Monolingual Alignment Models for Non-factoid Question Answering"
   [3]: http://www.aclweb.org/anthology/P14-1092	"Discourse Complements Lexical Semantics for Non-factoid Answer Reranking"
   [4]: http://www.aclweb.org/anthology/W13-3303	"Implicitation of Discourse Connectives in (Machine) Translation"
   [5]: https://www.cse.iitb.ac.in/~pb/papers/coling12-discourse-sa.pdf	"Sentiment Analysis in Twitter with Lightweight Discourse Analysis "
   [6]: http://acl2014.org/acl2014/P14-1/pdf/P14-1031.pdf	"Context-aware Learning for Sentence-level Sentiment Analysis with Posterior Regularization"

2. PDTB is one of the largest annotated discourse corpuses, were released in <cite> [Rashmi][7] </cite>, which explicit and implicit instances. annotated from the Wall Street Journal (WSJ) article. This dataset identify the discourse relation of two text spans. To be consistent with the prior works, we recognize the four top level classes : COMPARISON(COMP.), CONTINGENCY (CONT.), EXPANSION(EXP.) and TEMPORAL (TEMP.). To be comparable with exist approaches build 4 binary classifier to identify those relation. We use sections 2-20 as training set, 0-1 as valid set, 0-1 as the testing set.

   [7]: https://www.seas.upenn.edu/~pdtb/papers/pdtb-lrec08.pdf	"The penn discourse treebank 2.0."

3. Various approaches have been proposed in this task. Traditional classification methods directly rely on feature engineering, Many more exist approaches resorts to exploring linguistically informed
   features <cite> [Emily][9] </cite> start using the lexical features and other rich features like polarity tags, Levin verb classes, length of verb phrases, <cite>[Lin][10]</cite> design the syntactic features. Later, lots of approaches force on introducing more effective features, <cite>[Zhi-Min][8] </cite> used the predicting connective words as the the extra features, <cite>[Attapol][11]</cite> add the Brown cluster pair features. Or <cite> [Joonsuk][12] </cite> improve the performance by optimizing the feature set. However, those approaches has relied on hand-crafted features and it's hard to recover the discourse relations root in semantics from surface level features, therefore these approaches did not have the satisfactory performance and those work using the discrete features, it lead to data sparsity.  

   [8]: http://www.aclweb.org/anthology/C10-2172	"Predicting Discourse Connectives for Implicit Discourse Relation Recognition"
   [9]: http://www.aclweb.org/anthology/P09-1077	"Automatic sense prediction for implicit discourse relations in text"
   [10]: http://delivery.acm.org/10.1145/1700000/1699555/p343-lin.pdf?ip=222.195.92.128&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;id=1699555&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;acc=OPEN&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;key=BF85BBA5741FDC6E%2EA4F9C023AC60E700%2E4D4702B0C3E38B35%2E6D218144511F3437&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;CFID=797415270&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;CFTOKEN=77313517&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;__acm__=1502787238_92b4d95a2991494d808e6254d39970ae	"Recognizing Implicit Discourse Relations in the Penn Discourse Treebank"
   [11]: http://www.anthology.aclweb.org/E/E14/E14-1068.pdf	"Discovering Implicit Discourse Relations Through Brown Cluster Pair"
   [12]: https://www.cs.cornell.edu/home/cardie/papers/SIGDIAL12-Improving.pdf	"Improving Implicit Discourse Relation Recognition Through Feature Set Optimization"

4. With the neural model have been proved the effective for NLP in many tasks (<cite> [Dzmitry][13], [Alexander][14], [Yoon][15] </cite>),  also including the discourse relation analysis, those approach build a end-to-end system that avoiding costly feature engineering and shown their result better than traditional linear model. To fight against the data sparsity problem, <cite>[Biao][16]</cite> use word embedding to replace words into the word vectors in the text segment and build a simple neural model which only contain one simple convolution layer above the word vector. In order to  preserve the contextual information, <cite>[Jifan][18]</cite> encode the text segment to its positional representation via a recurrent neural network and propose a gated relevance network to overcome the semantic gap. <cite>[Lianhui][17]</cite> propose a stacking neural network model and achieve competitive performance. With using the implicit connective words which have been annotated for implicit examples, <cite>[Lianhui][26]</cite> propose a adversarial framework to learn the implicit discourse relation, even though without access to connectives words. Above approach avoiding costly feature engineering.

   [26]: https://arxiv.org/pdf/1704.00217.pdf	"Adversarial Connective-exploiting Networks for"
   [13]: https://arxiv.org/pdf/1409.0473.pdf	"NEURAL MACHINE TRANSLATION BY JOINTLY LEARNING TO ALIGN AND TRANSLATE"
   [14]: https://arxiv.org/pdf/1509.00685.pdf	"A Neural Attention Model for Abstractive Sentence Summarization"
   [15]: http://www.aclweb.org/anthology/D14-1181	"Convolutional Neural Networks for Sentence Classification"
   [16]: https://aclweb.org/anthology/D/D15/D15-1266.pdf	"Shallow Convolutional Neural Network"
   [17]: http://anthology.aclweb.org/D/D16/D16-1246.pdf	"A Stacking Gated Neural Architecture"
   [18]: https://aclweb.org/anthology/P/P16/P16-1163.pdf	"Implicit Discourse Relation Detection via a Deep Architecture with Gated Relevance Network"

5. Due to the limited amount of implicit training data, some approaches resort to additional data which are automatically obtained from explicit examples in which connective is removed<cite>[Daniel][19]</cite>. With this method it can create large amounts of additional implicit data from raw texts. However, those data set have the meaning shifts in some cases, for example in figures xxx, <cite>[Caroline][20]</cite> shown the system trained on this type data does not generalize well compared with the system trained on natural data. To overcome this issue, there are some recent works have make some efforts, <cite>[Chloé][22],[Yangfeng][21]</cite> use the domain adaptation, <cite>[Man][23],[Changxing][25]</cite> use the multi-task learning, <cite>[Attapol][25]</cite> classifying connectives that  can be dropped independently of the context without changing the interpretation of the discourse. Our approach base on .. have .., 

   [19]: https://pdfs.semanticscholar.org/ba81/b31598b85259b20399e485a1ab156db5511f.pdf	"An Unsupervised Approach to Recognizing Discourse Relations"
   [20]: http://www.research.ed.ac.uk/portal/files/7946297/Using_automatically_labelled_examples_to_classify.pdf	"Using automatically labelled examples to classify"
   [21]: http://aclweb.org/anthology/D/D15/D15-1264.pdf	"Closing the Gap: Domain Adaptation from Explicit to Implicit Discourse Relations"
   [22]: http://www.aclweb.org/anthology/C14-1160	"Combining Natural and Artificial Examples to Improve Implicit Discourse Relation Identification"
   [23]: http://www.aclweb.org/anthology/P13-1047	"Leveraging Synthetic Discourse Data via Multi-task Learning for Implicit"
   [24]: http://ac.els-cdn.com/S092523121730468X/1-s2.0-S092523121730468X-main.pdf?_tid=acaec15c-8261-11e7-a3fa-00000aacb360&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;acdnat=1502874348_246bdf88b0c03ecf226dc5be7d5d792a	"Leveraging bilingually-constrained synthetic data via multi-task neural"
   [25]: http://www.cs.brandeis.edu/~tet/papers/N15-1081.pdf	"Improving the Inference of Implicit Discourse Relations via Classifying"


1. introduce the adversarial training. The adversarial method success in deep generative modeling <cite>[Goodfellow][27],[Mehdi][28]<cite>, domain adaption<cite>[Yaroslav][29]</cite> and use adversarial example to improve the Robustness of the deep discriminant model <cite>[Goodfellow][30]</cite>. As far as we know, only <cite>[Lianhui][26]</cite> try to use the adversarial method in implicit discourse analysis, and our adversarial framework is total different with them. The main idea of their work is approximating the feature representation spaces without implicit connectives to the other feature representation spaces with implicit connectives. Our system is using the adversarial method to build a semi-supervising system that using the explicit examples to improve the performance of the implicit discourse recognize system. 

   [27]: https://arxiv.org/pdf/1406.2661.pdf	"Generative adversarial nets"
   [28]: https://arxiv.org/pdf/1411.1784.pdf	"Conditional Generative Adversarial Nets"
   [29]: http://www.jmlr.org/papers/volume17/15-239/15-239.pdf	"Domain-Adversarial Training of Neural Networks"
   [30]: https://arxiv.org/pdf/1412.6572.pdf	"EXPLAINING AND HARNESSING adversarial examples"

#### Cases study

##### Implicit:

relation_type: **Contingency**
arg_1: Economists consider that a sign that inflationary pressures are abating
relation: because
arg_2: When demand is stronger than suppliers can handle and delivery times lengthen, prices tend to rise

[Economists consider that a sign that inflationary pressures are abating]<sub>*Arg1*</sub> <u>Implicit=because</u> [When demand is stronger than suppliers can handle and delivery times lengthen, prices tend to rise】<sub>*Arg2*</sub>

##### Explicit:

relation_type: **Expansion**
arg_1: that Seymour is the chief designer of the Cray-3
relation: and
arg_2: without him it could not be completed

[Seymour is the chief designer of the Cray-3]<sub>*Arg1*</sub> <u>and</u> [without him it could not be completed]<sub>*Arg2*</sub>

remove the connective is can be belong to **Contingency** relation. guess: therefor



#### Approach

1. ​
2. ​

#### Experiments

1. The unbalanced sample distribution of PDTB 2.0

​      V1.0  one connective multi-relation , one sentence multi-relation 

| “CLASS”       | train | valid | test |
| :------------ | ----- | ----- | ---- |
| “TEMPORAL”    | 760   | 64    | 85   |
| “CONTINGENCY” | 3340  | 292   | 279  |
| “COMPARISON”  | 1943  | 197   | 152  |
| “EXPANSION”   | 7010  | 671   | 574  |

​      V2.0  one connective one relation, one sentence multi-relation

| “CLASS”       | train | valid | test |
| :------------ | ----- | ----- | ---- |
| “TEMPORAL”    | 689   | 56    | 70   |
| “CONTINGENCY” | 3288  | 288   | 276  |
| “COMPARISON”  | 1898  | 194   | 146  |
| “EXPANSION”   | 6900  | 659   | 563  |

​      V3.0  one connective one relation, one sentence one relation

| “CLASS”       | train | valid | test |
| :------------ | ----- | ----- | ---- |
| “TEMPORAL”    | 665   | 54    | 68   |
| “CONTINGENCY” | 3281  | 287   | 287  |
| “COMPARISON”  | 1894  | 191   | 146  |
| “EXPANSION”   | 6792  | 651   | 556  |

​      V4.0  one connective one relation, one sentence one relation, valid data(0,1,23,24), same as <cite>[Jifan][18]</cite>

| “CLASS”       | train | valid | test |
| :------------ | ----- | ----- | ---- |
| “TEMPORAL”    | 665   | 93    | 68   |
| “CONTINGENCY” | 3281  | 628   | 287  |
| “COMPARISON”  | 1894  | 401   | 146  |
| “EXPANSION”   | 6792  | 1253  | 556  |

1. additional data, explicit discourse example

| “CLASS”       | total |
| :------------ | ----- |
| “TEMPORAL”    | 665   |
| “CONTINGENCY” | 3250  |
| “COMPARISON”  | 5471  |
| “EXPANSION”   | 6792  |