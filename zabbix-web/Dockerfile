FROM zabbix/zabbix-web-nginx-mysql:alpine-3.2-latest

ENV TZ=Asia/Tokyo

RUN set -x \
	&& sed -i -e "s/^date\.timezone=.*$/date.timezone=\"Asia\/Tokyo\"/" /etc/php5/conf.d/99-zabbix.ini \
	\
	&& wget -O /tmp/ipaexg.zip  http://dl.ipafont.ipa.go.jp/IPAexfont/ipaexg00301.zip \
	&& cd /tmp \
	&& unzip ipaexg.zip \
	&& mkdir -p /usr/share/fonts/ipa/ \
	&& mv ipaexg*/*.ttf /usr/share/fonts/ipa/ \
	&& rm -rf ipaexg* \
	&& ln -s /usr/share/fonts/ipa/*.ttf /usr/share/zabbix/fonts/ \
	&& sed -i -e "s/^define('ZBX_GRAPH_FONT_NAME',.*$/define('ZBX_GRAPH_FONT_NAME', 'ipaexg');/g" /usr/share/zabbix/include/defines.inc.php \
	&& sed -i -e "s/^define('ZBX_FONT_NAME',.*$/define('ZBX_FONT_NAME', 'ipaexg');/g" /usr/share/zabbix/include/defines.inc.php
