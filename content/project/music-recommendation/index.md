---
slides: example
url_pdf: ""
summary: >-
  T﻿his is a project for music recommendations with Spark.


  * Accelerated parallel breadth-first search with Spark 10x faster than that with MapReduce in the self-deployed cluster after compressing the dataset with a 2% ratio by Apache Avro.

  * Employed the PageRank algorithm within ego-nets to generate divers.
url_video: ""
date: 2022-08-09T00:00:00.000Z
external_link: ""
url_slides: ""
title: Music Recommendation with Spark
tags:
  - Big Data
url_code: "https://github.com/frankling2020/Methods_and_Tools_for_Big_Data"
image:
  caption: ""
  focal_point: Smart
  filename: featured.jpg
url_code: ""
---
## MSD (Million Song Dataset)

The Million Song Dataset is a freely-available collection of audio features and metadata for a million contemporary popular music tracks.

The core of the dataset is the feature analysis and metadata for one million songs, provided by The Echo Nest. The dataset does not include any audio, only the derived features.

## Data Processing

1. Familiarize HDF5 and its related libraries
2. Use Apache Avro and Snappy Codec to compress data
3. Visualize dataset to gain an intuitive knowledge

## Drill and SQL

1. Range of dates covered by the songs
2. The hottest and shortest song with highest energy and lowest tempo
3. Album with the most tracks
4. Band that recorded the longest song

## BFS with Spark

1. Use k-hops to define the similarity
2. Relationship in the Graph (artist, song, similar_artists)
3. Input: Adjacency list (artist, similar_artists)
4. Output: similar artists within k-hop

**Algorithm**

1. Compared with bfs in mapreduce, Spark can implement mapper and reducer function with lambda function.
2. Mark the visited node and the most recently visited (MRV) node.
3. FromMRVnode to visit their neighbours in parallel
4. Mark those neighbours as MRV

**Implementation**

1. use the local variable to record MRV and broadcast to executors
2. use rdd to record how nodes are visited with each record (artist, distance).
3. For bfs part, v1 runs about 6 s, while v2 runs about 1 s with 2GB data.
4. However, when exporting the results to local files, v1 is much faster.

## Diverse Recommendation

1. Use the Page Rank to analyze the sub-graph around one artist
2. Page Rank is a link analysis algorithm measuring the relative importance within the set.
3. Markov chain model: a random walk model to detect the potential interests
4. Implement the graph visualization with networkX and show the potential\
   related artist to the user.

## Conclusion

1. BFS in Spark is much faster than BFS in MapReduce
2. Spark takes full advantage of memory in BFS.
3. From the k-hop graph, we can generally get the relationship between similar\
   artists.
4. The system can recommend the songs from those similar artists to the user.

More related experience with big data tools are shown in [Methods_and_Tools_for_Big_Data ](https://github.com/frankling2020/Methods_and_Tools_for_Big_Data)