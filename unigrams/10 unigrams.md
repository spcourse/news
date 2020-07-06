# Unigrams

## Goal

Write a program called `classify_unigram.py` that can determine relevant categories for a newspaper article.

## Example

The directory `articles` contains an article called `cooking veggies` from HuffPost on the question: is better to cook vegetables or eat them raw? The tool you're going to write should be able to determine the topics of this article:

    # python classify_unigram.py "articles\cooking veggies.txt"
    FOOD & DRINK             2323
    TASTE                    2157
    WELLNESS                 1449
    HEALTHY LIVING           1172
    SCIENCE                  1041

As you can see, the location of the text file is provided by the first command line argument. The output are the top five categories related to the article. The scores reflect how related the categories are (higher = better).

## Data

For this exercise we have to take a look at the `data` directory. It contains two subdirectories:

* `unigrams`: Contains the word lists for each category. These will be used for this exercise.
* `bigrams`: This directory will be used in the next assigment. We will ignore it for now.

## Unigrams

The directory `unigrams` contains 41 files ( `ARTS.csv`, `BUSINESS.csv`, `TASTE.csv`, etc.), all these files contains lists of single words (surprisingly called unigrams) and scores pertaining to the category. For example the file `TRAVEL.csv` contains the lines:

    overtourism,17
    airfares,17
    lagoons,17
    lençóis,17
    ...
    saltwater,10
    floridian,10
    croatian,10
    ...

These are just a couple of examples lines, the entire file contains many, many more. Every line contains a keyword, related to the topic and a score reflecting how strongly related it is (separated by a comma). So, the word 'overtourism' (with a score of 17) is more strongly related to 'TRAVEL' than 'croatian' (with a score of 10).

These unigrams are compiled by analyzing many tens of thousands of articles from HuffPost ([News Category Dataset](https://www.kaggle.com/rmisra/news-category-dataset)). You don't have to know the unigrams are generated, but the underlying principle is called Naive Bayes Classification. If you're interested you can have a look at [Andrew Ng's explanation on this subject](https://www.youtube.com/watch?v=z5UQyCESW64) (some familiarity with probability theory required).

## Scores

Using the scores in the word list above you can compute the total score for a category for a given article. For example, if we would have the text: "Overtourism in Croatian saltwater", we could compute the **total category score** for the `travel` category by adding up the scores for each word: 17 + 0 + 10 + 10 = 37 (assuming the word 'in' is not in the `travel` unigram list).

In general, the total category score for an article given a category is computed by looking up all the words of the article in the category unigram list and adding up all the scores. If a word is not in the unigram list, the score is assumed to be 0.

## Specification

* Create a program called `classify_unigram.py` that can read a text file provided as command line argument.
* Read and tokenize the text file.
* Read the unigram files and store the data in dictionaries.
* Use the unigram dictionaries and the tokenized text to compute the total category score for every category. Don't use any `for`-loops for *this* step, instead use the functions `my_map`, `my_filter`, and `my_reduce`.
* Print a sorted list with the 5 highest scoring categories for the text. (The formatting should be the same as shown above.)

### Tips

* If you cannot figure out how to avoid using a loop, write the program with loops first. Try to replace them with  `my_map`, `my_filter`, and `my_reduce `later.
