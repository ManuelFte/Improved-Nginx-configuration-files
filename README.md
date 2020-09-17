# Improved Nginx configuration files

These are configuration files for Nginx with some settings to improve aspects such as performance and security, as well as handling some possible errors. Designed for a setup based on server blocks as seen [here](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04).

*Last tested on Nginx 1.18.0 on Ubuntu 20.04.*

## Deployment

### nginx.conf

Back up the default configuration file:

`sudo mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bck`

Recreate it:

`sudo nano /etc/nginx/nginx.conf`

Paste the contents of the improved [nginx.conf](https://raw.githubusercontent.com/ManuelFte/Improved-Nginx-configuration-files/master/nginx.conf) file from this repository.

Test that everything is running well:

`sudo nginx -t`

Reload to apply changes:

`sudo systemctl reload nginx`

### Domain files

Disable the default file:

`sudo rm /etc/nginx/sites-enabled/default`

Open the contents of [example.com.conf](https://raw.githubusercontent.com/ManuelFte/Improved-Nginx-configuration-files/master/example.com.conf) with a text editor and use CTRL + H to replace all instances of `example.com` with your domain.

On the server, create a new file for the domain you're going to set up (replacing `example.com` with your domain):

`sudo nano /etc/nginx/sites-available/example.com`

Paste the contents of the previous file there (note that the file in this repository has a `.conf` extension merely for code highlighting purposes, the file in your server must not have this extension).

Enable it:

`sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/example.com`

Test that everything is running well:

`sudo nginx -t`

Reload to apply changes:

`sudo systemctl reload nginx`

Your website should now be live in your domain.

## Sources

* https://www.digitalocean.com/community/tutorials/how-to-redirect-www-to-non-www-with-nginx-on-centos-7
* https://geekflare.com/nginx-production-configuration/
* https://gist.github.com/plentz/6737338
* https://stackoverflow.com/questions/9824328/why-is-nginx-responding-to-any-domain-name/9826635
* https://nginx.org/en/docs/http/ngx_http_gzip_module.html
* https://www.codetd.com/en/article/6286848
* https://nginx.org/en/docs/ngx_core_module.html
* https://docs.nginx.com/nginx/admin-guide/monitoring/logging/
* https://nginx.org/en/docs/http/ngx_http_core_module.html
* https://medium.com/staqu-dev-logs/optimizations-tuning-nginx-for-better-rps-of-an-http-api-de2a0919744a
* https://www.digitalocean.com/community/tutorials/how-to-optimize-nginx-configuration
* https://www.digitalocean.com/community/tutorials/how-to-host-a-website-using-cloudflare-and-nginx-on-ubuntu-16-04