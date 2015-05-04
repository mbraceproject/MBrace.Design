
# Persisted, Partitioned and Cached Data in MBrace 

Taken from [this discussion](https://github.com/mbraceproject/MBrace.Core/issues/55#issuecomment-90097067)


| Cloud Type |  Underlying | Gives | Persist | Caching | Partition | Mutable | Core/Library |
| --------:|:-----------:|:------------:|:---------:|:---------:|:---------:|:---------:|:---------:|
| `CloudFile` | File store | byte[]/lines/text | yes | no | (Seek - needs docs) | no | core |
| `CloudAtom<'T>` | Table store | `'T` | no | no | no | yes | core |
| `CloudDictionary<'T>` | Table store | `Map<string, 'T>` | yes | no | no | yes | core |
| `CloudChannel<'T>` | Service Bus | `IObservable<'T>` | N/A | N/A | N/A | N/A | core |
| `CloudValue<'T>` | `CloudFile` + deserializer for `'T` | `'T`  | yes | on by default | single file | no | library |
| `CloudSequence<'T>` | `CloudFile` + deserializer for `seq<'T>` | `seq<'T>` | yes | off by default | single file | no | library |
| `PersistedCloudFlow<'T>` | `CloudSequence<'T> []` | `CloudFlow<'T>` | yes | on by default | yes | no | library |
