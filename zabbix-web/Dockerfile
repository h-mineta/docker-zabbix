FROM zabbix/zabbix-web-nginx-mysql:alpine-4.2-latest

ENV TZ=Asia/Tokyo

RUN set -x \
	&& apk upgrade --update \
	&& apk add \
		curl \
		ca-certificates \
		python3 \
		py3-pillow \
		sudo \
		nmap \
		fping \
		git \
	\
	&& apk add --virtual .build-deps \
		build-base \
		python3-dev \
	\
	&& pip3 install --upgrade pip \
	&& pip3 install py-zabbix ruamel.yaml==0.14.12 \
	\
	&& cd /tmp \
	&& curl -L https://oscdl.ipa.go.jp/IPAexfont/ipaexg00301.zip > /tmp/ipaexg.zip \
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
