# psql Authentication Failed
## Had a bit of trouble with this too

Found my answer here:

https://gist.github.com/AtulKsol/4470d377b448e56468baef85af7fd614

The key to this solution was using `-h localhost` to force a socket
connection. All told, what I typed in was `psql -h localhost -U postgres -d
analysis -W`.
