# Summary #

sbvj is a library for succinct bit vector written in Java.The rank and select functions are defined as follows.Given a static bit vector B of bits numbered from 0 to n - 1,

  * rank1\_B(x): Counts the number of 1's up to and excluding the position x in B.
  * select1\_B(y): Finds the position of the (y + 1)th 1bit in B.

# Requirement #

Java7 or later.

# Usage #

## Simple/Dense ##

  * rank in constant time
  * select in O(lg(n)) time

```
// create succinct bit vector.
SuccinctBitVector sbv = new SuccinctBitVector(10);

// set bit.
sbv.setBit(5, 1);

// print bit vector.
sbv.print();

// create auxiliary data structure.
sbv.build(BuildType.SIMPLE);

// get rank value.
long rank = sbv.getRank(6, 1);

// get select value.
long select = sbv.getSelect(0, 1);

// get serialized data.
SuccinctBitVectorData sbvData = sbv.getData();

// get succinct bit vector from serialized data.
SuccinctBitVector newSBV = new SuccinctBitVector(sbvData);
```

## Sparse ##

  * rank in constant time(worst case: O(2^lg(n/m)))
  * select1 in constant time
  * select0 in O(lg(m)) time

m: the number of 1's

```
// create auxiliary data structure.
sbv.build(BuildType.SPARSE);

// get rank value.
long rank = sbv.getRank(6, 1);

// get select value.
long select = sbv.getSelect(0, 1);
```

## CS ##

CS is a implementation of plain bitmaps using "combined sampling".

coming soon.

## CS\_RRR ##

CS\_RRR is a implementation of compressed bitmaps that achieve excellent time performance for rank and select queries.

Combined Sampling + RRR(on the fly)

  * rank in constant time
  * select1 in constant time
  * select0 in constant time

RRR block: t = 63

sampling rank: s = 32 × t

sampling select: 4096

```
// create auxiliary data structure.
sbv.build(BuildType.CS_RRR);

// get rank value.
long rank = sbv.getRank(6, 1);

// get select value.
long select = sbv.getSelect(0, 1);
```

## Re-Pair ##

coming soon.

## Select in constant time ##

  * rank in constant time
  * select in constant time

```
// create auxiliary data structure.
sbv.build(BuildType.SELECT1_IN_CONSTANT_TIME);
// finds the position of 1th 1 bit in bit vector.
long select = sbv.getSelect(0, 1);

or

// create auxiliary data structure.
sbv.build(BuildType.SELECT0_IN_CONSTANT_TIME);
// finds the position of 1th 0 bit in bit vector.
long select = sbv.getSelect(0, 0);

or

// create auxiliary data structure.
sbv.build(BuildType.SELECT_IN_CONSTANT_TIME_FULL);
```

# Reference #

The following blog article is a description of basic function for sbvj. However, Japanese version only.

http://d.hatena.ne.jp/ryokkie/20120328/1332951451

Also, I referred to the following paper.

### Simple/Dense ###
  * PRACTICAL IMPLEMENTATION OF RANK AND SELECT QUERIES, Rodrigo Gonzalez, WEA, 2005.
    * link:http://goanna.cs.rmit.edu.au/~e76763/tiger_ref/ggmn05-wea.pdf

### Select in constant time ###
  * Fast Computation of Rank and Select Functions for Succinct Representation, Joong Chae NA, IEICE, 2009.
    * link:http://ci.nii.ac.jp/naid/10026811627
  * Compressed Full-Text Indexes, Gonzalo Navarro, ACM COMPUTING SURVEYS, 2007.
    * link:http://www.cs.helsinki.fi/u/vmakinen/papers/survey.pdf

### Sparse ###
  * 高速文字列解析の世界, 岡野原大輔, 岩波書店, 2012.
    * link:http://www.iwanami.co.jp/.BOOKS/00/8/0069740.html

### CS/CS\_RRR ###
  * Fast, Small, Simple Rank/Select on Bitmaps, Gonzalo Navarro,SEA'12, 2012.
    * link:http://www.dcc.uchile.cl/~gnavarro/ps/sea12.1.pdf
  * Space-Efficient, High-Performance Rank & Select Structures on Uncompressed Bit Sequences, Dong Zhou, SEA'13, 2013.
    * link:http://www.cs.cmu.edu/~dga/papers/zhou-sea2013.pdf

### Re-Pair ###
  * Practical Compressed Document Retrieval, Gonzalo Navarro, SEA'11, 2011.
    * link:http://www.dcc.uchile.cl/~gnavarro/ps/sea11.2.pdf
  * Compressed Text Indexes with Fast Locate, Rodrigo Gonzalez, CPM'07, 2007.
    * link:http://www.dcc.uchile.cl/~gnavarro/ps/cpm07.1.pdf
  * Offline Dictionary-Based Compression, N. Jesper Larsson, DCC'99, 1999.
    * link:http://www.larsson.dogma.net/dcc99.pdf
  * Structures of String Matching and Data Compression, N. Jesper Larsson, PhD Thesis, p.95-101, 1999.
    * http://www.larsson.dogma.net/thesis.pdf
  * A fully linear-time approximation algorithm for grammar-based compression, Hiroshi Sakamoto, Journal of Discrete Algorithms, 2005.
    * http://www.sciencedirect.com/science/article/pii/S1570866704000632
  * An Online Algorithm for Lightweight Grammar-Based Compression, Shirou Maruyama, Algorithms 2012, 2012.
    * http://www.mdpi.com/1999-4893/5/2/214
  * General Document Retrieval in Compact Space, Gonzalo Navarro, ACM Journal of Experimental Algorihtmics, 2013.
    * http://www.dcc.uchile.cl/~gnavarro/ps/jea13.pdf