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
these systems in the form of JIRA issues. We group the eBugs and bad practices
that are in the same file into the same JIRA issue. At the time of writing,
developers have confirmed the two eBugs and 21 bad practices. Moreover, all of
the confirmed inaccurate exceptions are previously-unknown. Below is the list
of all the confirmed eBugs and bad practices. We only list one instance of
HDFS-14467 and one instance of HDFS-14468 because all the bugs in these two
issues have the same exception class and error message. You can find more
details about the detected eBugs and bad practices in both the
[dataset](https://github.com/hanseychen/eBugs/blob/master/eBugs.xlsx)
and our paper.

System | Exception Class | Error Message | Triggering Condition | Created Issue | Issue Type
-------|-----------------|---------------|----------------------|---------------|-----------
Cassandra (3.11) | RuntimeException | "Interrupted while waiting for stream/fetch ranges to finish" | untimely interrupt | [CASSANDRA-15111](https://issues.apache.org/jira/browse/CASSANDRA-15111) | bad practice
Cassandra (3.11) | RuntimeException | "Interrupted while waiting on rebuild streaming" | untimely interrupt | [CASSANDRA-15112](https://issues.apache.org/jira/browse/CASSANDRA-15112) | bad practice
Cassandra	(3.11) | RuntimeException | "Node interrupted while decommissioning" | untimely interrupt | [CASSANDRA-15113](https://issues.apache.org/jira/browse/CASSANDRA-15113) | bad practice
Cassandra (3.11) | RuntimeException | "Not enough space to write ... to ... (... available)" | out of resource | [CASSANDRA-15114](https://issues.apache.org/jira/browse/CASSANDRA-15114) | bad practice
Cassandra (3.11) | RuntimeException | "Not enough disk space to store ..." | out of resource | [CASSANDRA-15114](https://issues.apache.org/jira/browse/CASSANDRA-15114) | bad practice
Cassandra (3.11) | RuntimeException | "Failed to create failed snapshot tracking file \[...\]. Aborting" | file system error | [CASSANDRA-15115](https://issues.apache.org/jira/browse/CASSANDRA-15115) | bad practice
Cassandra (3.11) | RuntimeException | "Unable to create directory:" | file system error | [CASSANDRA-15116](https://issues.apache.org/jira/browse/CASSANDRA-15116) | bad practice
Cassandra (3.11) | RuntimeException | "Unable to list directory:" | file system error | [CASSANDRA-15117](https://issues.apache.org/jira/browse/CASSANDRA-15117) | bad practice
Hadoop (3.1.2) | DiskErrorException | "Invalid value configured for" | semantic condition | [HDFS-14467](https://issues.apache.org/jira/browse/HDFS-14467) | bad practice
Hadoop (3.1.2) | DiskErrorException | "Invalid value configured for" | semantic condition | [HDFS-14468](https://issues.apache.org/jira/browse/HDFS-14468) | bad practice
Hadoop (3.1.2) | DiskErrorException | "Invalid value configured for" | semantic condition | [HDFS-14469](https://issues.apache.org/jira/browse/HDFS-14469) | bug
Hadoop (3.1.2) | DiskErrorException | "Invalid value configured for" | semantic condition | [HDFS-14470](https://issues.apache.org/jira/browse/HDFS-14470) | bad practice
Hadoop (3.1.2) | IOException | "Interrupted receiveBlock" | untimely interrupt | [HDFS-14473](https://issues.apache.org/jira/browse/HDFS-14473) | bad practice
Hadoop (3.1.2) | IOException | "replaceFile interrupted." | untimely interrupt | [HADOOP-16295](https://issues.apache.org/jira/browse/HADOOP-16295) | bug
Hadoop (3.1.2) | RuntimeException | "Cannot create directory" | file system error | [HADOOP-16296](https://issues.apache.org/jira/browse/HADOOP-16296) | bad practice
Hadoop (3.1.2) | RuntimeException | "Specified work directory does not exists" | file system error | [HADOOP-16297](https://issues.apache.org/jira/browse/HADOOP-16297) | bad practice
Hadoop (3.1.2) | YarnException | "Interrupted while retrying to connect to ATS" | untimely interrupt | [YARN-9533](https://issues.apache.org/jira/browse/YARN-9533) | bad practice
Hadoop (3.1.2) | YarnException | "Interrupted while trying to connect ATS" | untimely interrupt | [YARN-9534](https://issues.apache.org/jira/browse/YARN-9534) | bad practice

## Publication

[ASE'19] *Understanding Exception-Related Bugs in Large-Scale Cloud Systems*.
Haicheng Chen, Wensheng Dou, Yanyan Jiang, and Feng Qin.
