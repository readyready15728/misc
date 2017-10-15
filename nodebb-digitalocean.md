# NodeBB Installation on Digital Ocean

What a pain in the ass this all was. I'm writing everything down so I don't
have to figure everything out again.

Start with the following tutorial:

https://www.blogsynthesis.com/install-nodebb-on-digitalocean/

...but it's perfectly possible to clone into `$HOME/nodebb` rather than going
through the steps mentioned setting it up in `/var/www` and adding the new user
etc.. Additionally, the most recent version of NodeBB requires (at least?) Node
6.x, which can be installed like so:

```bash
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

On my rather cheap $5 / mo. Digital Ocean droplet, `npm install` mysteriously
terminates with the terse error message "Killed". I discovered this was because
of limited memory. Here is how to set up swap space on a droplet:

https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-16-04

Notice that Digital Ocean advises against the use of swap space on SSD devices
(like theirs), so *immediately* after running `npm install` with swap enabled,
do `swapoff /swapfile` to prevent deterioration of the hardware. 

Then we come to the setup of NodeBB. NodeBB defaults to MongoDB now and I am
willing to go along with that. MongoDB setup instructions are here:

https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-mongodb-on-ubuntu-16-04

This should be followed pretty closely, except that the advice from the
following Stack Overflow thread should take precedence over it as far as the
creation of the administrative user is concerned:

https://stackoverflow.com/questions/23943651/mongodb-admin-user-not-authorized

Additionally, follow this thread's advice regarding the creation of the
`nodebb` table and user:

https://community.nodebb.org/topic/10939/nodebb-could-not-connect-to-your-mongo-database-error/3

When I ran `node app --setup` I ran into the cryptic "Killed" error again and
again swap solved my issue. Remember to turn it off immediately after use.

`./nodebb start` really is the best way to run NodeBB because it'll start in
the background. When I went and connected to NodeBB I had this issue of
"Looks like your connection to NodeBB was lost, please wait while we try to reconnect."
This can be fixed by going into `config.json` and changing the URL from localhost
to the IP or domain (in my case a bare IP) that NodeBB is being hosted from.

NodeBB is now fully operational but I want SSL. For that, nginx is needed. Start here:

https://www.digitalocean.com/community/tutorials/how-to-create-an-ssl-certificate-on-nginx-for-ubuntu-14-04

The guide is for Ubuntu 14.04 but is still relevant. Then start following this tutorial:

http://www.blogsynthesis.com/nginx-as-nodebb-proxy/

...but use an nginx config like the following, something I was finally able to
figure out after an immense amount of hair-pulling:

```nginx
server {
  listen 80;
  server_name [IP or DNS];
  return 301 https://$host$request_uri;
}

server {
  listen 443 ssl;
  ssl_certificate /etc/nginx/ssl/nginx.crt; 
  ssl_certificate_key /etc/nginx/ssl/nginx.key;

  # enables all versions of TLS, but not SSLv2 or 3 which are weak and now deprecated.
  ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

  # disables all weak ciphers
  ssl_ciphers 'AES128+EECDH:AES128+EDH';

  ssl_prefer_server_ciphers on;

  location / {
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;
      proxy_set_header Host $http_host;
      proxy_set_header X-NginX-Proxy true;

      proxy_pass http://127.0.0.1:4567;
      proxy_redirect off;

      # Socket.IO Support
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
  }
}
```

This will redirect all http:// requests to https://.

The BlogSynthesis tutorial has a bunch of stuff about reconfiguring NodeBB
after it gets set up with nginx. I'm not entirely sure how necessary that is.
In any case, (*inshallah*) if you've carried out all these steps faithfully you
should now have NodeBB set up behind nginx with an encrypted connection. 

I haven't tested this yet, but here is how someone set up NodeBB in a
subdirectory with other content being served around it:

https://community.nodebb.org/topic/10187/serving-up-static-content-with-nginx-with-nodebb-running-from-subfolder
