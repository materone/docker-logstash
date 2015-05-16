
# docker-logstash
Lean (307MB) and highly configurable Logstash Docker image, based on `progrium/busybox`.

[![Docker Repository on Quay.io](https://quay.io/repository/pires/docker-logstash/status "Docker Repository on Quay.io")](https://quay.io/repository/pires/docker-logstash)

I made this so that I could [easily cluster ELK on top of Kubernetes](https://github.com/pires/kubernetes-elk-cluster), and so, by default it will be listening for the [lumberjack](http://logstash.net/docs/1.4.2/inputs/lumberjack) protocol with certificates provisioned in a mounted directory, `/logstash/certs`.

## Current software

* Oracle JRE 8 Update 45
* Logstash 1.5.0

## Pre-requisites

* Docker 1.5.0+

## Run

* `/logstash/config` - where `logstash` will look for `logstash.conf` file
* `/logstash/certs` - where `logstash` will look for certificate files to be used with `lumberjack`

```
docker run --name logstash -p 5043:5043 -v conf:/logstash/config quay.io/pires/docker-logstash:0.2
```

or 

```
docker run --name logstash -p 5043:5043 -v /home/pires/logstash-config:/logstash/config -v /home/pires/logstash-certs:/logstash/certs quay.io/pires/docker-logstash:0.2
```

## SSL keys

[Since ```logstash-forwarder``` 0.4](http://www.elasticsearch.org/blog/logstash-forwarder-0-4-0-released/), you'll need to provide valid SSL certificates.
> * SSLv3 is no longer supported; TLS 1.0+ is required (compatible with Logstash 1.4.2+).
> * SSL certificates now require a matching hostname or IP SAN for the server.
