# Parsing Text Using Map-Reduce Programming Model

### TABLE OF CONTENTS
* [Objective](#objective)
* [Technologies](#technologies)
* [Data](#data)
* [Map-Reduce](#map-reduce)
* [Implementation](#implementation)
* [Results](#results)

## OBJECTIVE 
Perform processing of text and count the occurence of each word using map-reduce concept amd mimic Hadoop infrastructure with parallel processing. Multi-threading is used to execute two mapper and reducer functions.

## TECHNOLOGIES
Project is created with: 
* Python - Multi-Threading

## DATA
The data is made available [here](https://github.com/skotak2/Pasrsing-Text-with-MapReduce-programming-Paradigm-with-multithreading/blob/master/Data/Data.txt)

![GitHub Logo](https://github.com/skotak2/Pasrsing-Text-with-MapReduce-programming-Paradigm-with-multithreading/blob/master/Images/input.jpg)

## MAP REDUCE

Consider the following Text - "I am a human being. I am a Data Scientist"

<ins>MAP</ins> : Read Input and produce a set of key value pairs

**(I,1)
(am,1)
(a,1)
(human,1)
(being,1)
(I,1)
(am,1)
(a,1)
(Data,1)
(Scientist,1)**

<ins>GroupBy</ins> : Collect all pairs with same key

**(I,1),(I,1) | (am,1),(am,1) | (a,1),(a,1) | (human,1),(being,1) | (Data,1),(Scientist,1)**

<ins>Reduce</ins> : Collect all values belonging to the key & output

**(I,2) | (am,2) | (a,2) | (human,1) | (being,1) | (Data,1) | (Scientist,1)**

Here we implement the concept of multithreading, to parallelize the process. Map Reduce is divided into sub tasks in parallel & aggregate teh results of sub-totals to final output. The process of mapping key to value and further aggregating them through reducers is achieved by the theards.


## IMPLEMENTATION

With the above concept in place, we implement the setup in the following steps:

*Step1* : Map for key value pairs with multiple mappers

*Step2* : Sort the values and load in to the partition holder

*Step3* : Multiple Reducers to pic from the partition and aggregate them

The above steps will yield a list of outputs from the reducer, which could be concatenated and loaded into a datafram or a spreasheet


## RESULTS
The deployed model can be accessed from the url from any system to translate kannada sentences to english. 

![GitHub Logo](https://github.com/skotak2/Pasrsing-Text-with-MapReduce-programming-Paradigm-with-multithreading/blob/master/Images/output.jpg)

