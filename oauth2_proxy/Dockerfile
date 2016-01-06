FROM resnostyle/base
Maintainer Bryan Pearson <bwp.pearson@gmail.com>

ENV VERSION 2.0.1

ADD https://github.com/bitly/oauth2_proxy/releases/download/2.0.1/oauth2_proxy-2.0.1.linux-amd64.go1.4.2.tar.gz /tmp/oauth2_proxy.tgz

WORKDIR /tmp

RUN tar zxf oauth2_proxy.tgz \
    && mv oauth2_proxy-$VERSION.linux-amd64.go1.4.2 /usr/local/bin/ \
    && rm -rf /tmp/google_auth_proxy*

VOLUME ["/config"]

ADD ./oauth_proxy.cfg /config/oauth_proxy.cfg
ADD ./auth_emails.txt /config/auth_emails.txt
EXPOSE 4180

CMD ["oauth2_proxy", "-config", "/config/oauth_proxy.cfg"]
