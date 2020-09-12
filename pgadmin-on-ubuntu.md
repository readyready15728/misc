# pgAdmin on Ubuntu
## Had a little trouble with this one

pgAdmin complained about the lack of a default browser despite this being set.
I hardwired it to use Firefox. I couldn't create a server due to
authentication failure. The solution to this was doing `sudo -u postgres psql`
and then `ALTER USER postgres PASSWORD $new_password;`.
