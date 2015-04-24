## Overview of available and planned combinators for MBrace.Flow

### Producers

Function | Comment | F# | C# | PR | Status
-------- | ------  |--- |--- |--- | ----
`append` |   | o | o | --- | n/a
`ofArray`|   | o | o | -- | n/a
`ofCloudVector`|   | o | ADD | -- | n/a
`ofChannel`| Produce streams out of CloudChannels | ADD | ADD | -- | n/a

### Transformers

Function | Comment | F# | C# | PR | Status
-------- | ------  |--- |--- |--- | ----
`map` |   | o | o | --- | n/a
`filter`|   | o | o | -- | n/a
`collect`|   | o | o | -- | n/a
`choose`|   | o | n/a | -- | n/a

### Consumers

Function | Comment | F# | C# | PR | Status
-------- | ------  |--- |--- |--- | ----
`fold` |   | o | n/a | --- | n/a
`foldBy` |   | o | n/a | --- | n/a
`groupBy`|   | ADD | ADD | -- | n/a
`distinct`|   | ADD | ADD | -- | n/a
`countBy`|   | o | o | -- | n/a
`sortBy`|   | o | o | -- | n/a
`sortByDescending`|   | ADD | ADD | -- | n/a
`length`|   | o | o | -- | n/a
`sum`|   | o | o | -- | n/a
`sumBy`|   | o | o | -- | n/a
`find`|   | o | o | -- | n/a
`tryFind`|   | o | n/a | -- | n/a
`pick`|   | o | o | -- | n/a
`tryPick`|   | o | o | -- | n/a
`exists`|   | o | o | -- | n/a
`forall`|   | o | o | -- | n/a
`maxBy` |   | o | ADD | -- | n/a
`minBy` |   | o | ADD | -- | n/a
`reduce` |   | o | ADD | -- | n/a
`averageBy` |   | o | ADD | -- | n/a
`average` |   | o | ADD | -- | n/a
`groupBy` |   | o | ADD | -- | n/a
