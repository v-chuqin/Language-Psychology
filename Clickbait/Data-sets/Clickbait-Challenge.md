# [Clickbait Challenge 2017](http://www.clickbait-challenge.org/)

### Important Dates:

| Date                     | event                          |
| ------------------------ | ------------------------------ |
| March 31, 2017           | Registration begins.           |
| March 31, 2017           | Release of training dataset.   |
| May 31, 2017             | Release of validation dataset. |
| July 10 -- July 31, 2017 | Software evaluation phase.     |
| August 01, 2017          | Result Notifications.          |
| August 31, 2017          | Paper submission deadline.     |
| September 14, 2017       | Notification of acceptance.    |
| September 28, 2017       | Camera-ready deadline.         |
| TBD, 2017                | Workshop.                      |

 ### Example

[Some people are such food snobs](https://www.washingtonpost.com/news/wonk/wp/2015/06/11/some-people-are-such-food-snobs/?utm_term=.b5649733e9e7)

```json
// Input
{
 "id": "608999590243741697",
 "postTimestamp": "Thu Jun 11 14:09:51 +0000 2015",
 "postText": ["Some people are such food snobs"],
 "postMedia": ["608999590243741697.png"],
  "targetTitle": "Some people are such food snobs",
 "targetDescription": "You'll never guess one...",
 "targetKeywords": "food, foodfront, food waste...",
 "targetParagraphs": [
   "What a drag it is, eating kale that isn't ...",
   "A new study, published this Wednesday by ...", 
   ...],
 "targetCaptions": ["(Flikr/USDA)"]
 }
```

```json
// Classifiers have to output a clickbait score in the range [0,1], where a value of 1.0 denotes that a post is heavily click baiting.
{"id": "608999590243741697", "clickbaitScore": 1.0}
```

```json
//The posts in the training and test sets have been judged on a 4-point scale [0, 0.3, 0.66, 1] by at least five annotators.
{
   "id": "608999590243741697", 
   "truthJudgments": [0.33, 1.0, 1.0, 0.66, 0.33],
   "truthMean"  : 0.6666667,
   "truthMedian": 0.6666667,
   "truthMode"  : 1.0,
   "truthClass" : "clickbait"
}
```

### Download 

[Training](http://www.uni-weimar.de/medien/webis/corpora/corpus-webis-clickbait-16/clickbait17-train-170331.zip)

[Unlabeled](http://www.uni-weimar.de/medien/webis/corpora/corpus-webis-clickbait-16/clickbait17-unlabeled-170429.zip)

[Validation](http://www.uni-weimar.de/medien/webis/corpora/corpus-webis-clickbait-16/clickbait17-validation-170616.zip)

