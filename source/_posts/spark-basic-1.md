---
title: spark basic 1
---
date: 2018-12-19 18:01:17

## spark java code example
로컬 모드로 실행된 스파크로 csv를 읽고, 필터링하여 정제된 데이터를 DB에 넣는 예제

```java
package chapter1;

import org.apache.spark.sql.SparkSession;
import static org.apache.spark.sql.functions.concat;
import static org.apache.spark.sql.functions.lit;

import java.util.Properties;

import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SaveMode;

public class Application {

    public static void main(String args[]) throws InterruptedException {

        // Create a session
        SparkSession spark = new SparkSession.Builder()
                .appName("csv to db")
                .master("local")
                .getOrCreate();

        // get data
        Dataset<Row> df = spark.read().format("csv")
                .option("header", true)
                .load("src/main/resources/name_and_comments.txt");

        df.show(3);

        // transformation
        df = df.withColumn("full_name",
                concat(df.col("last_name"), lit(", "), df.col("first_name")))
                .filter(df.col("comment").rlike("\\d+"))
                .orderBy(df.col("last_name").asc());

        df.show(3);

        // Write to destination
		String dbConnectionUrl = "jdbc:mysql://127.0.0.1:3306/testdb";
		Properties prop = new Properties();
	    prop.setProperty("driver", "com.mysql.jdbc.Driver");
	    prop.setProperty("user", "testuser");
	    prop.setProperty("password", "password");

        df.write()
        .mode(SaveMode.Overwrite)
        .jdbc(dbConnectionUrl, "project1", prop);

    }
}

```
DB에 자동으로 테이블이 생성되어, 데이터가 들어감.
```sql
CREATE TABLE `project1` (
  `last_name` text COLLATE utf8mb4_bin,
  `first_name` text COLLATE utf8mb4_bin,
  `comment` text COLLATE utf8mb4_bin,
  `full_name` text COLLATE utf8mb4_bin
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin;

```


## 관련 git code 
- https://github.com/kjs850/spark-exercises/blob/master/src/main/java/chapter1/Application.java

tags:
