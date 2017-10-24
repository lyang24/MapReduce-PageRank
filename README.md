# MapReduce PageRank

I deploy this project with a hadoop cluster on Docker.

### Main Steps

  Build a pagerank Libraray from wiki data sets.

  According to the transmition matrix build a relationship model between webpages.

  According to the pagerank matrix calculate the weight between webpages.

  Using teleporting to solve two edge case problems:Spider traps and Dead ends.

  Using Python httpserver to show the result.

raw data from https://www.limfinity.com/ir/

### Data preprocessing

I preprocessed the original dataset in two steps:

Give every website a tag, mapping the tag to every website.

Change the data in each pagelink file into the following format: frompage-id topage-id.

### Technical details:

  mr1_mapper1: use relation.txt to generate transition matrix cell

  mr1_mapper2: use PageRank.txt to generate pagerank matrix cell

  mr1_reducer: calculate results of matrix cell * pagerank cell

  mr2_mapper1: read file generated from last mapreduce

  mr2_mapper2: teleporting:read pageRank_i.txt, which will add beta*e to result sum

  mr2_reducer: sum up cell for each page

  $ hadoop com.sun.tools.javac.Main *.java
  $ jar cf ngram.jar *.class
  $ hadoop jar pr.jar Driver /transition /pagerank /output 5 0.8
  
  args0: dir of transition.txt
  args1: dir of PageRank.txt
  args2: dir of unitMultiplication result
  args3: times of convergence
  args4: value of beta
