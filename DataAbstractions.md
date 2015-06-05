
# Persisted, Partitioned, Indexed and Cached Data in MBrace 

Taken from [this discussion](https://github.com/mbraceproject/MBrace.Core/issues/55#issuecomment-90097067)


| Cloud Type |  Underlying | Gives | Persist | Caching | Partition | Indexed | Mutable | Core/Library |
| --------:|:-----------:|:------------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|
| `CloudFile` | File store | byte[]/lines/text | yes | no | via seek | via seek | no | core |
| `CloudAtom<'T>` | Table store | `'T` | no | no | no | no | yes | core |
| `CloudDictionary<'T>` | Table store | `string -> 'T` | yes | no | yes (one per key) | yes | core |
| `CloudChannel<'T>` | Service Bus | `'T` values | N/A | N/A | no | N/A | N/A | core |
| `CloudValue<'T>` | `CloudFile` + deserializer for `'T` | `'T`  | yes | on by default | single file | no | no | library |
| `CloudSequence<'T>` | `CloudFile` + deserializer for `seq<'T>` | `seq<'T>` | yes | off by default | single file | no | no | library |
| `PersistedCloudFlow<'T>` | `CloudSequence<'T> []` | `CloudFlow<'T>` | yes | on by default | yes | no | no | library |
