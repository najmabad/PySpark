Source: [edX: Big Data Analytics Using Spark](https://learning.edx.org/course/course-v1:UCSanDiegoX+DSE230x+1T2021/block-v1:UCSanDiegoX+DSE230x+1T2021+type@sequential+block@56608329f8fc42fc8fcaa5e49673ee3b/block-v1:UCSanDiegoX+DSE230x+1T2021+type@vertical+block@ca9dad9075534f1598561bd910964bf4)


## Plain RDDs
They are made of a list of elements.

```python
# initialize a plain RDD
rdd = sc.parallelize([0, 1, 2])

# sum the square of each items
rdd.map(lambda x: x * x).reduce(lambda (x, y): x + y)
```

## Key-Value RDD
It's a special type of RDD made of (key, value) pairs. NB: the key doesn't need to be unique.

``` python
# initialize a key-value RDD
rdd = sc.parallelize(range(4)).map(lambda x: (x, x*x))
>>> [(0, 0), (1, 1), (2, 4), (3, 9)]
```


## Explore your RDD
When you want to look into the content of your rdd, it's best to do one of the following (instead of `collect()`):
1. `rdd.first()` --> retrieves the first element
2. `rdd.take(n)` --> retrieves the first n elements
3. `rdd.sample(m/n)` --> where `m` are the elements you want to get back and `n` is the lenght of the RDD.

`first()`, `take()`, `sample()` do not return an RDD. 


## Types of commands
We have 3 groups of command in Spark:
1. **Creation commands**: e.g. create an RDD from a file, a database, etc.
2. **Transformation commands**: from an RDD to a new RDD
3. **Action commands**: from an RDD to data on the driver node, database, file, etc.

### Example of Transformations
Transformations take an RDD and return another RDD.
E.g. `map()` and `sample()`

### Example of Actions
`sc.parallelize(range(4)).collect()`

`sc.parallelize(range(4)).count()`

`sc.parallelize(range(4)).reduce(lambda (x, y): x + y)`


### Actions for key-value RDDs

`reduceByKey()` --> performs the reduce operation separatetly on each key value.

```python
A = sc.parallelize([(1, 3), (3, 100), (1, -5), (3, 2)])
A.reduceByKey(lambda (x, y): x * y).collect()
>>> [(1, -15), (3, 200)]
```

`groupByKey()` --> returns a (key, iterator) pair for each key value.

```python
A = sc.parallelize([(1, 3), (3, 100), (1, -5), (3, 2)]
A.groupByKey().map(lambda k, iter: (k, [x for x in iter])
>>> [(1, [3, -5]), (3, [100, 2])]
```

`countByKey()` --> counts how many time the key occurred. It returns a Python dictionary.

```python
A = sc.parallelize([(1, 3), (3, 100), (1, -5), (3, 2)])
A.countByKey()
>>> {1: 2, 3:2}
```

`lookup(key)` --> returns the list of all values associated to a given key.

```python
A = sc.parallelize([(1, 3), (3, 100), (1, -5), (3, 2)]
A.lookup(3)
>> [100, 2]
```

`collectAsMap` --> returns a dict

```python
A = sc.parallelize([(1, 3), (3, 100), (1, -5), (3, 2)])
A.collectAsMap()
>>> {1: [3, -5], 3: [100, 2]}
```



