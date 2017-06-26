# Automated Student Assessment Prize 

1. [Download](https://www.kaggle.com/c/asap-aes) 

2. Train-set

   > - **essay_id**: A unique identifier for each individual student essay
   >
   > - **essay_set**: 1-8, an id for each set of essays
   >
   > - **essay**: The ascii text of a student's response
   >
   > - **rater1_domain1**: Rater 1's domain 1 score; all essays have this
   >
   > - **rater2_domain1**: Rater 2's domain 1 score; all essays have this
   >
   > - **rater3_domain1**: Rater 3's domain 1 score; only some essays in set 8 have this.
   >
   > - **domain1_score**: Resolved score between the raters; all essays have this
   >
   > - **rater1_domain2**: Rater 1's domain 2 score; only essays in set 2 have this
   >
   > - **rater2_domain2**: Rater 2's domain 2 score; only essays in set 2 have this
   >
   > - **domain2_score**: Resolved score between the raters; only essays in set 2 have this
   >
   > - **rater1\_trait1 score - rater3_trait6 score**: trait scores for sets 7-8


3. Valid-set

   > - **essay_id**: A unique identifier for each individual student essay
   > - **essay_set**: 1-8, an id for each set of essays
   > - **essay**: The ascii text of a student's response
   > - **domain1_predictionid**: A unique prediction_id that corresponds to the predicted_score on the essay for domain 1; all essays have this
   > - **domain2_predictionid**: A unique prediction_id that corresponds to the predicted_score on the essay for domain 2; only essays in set 2 have this

4. Submission-sample

   > - **prediction_id**: A unique identifier for the score prediction, corresponding to the domain1_predictionid or domain2_predictionid columns
   >
   > - **essay_id**: A unique identifier for each individual student essay
   >
   > - **essay_set**: 1-8, an id for each set of essays
   >
   > - **prediction_weight**: This identifies how the prediction is weighted when the mean of the transformed quadratic weighted kappas is taken.  For essay set 2, which is scored in two domains, this is 0.5 so that each essay contributes equally to the final score.  For the remaining essay sets, this is 1.0.
   >
   > - **predicted_score**: This is the score output by your automated essay scoring engine for the specific essay and domain

5. [Named Entity Recognizer (NER)](http://nlp.stanford.edu/software/CRF-NER.shtml). The entitities identified by NER are: "PERSON", "ORGANIZATION", "LOCATION", "DATE", "TIME", "MONEY", "PERCENT"

6. [Benchmark](https://github.com/benhamner/asap-aes)