## Overview
This build of spark features an attempt to acquire Java native thread IDs within each instance of a task. We accomplish this by creating an instance of the GetThreadID class at runtime via reflection. This class uses the Java Native Interface to acquire its native thread ID.

## Build Instructions
Follow steps outlined at the following link to build the required system-dependent shared library.

http://stackoverflow.com/questions/11224394/obtaining-the-thread-id-for-java-threads-in-linux

## File Structure of JNI_getThreadNID
Upon completion of the necessary steps outlined in the link provided above, these files must be present in JNI_getThreadNID

/JNI_getThreadNID
--GetThreadID.java
--GetThreadID.class
--libGetThreadID.so

## Path Dependencies
Once compiled, insert the following into ~/.bashrc on each executor machine:

export LD_LIBRARY_PATH=$PATH:/path/to/JNI_getThreadNID

And insert this into $SPARK_HOME/conf/spark-defaults.conf on each executor machine:

spark.executor.extraClassPath /path/to/JNI_getThreadNID
