FROM zabbix/zabbix-web-nginx-mysql:alpine-3.4-latest

ENV TZ=Asia/Tokyo

RUN set -x \
	&& apk upgrade --update \
	&& apk add \
		curl \
		ca-certificates \
		python3 \
		sudo \
		nmap \
		fping \
	\
	&& apk add --virtual .build-deps \
		build-base \
		python3-dev \
	\
	&& pip3 install --upgrade pip \
	&& pip3 install py-zabbix ruamel.yaml \
	&& cd /tmp \
	&& curl -L https://github.com/Prototype-X/Zabbix-Network-Weathermap/archive/1.1.zip > /tmp/Zabbix-Network-Weathermap.zip \
	&& mkdir -p /opt \
	&& unzip Zabbix-Network-Weathermap.zip -d /opt \
	&& cd /opt \
	&& mv Zabbix-Network-Weathermap* Zabbix-Network-Weathermap \
	&& chmod a+x Zabbix-Network-Weathermap/*.py \
	\
	&& sed -i -e "s/^date\.timezone=.*$/date.timezone=\"Asia\/Tokyo\"/" /etc/php5/conf.d/99-zabbix.ini \
	\
	&& cd /tmp \
	&& curl -L http://dl.ipafont.ipa.go.jp/IPAexfont/ipaexg00301.zip > /tmp/ipaexg.zip \
	&& unzip ipaexg.zip \
	&& mkdir -p /usr/share/fonts/ipa/ \
	&& mv ipaexg*/*.ttf /usr/share/fonts/ipa/ \
	&& rm -rf ipaexg* \
	&& ln -s /usr/share/fonts/ipa/*.ttf /usr/share/zabbix/fonts/ \
	&& sed -i -e "s/^define('ZBX_GRAPH_FONT_NAME',.*$/define('ZBX_GRAPH_FONT_NAME', 'ipaexg');/g" /usr/share/zabbix/include/defines.inc.php \
	&& sed -i -e "s/^define('ZBX_FONT_NAME',.*$/define('ZBX_FONT_NAME', 'ipaexg');/g" /usr/share/zabbix/include/defines.inc.php \
	\
	# cleaning
	&& cd / \
	&& apk del --purge .build-deps \
	&& rm -rf /tmp/* \
	&& rm -rf /var/cache/apk/*
