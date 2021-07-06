## Running PySpark on a Jupyter Notebook

1. Verify that Docker is running
2. In the command line, type `docker run -p 8888:8888 jupyter/pyspark-notebook`
3. Click on the URL printed at the end 
4. Open a new Python Shell in the Jupyter Notebook

### Example
```python
import pyspark

# this will work if you are running PySpark locally
sc = pyspark.SparkContext('local[*]')

txt = sc.textFile('file:////usr/share/doc/python3/copyright')
print(txt.count())

python_lines = txt.filter(lambda line: 'python' in line.lower())
print(python_lines.count())
```
