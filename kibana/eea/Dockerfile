FROM docker.elastic.co/kibana/kibana:6.8.8
MAINTAINER michimau <mauro.michielon@eea.europa.eu>

USER root
ADD docker-entrypoint.sh /
RUN chmod a+x /docker-entrypoint.sh

ADD src/iframe_custom_styles.js /tmp/iframe_custom_styles.js
ADD src/ui_app.jade /tmp/ui_app.jade
ADD src/*.png /opt/kibana/src/ui/public/assets/favicons/
ADD src/*.ico /opt/kibana/src/ui/public/assets/favicons/
ADD src/*.svg /opt/kibana/src/ui/public/assets/favicons/

RUN sed "s#Loading Kibana# #g" -i  /opt/kibana/src/ui/ui_render/views/ui_app.pug \
  && sed "s#title Kibana#title EEA#g" -i /opt/kibana/src/ui/ui_render/views/chrome.pug \
  && sed -i -e '/\.kibanaWelcomeLogo {/{r /tmp/ui_app.jade' -e 'd}'   /opt/kibana/src/ui/ui_render/views/ui_app.pug \
  && rm /tmp/ui_app.jade \
  && cat /tmp/iframe_custom_styles.js >> /opt/kibana/src/ui/ui_render/bootstrap/template.js.hbs

USER kibana

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["/usr/local/bin/kibana-docker"]
