# alpine-docker-bind

Small bind server for Internal zone and caching.

==> dns.docker <==
FROM alpine
RUN apk update && apk add bind bind-tools bind-libs bind-doc \
&& mkdir /var/cache/bind \
&& chown named /var/cache/bind \
&& mkdir /var/lib/bind \
&& chown -R named /var/lib/bind \
&& touch /etc/bind/named.conf \
&& chmod +r /etc/bind/named.conf
EXPOSE 53
VOLUME ["/etc/bind","/var/lib/bind"]

#CMD /usr/sbin/named -4 -u named -g
CMD named -u named -4 -g -c /etc/named/named.conf

==> readme <==
docker run -d -p 192.168.0.150:53:53 -p 192.168.0.150:53:53/udp -v /srv/named/etc:/etc/named -v /srv/named/zones:/var/lib/bind --name bind --hostname bind aink99/alpine-docker-bind
seb@fox ~/docker/dns <--$
