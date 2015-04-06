
# Data abstractions in MBrace 

Taken from [this discussion](https://github.com/mbraceproject/MBrace.Core/issues/55#issuecomment-90097067)

### Concrete

| Cloud Type |  Underlying | Gives | Persisted | Caching | Partitioned | Input to CloudFlow | Ongoing Work |
| --------:|:-----------:|:------------:|:---------:|:---------:|:---------:|:-----:|:-----:|
| `CloudFile` | `System.IO.Stream` | byte[]/lines/text | yes | ?? | (Seek - needs documentation) | many | |
| `CloudCell<'T>` | `System.IO.Stream` + deserializer for T | `'T`  | yes | off by default | no | no |
| `CloudCacheable<'T>` | computation generating 'T on demand | `'T` on demand | no | on by default | no  | no | |
| `CloudSequence<'T>` | `System.IO.Stream` + deserializer for type 'T | `seq<'T>` | yes | off by default | no (see CloudVector) | no | may be unified with `CloudVector` | 
| `CloudVector<'T>` | `System.IO.Stream` + deserializer for type 'T |  `seq<'T>` | yes | on by default (?) | yes  | one | may be unified with `CloudSequence` |

### Interfaces

TBD

