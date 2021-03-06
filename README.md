# DistributedQueue
A naive distributed queue implementation using Couchbase

[MAVEN]
<dependency>
   <groupId>com.couchbase.client</groupId>
   <artifactId>java-client</artifactId>
   <version>2.4.7</version>
</dependency>

 
 **Queue is a FIFO data structure. Documents inserted first will be deleted first
 Front and rear pointers are the document ID**
 
 The idea is operations in Couchbase are atomic operation.  It has one operation called Counter, which will create 
 document counter. Implement a queue with two pointer rear and front. Both of them are considered as two documents 
 with initial value is 1.  

**[PUSH]**
>> When PUSH operation is called it will create a document  with Auto Increment. For example documents with ID like ADJ_TXN_ID:2, ADJ_TXN_ID:3 will be created in incremented way.
 
 **[POP]**
 >>Now with the counter operation , it will create a document with increment rear like ADJ_TXN_ID:1,
 POP operation will delete the document with ids which are inserted in first order, it will retrieve the value from rear Counter ID.
 
 As operations are atomic, so it can happen in distributed environment. Couchbase will take care of the atomicity .
 
 
 **PUSH] -->  ["queue:front"] --> New Document**. 
 
 **[POP] ---> [""queue:rear"] --> Delete Document**
