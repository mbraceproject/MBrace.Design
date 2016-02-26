
# MBrace Types in Overview

## MBrace.Core

### Distributed Computation in MBrace.Core


| Cloud Type |   | 
| --------:|:-----------:|
| `Cloud<T>` |  Represents a distributed cloud computation | 
| `LocalCloud<T>` |  Represents a machine-constrained cloud computation. The computation runs to completion as a locally executing in-memory computation. The computation may access concurrent shared memory and unserializable resources. | 


### Distributed Data in MBrace.Core

Taken from [this discussion](https://github.com/mbraceproject/MBrace.Core/issues/55#issuecomment-90097067)


| Cloud Type            |  Underlying                         | Gives             | Persist | Caching    | Partition   | Indexed  | Mutable | Description           |
| ---------------------:|:-----------------------------------:|:-----------------:|:-------:|:----------:|:-----------:|:--------:|:-------:|:---------------------:|
| `CloudFile`           | Blob store                          | byte[]/lines/text | yes     | no         | via seek    | via seek | no      | Files named by string |
| `CloudValue<T>`       | `CloudFile` + deserializer for `T`   | `T`               | yes     | on default | single file | no       | no      | A distributed value that has been cached by the MBrace runtime  |
| `CloudArray<T>`       | `CloudFile` + deserializer for `T`   | `T[]`             | yes     | no         | no          | no       | no      | A distributed, immutable array that has been cached by the MBrace runtime |
| `CloudAtom<T>`        | Table store                          | `T`               | no      | no         | no          | no       | yes     | A distributed. atomically updatable value reference |
| `CloudDictionary<T>`  | Table store                          | `string -> T`     | yes     | no         | yes, one per key | yes | yes     | A distributed key-value collection |
| `CloudQueue<T>`       | Service Bus                          | `T` values        | N/A     | N/A        | no          | N/A      | yes     | A distributed queue  |

##  MBrace.Flow


###  Distributed/Parallel/Multi-core Computation in MBrace.Flow

| Cloud Type              | Description | Mechanism |  
| -----------------------:|:-----------:|:---------:|
| `CloudFlow<T>`          |  Represents a distributed stream of values | The stream iterated via a distributable evaluators that transform the ultimate input using a multi-core, distributed pipeline  | 


### Distributed/Parallel/Multi-core Data Sources in MBrace.Flow

| CloudFlow Producer                  |  Source                  | Partition    | Description |
|------------------------------------:|:------------------------:|:------------:|:------------:|
| `CloudFlow.OfArray`                 | Serialized array         | divide by #workers + #cores   | | 
| `CloudFlow.OfCloudArrays`           | `CloudArray<T>`          | by #arrays | | 
| `CloudFlow.OfCloudCollection`       | `ICloadCollection<T>`    | divide by #workers + #cores | | 
| `CloudFlow.OfCloudDirectory`        | Cloud file system        | by file (?) |  Constructs a CloudFlow from all files in provided directory using the given reader | 
| `CloudFlow.OfCloudDirectoryByLine`  | Cloud file system        | by file + chunks (?) | Constructs a text CloudFlow by line from all files in supplied CloudDirectory | 
| `CloudFlow.OfCloudFileByLine`       | Cloud file system        | by chunks (?) |  Constructs a CloudFlow of lines from a single large text file.| 
| `CloudFlow.OfCloudFilesByLine`      | Cloud file system        | by files + chunks (?) | Constructs a CloudFlow of lines from a collection of text files. | 
| `CloudFlow.OfCloudFiles`            | Cloud file system        | by files |  | 
| `CloudFlow.OfCloudQueue`            | Cloud queue              | by provided count |  Creates a CloudFlow from the ReceivePort of a CloudQueue | 
| `CloudFlow.OfHttpFileByLine`        | Network                  | by #workers + #cores depending on request | Constructs a CloudFlow of lines from a single HTTP text file. | 
| `CloudFlow.OfHttpFilesByLine`       | Network                  | by #requests + #workers + #cores depending on request |  Constructs a CloudFlow of lines from a collection of HTTP text files. | 
| `CloudFlow.OfSeqs`                  | Serialized IEnumerables  | by #collections |  Creates a CloudFlow instance from a finite collection of serializable enumerations | 

###  Distributed/Parallel/Multi-core Data Sinks in MBrace.Flow

| CloudFlow Sink                |  Writes To                       | Partitioned Write   | Description  |
| -----------------------------:|:--------------------------------:|:-------------------:|:------------:|
| `CloudFlow.toArray`           | Serialized array                 | yes                 | Creates an array from the given CloudFlow.            | 
| `CloudFlow.toCloudQueue`      | Cloud queue                      | yes (?)             |  Sends the values of CloudFlow to the SendPort of a CloudQueue            | 
| `CloudFlow.toTextCloudFiles`  | Cloud file system                | yes                 |  Creates line separated CloudFiles from the given CloudFlow of strings            | 
| `CloudFlow.cache`             | Cloud temp storage on workers    | yes                 |   Creates a PersistedCloudFlow from the given CloudFlow           | 
| `CloudFlow.persist`           | Cloud bloc storage or temp storage on workers    | yes (?)  |   Creates a PersistedCloudFlow from the given CloudFlow, with its partitions cached to a specified storage level.      | 
