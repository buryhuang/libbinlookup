# libbinlookup
A tiny library doing simple "fingerprint to data_uri" mapping using Google leveldb.

Deduplication is a rather mature domain where tons of research is published. This little library is based on the paper:
"Extreme Binning: Scalable, Parallel Deduplication for Chunk-based File Backup"
from 2009. All credits go to the paper.
http://cs.ucsb.edu/~vj/projects/SDDS/ExtremeBinning.pdf

Many of the techinques may be traced back to eariler paper quoted in this one, but it's good enough to based on a rather new paper as a convenient way.

On the other hand, as times goes by, the novel levelDB from Google has been matured enough to be a tool that the right level of consolidation of features collections: B tree search efficiency, batch fetch based on locality, post-merge for better inline insert.
Using bloom filter is also mature in most areas.

Combining all the common techiques and general available frameworks, we can easily have the stable and high performance finger print lookup system that people used to have to create an enterprise to home-brew one.

Yet another level, in-memory is a trend. LevelDB takes care of it too with the memory-storage leveling/post-merge tree.

# Interface
- bin_uri
  - \<blob_uri:offset:length>

- put(key, bin_uri)
  - [return] boolean

- get(key)
  - [return] bin_uri

- puts(std::vector\<key, bin_uri>)
  - [return] boolean

- gets(std::vector\<key>)
  - [return] std::vector\<key, bin_uri>
