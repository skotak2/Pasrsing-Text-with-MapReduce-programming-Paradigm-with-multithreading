# Parsing Text Using Map-Reduce Programming Model

The evolution of big data systems is based on the foundational programming paradigm of Map-Reduce, involving high scale computation of data processing on a network of comodity hardware.This project is to illustrate on implementation of map-reduce and parallelize the process.

<ins>**Concept of Map-Reduce**</ins>:

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

<ins>**Implementation:**</ins>

With the above concept in place, we implement the setup in the following steps:

**Step1** : Map for key value pairs with multiple mappers

**Step2** : Sort the values and load in to the partition holder

**Step3** : Multiple Reducers to pic from the partition and aggregate them

The above steps will yield a list of outputs from the reducer, which could be concatenated and loaded into a datafram or a spreasheet
