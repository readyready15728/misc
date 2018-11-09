# mongodump Authorization
## Avoiding further headaches

In another of my fantastic misadventures with MongoDB authorization, I learned
that this is how I get a database to dump with version 2.6.10, more or less:

```bash
mongodump -h localhost:27017 -d <database> -o ~/tmp/mongodump --username admin --password '' --authenticationDatabase admin
```
