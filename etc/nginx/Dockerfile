FROM nginx:1.15.2

LABEL maintrainer="Jakkrapan Wongchan<casanovakung@windowslive.com>"

ARG WORKDIR

RUN usermod -u 1000 www-data
RUN mkdir ${WORKDIR} && exit 0
RUN chown -R www-data: ${WORKDIR}

CMD ["nginx", "-g", "daemon off;"]
