FROM alpine:latest
RUN apk update && apk add  bind bind-tools bind-libs bind-doc \
	&& mkdir /var/cache/bind \
	&& chown named /var/cache/bind \
	&& mkdir  /var/lib/bind \
	&& chown -R named /var/lib/bind \
	&& touch  /etc/bind/named.conf \
	&& alias rndc="rndc -c /etc/named/rndc.conf" >> ~/.bashrc \
	&& chmod +r    /etc/bind/named.conf
EXPOSE 53
VOLUME ["/etc/bind","/var/lib/bind"]

#CMD    /usr/sbin/named -4 -u named -g
CMD   named -u named -4 -g -c /etc/named/named.conf
