# Setup Server
Following the concept in [this wonderful guide](https://www.humankode.com/ssl/how-to-set-up-free-ssl-certificates-from-lets-encrypt-using-docker-and-nginx) of creating a minimal nginx server to get SSL certificates from LetsEncrypt to inject into your Docker container for your website.

Once the docker container is running you have to issue (on the host machine)
```
sudo docker run -it --rm -v /docker-volumes/etc/letsencrypt:/etc/letsencrypt -v /docker-volumes/var/lib/letsencrypt:/var/lib/letsencrypt -v $LOCAL_REPO_DIR/www:/data/letsencrypt -v "/docker-volumes/var/log/letsencrypt:/var/log/letsencrypt" certbot/certbot certonly --webroot --email $YOUR_EMAIL --agree-tos --no-eff-email --webroot-path=/data/letsencrypt -d $YOUR_URL(S)
```

## How it works
Once `Dockerfile` has been compiled and run, you will have a simple webserver that listens on port 80. The above command mounts some directories in `/docker-volumes` that will save the logs and configuration files and certificates that are created upon running `certbot`.

At this point you are ready to rock! You can simply mount the appropriate `docker-volumes` in your website's Docker container and you're off and running!
