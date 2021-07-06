*Speaker: Holden Karau*

*URL: https://www.youtube.com/watch?v=bJouNc1REno*

## Transformations (lazy)
- `map()`
- `filter()`
- `flatMap()`
- `reduceByKey()`
- `join()`
- `cogroup()`

## Actions (eager)
- `count()`
- `reduce()`
- `collect()`
- `take()`
- `saveAsTextFile()`
- `saveAsHadoop()`
- `countByValue()`



## Exercise: Count the # of word occurrences

```python
import pyspark
import os

sc = pyspark.SparkContext('local[*]')
src = "file:///" + os.environ['SPARK_HOME'] + "\README.md"

text = sc.fileText(src)
# flattens the RDD after applying the function on every element and returns a new PySpark RDD
words = text.flatMap(lambda x: x.split(" "))

# merge the values of each key using an associative reduce function
word_count = (words.map(lambda x: (x, 1)).reduceByKey(lambda x, y: x + y))

word_count.saveAsTextFile('output')
```


