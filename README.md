# navitia_base_image


Warning: If your goal is to deploy Navitia images, https://github.com/CanalTP/navitia-docker-compose should better suit your need.


To use these Dockerfile you will probably need to add the following lines to your `/etc/resolv.conf` file (so that canaltp.local can be found from a docker):
```
search canaltp.local
nameserver 10.2.0.15
nameserver 10.50.83.15
```
