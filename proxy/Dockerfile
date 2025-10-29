FROM nginxinc/nginx-unprivileged:1-alpine
LABEL maintainer='Gonzo'

COPY ./default.conf.tpl /etc/nginx/default.conf.tpl
COPY ./uwsgi_params /etc/nginx/uwsgi_params
COPY ./run.sh /run.sh

ENV LISTEN_PORT=8000
ENV APP_HOST=app
ENV APP_PORT=9000

USER root

#Primero creamos un nuevo directorio, volstatic, y después le cambiamos los permisos a 755 a ese directorio.
#Despues hacemos touch para crear un nuevo archivo y despues damos al user nginx de ese archivo para que lo pueda modificar.
#Por último le damos permiso a run.sh

RUN mkdir -p /vol/static && \
    chmod 755 /vol/static && \
    touch /etc/nginx/conf.d/default.conf && \
    chown nginx:nginx /etc/nginx/conf.d/default.conf && \
    chmod +x /run.sh

VOLUME /vol/static

USER nginx

CMD ["/run.sh"]
