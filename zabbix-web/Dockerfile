FROM zabbix/zabbix-web-nginx-mysql:alpine-3.2-latest

ENV TZ=Asia/Tokyo

RUN set -x \
	&& sed -i -e "s/^date\.timezone=.*$/date.timezone=\"Asia\/Tokyo\"/" /etc/php5/conf.d/99-zabbix.ini \
	\
	&& wget -O /tmp/ipagp.zip  http://ipafont.ipa.go.jp/old/ipafont/ipagp00303.php \
	&& cd /tmp \
	&& unzip ipagp.zip \
	&& mkdir -p /usr/share/fonts/ipa/ \
	&& mv ipagp*/*.ttf /usr/share/fonts/ipa/ \
	&& rm -rf ipagp* \
	&& ln -s /usr/share/fonts/ipa/*.ttf /usr/share/zabbix/fonts/ \
	&& sed -i -e "s/^define('ZBX_GRAPH_FONT_NAME',.*$/define('ZBX_GRAPH_FONT_NAME', 'ipagp');/g" /usr/share/zabbix/include/defines.inc.php \
	&& sed -i -e "s/^define('ZBX_FONT_NAME',.*$/define('ZBX_FONT_NAME', 'ipagp');/g" /usr/share/zabbix/include/defines.inc.php
