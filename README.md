# EBugs in Cloud Systems

This repository contains a dataset of 210 exception-related bugs, also denoted
as ***eBugs***, curated from six widely deployed cloud systems, including
Cassandra, HBase, HDFS, Hadoop MapReduce, YARN, and ZooKeeper. The repository
also contains a list of *inaccurate exceptions*\* detected by ***DIET***, a
static analysis tool that detects inaccurate exceptions by finding
inconsistency between an exception's class and its error message.

*\* Please refer to our paper (see below) for the definition of inaccurate
exceptions and other types of eBugs.*

## The eBugs dataset

The [eBugs dataset](https://github.com/hanseychen/eBugs/blob/master/eBugs.xlsx)
contains 210 exception-related bugs. These bugs are selected from more than
60,000 JIRA issues, which were submitted for the six studied cloud systems from
2007 to 2018. Every eBug is studied from multiple perspectives to answer the
following key research questions:

- **RQ1:** How are eBugs triggered in cloud systems?
- **RQ2:** What is the relation between the triggering conditions and the root
causes of eBugs?
- **RQ3:** What are the impacts of eBugs on cloud systems?

Please check out our paper (see below) for detailed statistics of each
perspective, as well as the findings and implications on them.

## DIET - **D**etecting **I**naccurate **E**xceptions using triggering condition **T**ypes

Based on the findings on the eBugs dataset, we design and implement a static
analysis tool, called DIET, to detect an important class of eBug, i.e.,
inaccurate exception. From a high level perspective, DIET detects inaccurate
exceptions by understanding an exception's class and error message. If the
class and the error message imply different types of triggering conditions,
DIET will flag the exception as an inaccurate one.

Please refer to our paper for more details about how DIET works.

## Inaccurate exceptions detected by DIET

We apply DIET to the latest versions of the studied systems, and find 31
inaccurate exceptions. Two of them are eBugs that cause failure symptoms.
The remaining 29 inaccurate exceptions are bad practices, where their classes
and error messages are indeed inconsistent. We submit them to the developers of
these systems. At the time of writing, developers have confirmed 23 of them.
Moreover, all of the confirmed inaccurate exceptions are previously-unknown.
Below is the list of all confirmed inaccurate exceptions. You can find more
details in both the
[dataset](https://github.com/hanseychen/eBugs/blob/master/eBugs.xlsx)
and our paper.

## Publication

[ASE'19] *Understanding Exception-Related Bugs in Large-Scale Cloud Systems*.
Haicheng Chen, Wensheng Dou, Yanyan Jiang, and Feng Qin.
