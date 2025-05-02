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
 
   <pre lang="markdown"> ``` docker start hadoop-master hadoop-worker1 hadoop-worker2 ``` </pre>
   

