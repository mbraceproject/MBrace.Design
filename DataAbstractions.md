
# Persisted, Partitioned and Cached Data in MBrace 

Taken from [this discussion](https://github.com/mbraceproject/MBrace.Core/issues/55#issuecomment-90097067)


| Cloud Type |  Underlying | Gives | Persist | Caching | Partition | Input to CloudFlow | Ongoing Work |
| --------:|:-----------:|:------------:|:---------:|:---------:|:---------:|:-----:|:-----:|
| `CloudFile` | `System.IO.Stream` | byte[]/lines/text | yes | ?? | (Seek - needs docs) | many | |
| `CloudCell<'T>` | `System.IO.Stream` + deserializer for T | `'T`  | yes | off by default | no | no |
| `CloudCacheable<'T>` | computation generating 'T on demand | `'T` on demand | no | on by default | no  | no | |
| `CloudSequence<'T>` | `System.IO.Stream` + deserializer for type 'T | `seq<'T>` | yes | off by default | no (see CloudVector) | no | may be unified with `CloudVector` | 
| `CloudVector<'T>` | `System.IO.Stream` + deserializer for type 'T |  `seq<'T>` | yes | on by default (?) | yes  | one | may be unified with `CloudSequence` |

Plus the various interfaces, the CloudAtom mutable abstraction and any future Key/Value store abstraction.  (Please add any other non-interface abstractions I've missed)

### Comments:

@dsyme says:

* CloudCacheable still feels somewhat confusing as a name (ICloudCacheable is OK as an interface though. Newcomers looking for a construct for cached cell, vector and file data will naturally gravitate straight to that, when it will rarely be what they need. (I wonder if it can be removed in favour of a library function returning an ICloudCacheable). 

* There also seems overlap between `CloudCacheable<'T>` and `CloudCell<T>` - the main difference seems to be that one is persisted and one is not, and caching is on/off by default

