# Assignment-20.3

1.Explain in brief Writable and Writable Comparable in Hadoop with an example.

Ans.Writable is an interface in Hadoop. Writable in Hadoop acts as a wrapper class to almost all the primitive data type of Java. That is how int of java has become IntWritable in Hadoop and String of Java has become Text in Hadoop.Writables are used for creating serialized data types in Hadoop.
Hadoop frame work definitely needs Writable type of interface in order to perform the following tasks:

a.Implement serialization
b.Transfer data between clusters and networks
c.Store the deserialized data in the local disk of the system

Implementation of writable is similar to implementation of interface in Java. It can be done by simply writing the keyword ‘implements’ and overriding the default writable method.

Writable is a strong interface in Hadoop which while serializing the data, reduces the data size enormously, so that data can be exchanged easily within the networks. It has separate read and write fields to read data from network and write data into local disk respectively. Every data inside Hadoop should accept writable and comparable interface properties.
Serialization is important in Hadoop because it enables easy transfer of data. If Writable is not present in Hadoop, then it uses the serialization of Java which increases the data over-head in the network.

we can make a custom type in Hadoop using Writables.
For implementing Writables, we need few more methods in Hadoop:

public interface Writable {
 
void readFields(DataInput in);
 
void write(DataOutput out);
 
}

Here, readFields, reads the data from network and write will write the data into local disk. Both are necessary for transferring data through clusters. DataInput and DataOutput classes (part of java.io) contain methods to serialize the most basic types of data.

WritableComparable

WritableComparable can be defined as a sub interface of Writable, which has the feature of Comparable too.We need to make our custom type, comparable if we want to compare this type with the other.We want to make our custom type as a key, then we should definitely make our key type as WritableComparable rather than simply Writable. This enables the custom type to be compared with other types and it is also sorted accordingly. Otherwise, the keys won’t be compared with each other and they are just passed through the network.
If we have made our custom type Writable rather than WritableComparable our data won’t be compared with other data types. There is no compulsion that our custom types need to be WritableComparable until unless if it is a key. Because values don’t need to be compared with each other as keys.

If our custom type is a key then we should have WritableComparable or else the data won’t be sorted.
The implementation of WritableComparable is similar to Writable but with an additional ‘CompareTo’ method inside it.

public interface WritableComparable extends Writable, Comparable
{
    void readFields(DataInput in);
 
    void write(DataOutput out);
 
    int compareTo(WritableComparable o)
}

With the use of these Writable and WritableComparables in Hadoop, we can make our serialized custom type with less difficulty. This gives the ease for developers to make their custom types based on their requirement.
