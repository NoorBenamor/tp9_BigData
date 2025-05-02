# TP9 - المعالجة الدفعية والفورية باستخدام Apache Spark

##  الهدف من المشروع

يهدف هذا المشروع إلى تطبيق تقنيات معالجة البيانات باستخدام إطار العمل **Apache Spark**، وذلك من خلال نوعين من المعالجة:

- **المعالجة الدفعية (Batch Processing)** باستخدام Spark Core
- **المعالجة الفورية (Streaming Processing)** باستخدام Spark Structured Streaming

---

##  بيئة العمل

- **Apache Hadoop**: الإصدار 3.3.6  
- **Apache Spark**: الإصدار 3.5.0  
- **Java**: الإصدار 1.8  
- **Docker**: أحدث إصدار  
- **VS Code** أو أي بيئة تطوير أخرى  
- **نظام التشغيل**: Linux أو Mac (أو أي نظام شبيه بـ Unix)

---

##  إعداد بيئة العمل

1. تشغيل حاويات Docker:
   --------------------------
 
   <pre lang="markdown">  docker start hadoop-master hadoop-worker1 hadoop-worker2 </pre>

   ------------------------------------------
   ![spark](https://github.com/user-attachments/assets/68fde0d9-21e1-4431-b399-df9e1d0f10cf)

   2.الدخول إلى الحاوية الرئيسية:
   ------------------
    <pre lang="markdown">  docker exec -it hadoop-master bash </pre>

    --------------------
    
   3.تشغيل خدمات Hadoop:

    ------------
    <pre lang="markdown">  ./start-hadoop.sh </pre>

    -------------
   ![spark1](https://github.com/user-attachments/assets/aa469a96-f4eb-45a9-9205-df5fd63df574)


   ## الجزء ألاول: المعالجة الدفعية (Batch Processing)
   -------------
   #مثال باستخدام Spark Shell
   ---------
   1.إنشاء ملف نصي:
   -----------
    <pre lang="markdown"> echo -e 'Hello Spark wordcount!\nHello Hadoop Also :)' > file.txt </pre>

    ------------
   2.رفع الملف إلى نظام HDFS:
   -----------
    <pre lang="markdown">  hdfs dfs -mkdir -p /user/root
    hdfs dfs -put file.txt</pre>
   ----------------
   ![spark6](https://github.com/user-attachments/assets/1b00d13d-dbbe-4974-a366-8434c47e0a3b)

   3.تشغيل Spark Shell:
   ------------
    <pre lang="markdown">  spark-shell </pre> 
    
    ---------
   4.تنفيذ كود WordCount:
   ----------
    <pre lang="markdown"> val lines = sc.textFile("file.txt")
    val words = lines.flatMap(_.split("\\s+"))
    val wc = words.map(w => (w, 1)).reduceByKey(_ + _)
    wc.saveAsTextFile("file1.count")
    </pre>
   
    --------------
   
    #مثال باستخدام Java و Maven:
   -----------
   1.إنشاء مشروع Maven وإضافة التبعيات الخاصة بـ Spark في ملف pom.xml.5.
   2.إنشاء الكلاس WordCountTask داخل الحزمة spark.batch.tp21.
   3.بناء المشروع باستخدام:

   -----
   <pre lang="markdown"> mvn package </pre> 

   ------
   4.نسخ ملف JAR إلى الحاوية:
   ---------
   <pre lang="markdown">  docker cp target/wordcount-spark-1.0-SNAPSHOT.jar hadoop-master:/root/wordcount-spark.jar </pre>

   ---------

   5.تنفيذ المهمة باستخدام spark-submit:
   ---------
   <pre lang="markdown"> spark-submit --class spark.batch.tp21.WordCountTask --master yarn --deploy-mode cluster wordcount-spark.jar input/purchases.txt out-spark2 </pre> 

   --------------
   
   
