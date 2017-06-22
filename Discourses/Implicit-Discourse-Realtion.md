# Implicit Discourse Relation

## Data-set

### PDTB-2.0

1. Penn Discourse TreeBank 2.0](https://www.seas.upenn.edu/~pdtb/papers/pdtb-lrec08.pdf) describing its lexically-grounded annotations of discourse relations and their two abstract object arguments over the 1 million word Wall Street Journal corpus. 

2. This data-set can be broadly characterized into __two types__: 
   * **Explicit**

     *  subordinating conjunctions (e.g., because, when, etc.)

         > E.g., Michelle lives in a hotel room, and **although** she drives a canary-colored Porsche, she hasn’t time to clean or repair it.

     *   coordinating conjunctions (e.g., and, or, etc.)

     *  discourse adverbials (e.g., for example, instead, etc.)
   * **Implicit**
     > E.g., But a few funds have taken other defensive steps. Some have raised their cash positions to record levels. **Implicit = BECAUSE** High cash positions help buffer a fund when the market falls.

   * AltLex: express an inferred elation led to a redundancy
     > E.g., Ms. Bartlett’s previous work, which earned her an international reputation in the non-horticultural art world, often took gardens as its nominal subject. **AltLex** <u>Mayhap this metaphorical connection made</u> the BPC Fine Arts Committee think she had a literal green thumb
   * EntRel: entitybased coherence

      > E.g., Hale Milgrim, 41 years old, senior vice president, marketing at Elecktra Entertainment Inc., was named president of Capitol Records Inc., a unit of this entertainment concern. **EntRel** <u>Mr. Milgrim succeeds David Berman, who resigned last month.</u>

   * NoRel: no discourse relation or entity-based relationt

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

   | “CLASS” Explicit (18459) | Implicit (16224) | AltLex (624) | Total |
   | :----------------------- | ---------------- | ------------ | ----- |
   | TEMPORAL                 | 3612             | 950          | 88    |
   | CONTINGENCY              | 3581             | 4185         | 276   |
   | COMPARISON               | 5516             | 2832         | 46    |
   | EXPANSION                | 6424             | 8861         | 221   |
   | **Total**                | 19133            | 16828        | 634   |

5. Download from https://catalog.ldc.upenn.edu/LDC2008T05 / https://github.com/cgpotts/pdtb2

   ​
