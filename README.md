# Docker Images

Repository of docker images created by [Ionx Solutions](https://www.ionxsolutions.com)

## Postgres with plv8 [(ionx/postgres-plv8](https://hub.docker.com/r/ionx/postgres-plv8))
[![ionx/postgres-plv8][docker-pulls-image]][docker-hub-url]
[![ionx/postgres-plv8][docker-stars-image]][docker-hub-url]
[![ionx/postgres-plv8][docker-automated-image]][docker-hub-url]
[![ionx/postgres-plv8][docker-build-image]][docker-hub-url]

These images are based on the [official Postgres image](https://hub.docker.com/r/_/postgres/), and have the [plv8](https://github.com/plv8/plv8) extension installed and enabled.

### Tags
- [10.2](https://github.com/IonxSolutions/docker-images/tree/master/postgres-plv8/10.2)
- [10.6](https://github.com/IonxSolutions/docker-images/tree/master/postgres-plv8/10.6)
- [11.1](https://github.com/IonxSolutions/docker-images/tree/master/postgres-plv8/11.1)
- [11.5](https://github.com/IonxSolutions/docker-images/tree/master/postgres-plv8/11.5)
- [12.2](https://github.com/IonxSolutions/docker-images/tree/master/postgres-plv8/12.2)
- [12.8](https://github.com/IonxSolutions/docker-images/tree/master/postgres-plv8/12.8)
- [13.6](https://github.com/IonxSolutions/docker-images/tree/master/postgres-plv8/13.6)

### Usage
```bash
$ docker run -d --name postgres ionx/postgres-plv8:11.5
```

_Copyright &copy; 2018 [Ionx Solutions](https://www.ionxsolutions.com) - Provided under the [Apache License, Version 2.0](http://apache.org/licenses/LICENSE-2.0.html)._


[docker-hub-url]: https://hub.docker.com/r/ionx/postgres-plv8/
[docker-pulls-image]: https://img.shields.io/docker/pulls/ionx/postgres-plv8.svg?style=flat-square
[docker-stars-image]: https://img.shields.io/docker/stars/ionx/postgres-plv8.svg?style=flat-square
[docker-automated-image]: https://img.shields.io/docker/automated/ionx/postgres-plv8.svg?style=flat-square
[docker-build-image]: https://img.shields.io/docker/build/ionx/postgres-plv8.svg?style=flat-square
