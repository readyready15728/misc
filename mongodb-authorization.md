# MongoDB Authorization

As alluded to in my [instructions on installing NodeBB on a Digital Ocean
droplet](nodebb-digitalocean.md), there are old instructions on how to set up
authorization on MongoDB out there that will only frustrate users of more
recent versions. This is *right* way to do things in the MongoDB shell as of
2.6.10:

```javascript
use admin;
db.createUser({
  user: 'admin',
  pwd: 'password',
  roles: [{role: 'root', db: 'admin'}]
});
```

Remember to enable authorization in `mongod.conf` afterwards (with `auth =
true`) and restart the service.

Typically, after this one will want to set up databases with respective users
having less than full administrative power. An example of what this would look
like:

```javascript
use database;
db.createUser({
  user: 'database',
  pwd: 'password',
  roles: ['readWrite', 'dbAdmin']
});
```
