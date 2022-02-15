# data warehouse

original developed for big data and business intelligence apps

aatributes:
aggregate data from multiple sources
data processes and analyzed
intended for long runing batch jobs
optimzed for read operations
not real-time 
subject oriented revolves around topic
integrated from relational dbs, files, etc.
data is time stamped
non-volitile, previous versions are not erased
data can be accessed as function of time and understand data evolution
very consistent schema
high quality and consistency
read and query rates are high

compared to dbs:
|datawares|database|
|-|-|
|intended to analyze data|intended to analyze transactions|
|online analytical processing OLAP|online transactional processing OLTP|
|data is refreshed/delayed from sources|data is available real-time|
|stores data as a function of time|stores only current data|
|data can scale to >=terabytes|data scales to gigabytes|
|queries are complex and long running jobs|queries execute in real time|
|tables dont need to be normalized|tables normalized for efficiency|

