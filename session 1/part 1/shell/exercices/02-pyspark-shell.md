## PYSPARK-SHELL Workshop

- Prereqs : <br>
  * You ssh'd into your master instance<br>
  * You dowloaded data<br>
  * Uploaded it to hdfs<br>
  * you are logged in as root (sudo)<br>

## Let's launch a pysark console


```
sudo su 
cd
pyspark
```
![pyspark-shell](/res/img/pyspark.png)

````
print('hello pyspark')
````
- Let's create an RDD from scratch and display its content :

````  
dataList = [("KRYPTON", 36), ("XENON", 54), ("OSMIUM", 76)]
rdd=spark.sparkContext.parallelize(dataList)
````

  * What did you notice ?
  * Which instructon took most time ?
  * Why in you opinion ?

- For a list of possible operations on RDD's  
  https://spark.apache.org/docs/latest/rdd-programming-guide.html#transformations
  https://spark.apache.org/docs/latest/rdd-programming-guide.html#actions

- Let's play a bit with our rdd

````
rdd.take(2)
rdd.first()
rdd.count()
````

- Let's create a second rdd, and join both into a 3rd rdd 

````
dataList2 = [("CHROMIUM", 25), ("CESIUM", 55), ("BARIUM", 56)]
rdd2=spark.sparkContext.parallelize(dataList2)
````

````
rdd3 = rdd.union(rdd2)
rdd3.collect()
````
  * What do you notice in the output ?
  * What are your thoughts about immutability ?

- Let's sort our union RDD : 

````
rdd4 = rdd3.sortBy(lambda a: a[1])
rdd4.collect()
````

- Try the following commands : 
````  
  rdd4.toDebugString()
  rdd3.toDebugString()
````
  
  * What do you think about the output ?
  * What are your guesses ?
  * Why does it refer to Java & Scala in your opinion ?

- Now let's create a dataframe from a CSV file and display its content 
- File should be downloaded and uploaded on HDFS 

**Useful Ressources : **
- [SPARK DATARFAME API REFERENCE](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/dataframe.html)
- [PYSPARK BY EXAMPLE](https://sparkbyexamples.com/pyspark-tutorial/)

- Replace `putyourfirstnamehere` by the personal folder you created while uploading the data to HDFS

````
df = spark.read.option("header", True).format("csv").load("hdfs:///user/root/putyourfirstnamehere/data/zipcodes.csv")
df.show()
````
- Let's count the entries in our file : 

````
df.count()
````

  * What did you notice ?
  * Which instructon took most time ?
  * Why in you opinion ?
  
- Let's play with the Dataframe :
- 
````
df.filter(df.city == "New York").show(df.count(), False)
````

````
df.filter(df.state == "MA").count()
````

````
df.groupBy("state").count().show()
````

````
df.groupBy("state","city").count().orderBy("state", "city").where().show(100)
````

````
df.groupBy("state","city").count().alias("zipcount").orderBy("state", "city").where("count > 50").orderBy("count").show(10)
````

- Gracefully shut down your spark-shell : type exit() + enter

### Caution !!! PLEASE READ !!!
As will be explained later, do NOT launch more than ONE shell per user. 
Always quit your sessions properly (:q in scalla or exit() in pyspark).
Being careless regarding this warning will result in freezing your shells,  
and needing to restart services and killing ghost jobs
