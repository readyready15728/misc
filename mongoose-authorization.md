# Authorization for MongoDB in Mongoose

One who has authorization set up for MongoDB (as described
[here](mongodb-authorization.md)) might then want to write a Node/Express
application that somehow involves the use of Mongoose. This requires an extra
step not documented in a number of guides on this subject, but is easy to
remedy. Connection should look something like this:

```javascript
const dbURI = 'mongodb://admin:password@localhost/db?authSource=admin';

mongoose.connect(dbURI, {
  useMongoClient: true
});
```
