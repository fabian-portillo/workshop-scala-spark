### June 17 2019
# WORKSHOP - Setup Scala & Spark locally 
using IntelliJ IDEA
This is a guide for setting up Scala and Spark environments in your local machine. 

## Introduction.
This guide has been created for windows users so the configuration may change depending of the O.S you are using.

## Prerequisites.
Java 1.8. 

Install 7-zip tool. (Optional)

## Requisites.
Download and install Scala 2.11.12 version.

Download and install Apache Spark 2.3 version.

Install IntelliJ IDEA community edition.
******************************************************************************************************************************************************************************************************************************************************************************

# First steps:
### 1. Verify Java version in your local machine.

The first step is to verify if you have the Java 1.8 version installed in your local machine since Java 1.8 is the most stable version and also a essential requirement to use Apache Spark in order to continue with the following steps.

If you use Windows O.S you can verify your Java version through the CMD console as shown below:

![java-version](https://media.github.ibm.com/user/213691/files/579a2d80-91de-11e9-94bb-90e4c354f067)

### 2. Set up Java in your local machine.
Once you have verified your Java version if java 1.8 has not been installed yet then continue to the following steps:

### Download & install JRE:
https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html
![jre](https://media.github.ibm.com/user/213691/files/29691d80-91df-11e9-8718-d56e573f7bc1)

### Download & install JDK:
https://www.oracle.com/technetwork/java/javaee/downloads/jdk8-downloads-2133151.html
![jdk](https://media.github.ibm.com/user/213691/files/2ff79500-91df-11e9-9353-27846522accd)

### 3. Set up environment & Path variables.

In order to avoid dependencies issues you need to set up your local environment variables of your system and create a new one with the name of JAVA_HOME as shown below.

Also you need to add other variable to your PATH named as SPARK_HOME located into your main local machine drive. 
![variables-entorno](https://media.github.ibm.com/user/213691/files/37b73980-91df-11e9-8933-20c7108d96bb)

******************************************************************************************************************************************************************************************************************************************************************************
# Apache Spark
Once you are on this point ready to continue to the following steps, make sure you choose Apache Spark 2.3 version as you can see in the image below.


Go to the following link to download it:

### Apache Spark website: https://spark.apache.org/downloads.html

![spark-1](https://media.github.ibm.com/user/213691/files/384fd000-91df-11e9-9f01-f69a33b90d7a)

******************************************************************************************************************************************************************************************************************************************************************************
# IntelliJ IDEA

### Download IntelliJ IDEA Community edition from the following link: https://www.jetbrains.com/idea/download/#section=windows
![intellij](https://media.github.ibm.com/user/213691/files/ed36bc80-91e0-11e9-8f30-9be947935a13)


Once you have installed IntelliJ you need to install the IntelliJ Scala plugin. 
To do that, navigate to preferences > Plugins > Browse Repositories > search and install Scala.
![scala-plugin](https://media.github.ibm.com/user/213691/files/ec9e2600-91e0-11e9-8654-b76da7db4734)

******************************************************************************************************************************************************************************************************************************************************************************
# Demo - Set up IntelliJ
### 1. Open IntelliJ


![intellij-create](https://media.github.ibm.com/user/213691/files/32f38500-91e1-11e9-94a7-1685782f4f87)

### 2. Create a project. 


![create](https://media.github.ibm.com/user/213691/files/32f38500-91e1-11e9-8b4d-18fc62db9116)


### 3. Name your project and select your appropriate Scala and SBT versions.
![image](https://user-images.githubusercontent.com/50177169/59732382-9b595b00-920f-11e9-90e8-7611227c4789.png)

## SBT 

### 1. Select your sbt file as shown below and then open it.
       
![image](https://user-images.githubusercontent.com/50177169/59731624-86c79380-920c-11e9-883f-9881463f353e.png)

       
### 2. Add the corresponding dependencies for your project.
       
![image](https://user-images.githubusercontent.com/50177169/59731648-a2cb3500-920c-11e9-95ba-4bc771c43722.png)   
       
### 3. Ensure the changes are imported without problem.
       
![image](https://user-images.githubusercontent.com/50177169/59731663-b24a7e00-920c-11e9-82ba-9d488699736f.png)

******************************************************************************************************************************************************************************************************************************************************************************
# Demo - Scala ‘hello world’

### 1. In the same project you have, create a Scala class and then run it:


![image](https://user-images.githubusercontent.com/50177169/59731754-0e150700-920d-11e9-97bf-67bf37a0c080.png)


### 2. Run your application

.
![image](https://user-images.githubusercontent.com/50177169/59731768-1cfbb980-920d-11e9-90b2-5015d1b45e82.png)

******************************************************************************************************************************************************************************************************************************************************************************
# Demo - Apache Spark
Once you have followed all the steps before then you are able to test the functionality of Apache Spark in action with the following example:

### 1. Add the following text file named shakespeare.txt
![image](https://user-images.githubusercontent.com/50177169/59731820-4ae0fe00-920d-11e9-9337-4fac9624819f.png)

### 2. Replace your scala code of “hello world” you have previously created for this: 

   
     import org.apache.spark.{SparkConf, SparkContext}
  
     object PrimerPrograma {

     def main(args: Array[String]) {

     //Create a SparkContext to initialize Spark
     val conf = new SparkConf()
     conf.setMaster("local")
     conf.setAppName("Word Count")
     val sc = new SparkContext(conf)


     // Load the text into a Spark RDD, which is a distributed representation of each line of text
     val textFile = sc.textFile("src/main/shakespeare.txt")


     //word count
     val counts = textFile.flatMap(line => line.split(" "))
       .map(word => (word, 1))
       .reduceByKey(_ + _)


     counts.foreach(println)
     System.out.println("Total words: " + counts.count());
     counts.saveAsTextFile("/tmp/shakespeareWordCount")
      }
     }

     

  
Just like when you ran the scala application now do the same with Apache Spark code.


   ### 3. Run PrimerPrograma Scala class. 
![image](https://user-images.githubusercontent.com/50177169/59731857-6ba95380-920d-11e9-9ac2-181a93909bb5.png)

This program print the frequency of each word that appears in Shakespeare, the expected output looks like this:

## Results:

**********************************************************************************************************************************
**********************************************************************************************************************************

# References.

### Documentation.
Scala documentation.
https://docs.scala-lang.org/

### Spark documentation
https://spark.apache.org/documentation.html

### IntelliJ IDEA documentation
https://www.jetbrains.com/idea/documentation/
_________________________________________________________________________

## Guides

### Setting up a Spark Development Environment with Scala
https://es.hortonworks.com/tutorial/setting-up-a-spark-development-environment-with-scala/

### Spark: How to install on Windows in 5 steps.
https://medium.com/big-data-engineering/how-to-install-apache-spark-2-x-in-your-pc-e2047246ffc3
____________________________________________________________

## Tutorials
(Open Source)
Spark

### Spark tutorial.
https://data-flair.training/blogs/spark-tutorials-home/

### Apache Spark and Scala
https://www.edureka.co/blog/spark-tutorial/

### Scala 
Scala tutorials.
https://data-flair.training/blogs/scala-tutorials-home/

(Not Open Source) -  Spark & Scala
Apache Spark with Scala - (Oreilly) 
### Introduction and Getting Set Up.
https://learning.oreilly.com/videos/apache-spark-with/9781787129849/9781787129849-video1_1

### Apache Spark 2 with Scala - Hands On with Big Data! - (Udemy)
https://www.udemy.com/apache-spark-with-scala-hands-on-with-big-data/learn/v4/overview


