# Database Sharding

###  Horizontally scale your database: spliting large Db into smaller DB.
- If too many users attempt to use the application to read or save data at the same time.
- It might affect the user experience.

### Benefits of sharding:
- It helps to save more data and improves query performance and general performance.
- Database can reach its maximum capacity, when sharding it can prevent losing the entire service. 
- It is possible to add shards on the fly.

Each shards share the same schema, where physical shard contains multiple and logical has less than the number of schemas in physical.


