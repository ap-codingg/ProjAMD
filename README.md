[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1XNlInZ54HkOZSpTXzkrKXIwDtLOFDx2s#scrollTo=6b55aa31)

# Market-basket analysis on the IMDB dataset "Top 1000 Movies by IMDB Rating"

## Introduction
This project applies market-basket analysis to analyze patterns among actors, downloading the IMDB dataset via the Kaggle API. 

By leveraging Spark, the SON algorithm processes the dataset to discover frequent actor itemsets and derive association rules. 

## Summary
- Overview and key features
- Dataset
- Dependencies
- Algorithm and implementations
- How to run

## Overview and key features
Memory efficiency is allowed through the MEMORY_AND_DISK function of Spark and the division of the dataset in partions.

Another important feature is the SON algorithm, which makes possible to be sure that frequent itemsets are not discarded,
since the way it's built does not allow for false negatives.

After the SON is run, the association rules are defined to evaluate the relations between the pairs and triples of frequent actors,
which are visualized in the graph at the end of the code.

## Dataset
The dataset is found at this link https://www.kaggle.com/datasets/harshitshankhdhar/imdb-dataset-of-top-1000-movies-and-tv-shows/code
and contains the top 1000 movies by IMDB rating.

Each row of the dataset is used, since it was already cleaned and corresponds to a movie 
(or basket if we are using the market-basket analysis terms), while the columns used are the ones from "Star1" to "Star4",
which correspond to the first 4 leading actors and to the items of the analysis.

## Algorithm and implementations
First, apriori is run in each partition, so that it's possible to generate the local frequent itemsets.

In the second pass of the SON algorithm the candidates from all partitions are merged and there is the search for 
frequent pairs and triples of frequent actors.

When this pass end, the association rules are formed to see if the frequent pairs and triples occur randomly or not.
Then the visualization takes place to be able to better see the associations between the pairs and triples.

## Dependencies
import pandas as pd

from pyspark.sql import SparkSession

from pyspark import StorageLevel

from pyspark.sql.types import StructType, StructField, StringType, DoubleType, IntegerType

import math

from collections import Counter

from itertools import combinations

import networkx as nx

import matplotlib.pyplot as plt

Python 3.10+
## Running the code
- Set the Kaggle credentials,
- Install the dependencies listed above
- Set, if necessary, the environmental variables, like TARGET_ROWS_PARTITION,
- Launch the notebook by running the cells in order.
