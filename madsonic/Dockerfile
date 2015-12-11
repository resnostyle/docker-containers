FROM resnostyle/base-java
Maintainer Bryan Pearson <bwp.pearson@gmail.com>

# Madsonic Package Information
ENV PKG_NAME madsonic
ENV PKG_VER 6.0
ENV PKG_BUILD 7520
ENV PKG_DATE 20150922
ENV PKG_EXT zip

# Use init system
CMD ["/sbin/my_init"]

# Fix ids
#RUN usermod -u 99 nobody
#RUN usermod -g 100 nobody

RUN yum install -y wget unzip

# download madsonic
RUN mkdir -p /var/madsonic/transcode \
  && wget -O /var/${PKG_NAME}/${PKG_NAME}.zip http://www.madsonic.org/download/${PKG_VER}/${PKG_DATE}_${PKG_NAME}-${PKG_VER}.${PKG_BUILD}-standalone.${PKG_EXT} \
  && wget -O /var/${PKG_NAME}/transcode.zip http://www.madsonic.org/download/transcode/${PKG_DATE}_${PKG_NAME}-transcode-linux-x64.zip

# Install Madsonic
RUN mkdir -p /var/${PKG_NAME}/transcode \
  && unzip /var/${PKG_NAME}/${PKG_NAME}.zip -d /var/${PKG_NAME} \
  && unzip /var/${PKG_NAME}/transcode.zip -d /var/${PKG_NAME} \
  && chown -R nobody:users /var/${PKG_NAME} \
  && chmod -R 755 /var/${PKG_NAME} \
  && rm /var/${PKG_NAME}/${PKG_NAME}.${PKG_EXT} \
  && rm /var/${PKG_NAME}/transcode.zip

# Force Madsonic to run in foreground
RUN sed -i 's/-jar madsonic-booter.jar > \${LOG} 2>\&1 \&/-jar madsonic-booter.jar > \${LOG} 2>\&1/g' /var/$PPKG_NAME}/madsonic.sh

# Set Locale env
#ENV LANG en_US.UTF-8
#ENV LC_ALL en_US.UTF-8
#ENV LANGUAGE en_US.UTF-8

# Set Locale
#RUN locale-gen en_US en_US.UTF-8
#RUN dpkg-reconfigure locales 

# default http https port
EXPOSE 4040 4050

# App configuration
VOLUME /config

# Media directory
VOLUME /media

# Copy start.sh script
ADD ./start.sh /start.sh
RUN chmod +x /start.sh
RUN chown -R nobody:users /start.sh

# run App as user
USER nobody
ENTRYPOINT ["/start.sh"]
