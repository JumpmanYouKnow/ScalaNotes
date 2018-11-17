ScalaNotes
====================
I wrote more than 5000 lines of scala code about 1 year ago, but later on I don't have any chance to write it. (Univeristy doesn't teach it, previous internships don't use it)

Now I'm picking it up as the university teaches spark by scala, but I feel that I forgot lots of not only syntax but also some key knowledge about scala.

Therefore I want to open this repo as my scala notes.



Side Effect
---------------------

### 1. map on iterator no side effect: https://stackoverflow.com/questions/12631778/scala-map-on-iterator-does-not-produce-side-effects

> List(1,2,3,4).iterator.map((x: Int) => println(x))

doesn't print

while

> List(1,2,3,4).map((x: Int) => println(x)) 

> List(1,2,3,4).foreach((x: Int) => println(x))

> List(1,2,3,4).iterator.foreach((x: Int) => println(x))

all do
#### Note:

- map on iterator is lazy, put "toList" in the end will fix it.
- but should use foreach, as it is designed for side effects(won't allow laziness)

### 2.   ==, eq, and equals
- equals in scala is same as equals in java, throw null exception 
- == check for null, then redirect to equals
- eq is scala equivalent to == in java

Examples
- 1 equals 2 will return false, as it redirects to Integer.equals(...)
- 1 == 2 will return false, as it redirects to Integer.equals(...)
- 1 eq 2 will not compile, as it requires both arguments to be of type AnyRef
- new ArrayList() equals new ArrayList() will return true, as it checks the content
- new ArrayList() == new ArrayList() will return true, as it redirects to equals(...)
- new ArrayList() eq new ArrayList() will return false, as both arguments are different instances
- foo equals foo will return true, unless foo is null, then will throw a NullPointerException
- foo == foo will return true, even if foo is null
- foo eq foo will return true, since both arguments link to the same reference 

### 3. A very good command line input parse library
import org.rogach.scallop._
https://github.com/scallop/scallop

### 4. scala split
java split() takes regular expression string as input only: split(String: regex)  
example: split by character '|', we must escape '|', split("\\|")  
split("|") has a semantic meaning of "split  by empty string or split by empty string"  
thus, "abcde" will be split to (a, b, c, d, e)  
  
scala override the split() function  
Split by character: split(Char: c)  
Split by regex: split(String: regex)  




Spark
---------------------
### 1.
pairs.reduceByKey((accumulatedValue: Int, currentValue: Int) => accumulatedValue + currentValue)  
#### Note:
- explicit type, need bracket. reduceByKey((x:type, y:type)=> ... )  

### 2. read parquet files
import org.apache.spark.sql.SparkSession

val sparkSession = SparkSession.builder.getOrCreate

val lineitemDF = sparkSession.read.parquet("TPC-H-0.1-PARQUET/lineitem")

### 3. Scala REPL
spark-shell  
scala >   
default: SparkSession as spark  
SparkContext as sc  

### 4. spark dataframe
#### 1. return rows
 
head(n = 5), default = 5
get first n row

#### 2. return Unit
show(n = 20), default n = 20  
print n rows  
  
show(b = true), default b = true  
print maximum 20 characters for each row if b == true, else no limit  

describe:  
show statistic summary for each column: count, mean, stddev, min, max  
Example: https://img-blog.csdn.net/20161012231742058 

#### 2. return dataframe  
limit(int n)
