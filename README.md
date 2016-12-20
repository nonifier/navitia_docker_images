# navitia_base_image


To use these Dockerfile you will probably need to add the following lines to your `/etc/resolv.conf` file (so that canaltp.local can be found from a docker):
```
search canaltp.local
nameserver 10.2.0.15
nameserver 10.50.83.15
```
