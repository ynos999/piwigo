FROM nginx:1.31.8

ENV TZ=Europe/Riga
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends nano && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN rm -rf /etc/nginx/conf.d/*
COPY nginx.conf /etc/nginx/nginx.conf