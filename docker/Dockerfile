FROM nginx:1.15
LABEL maintainer="mshah.omar@gmail.com"

USER root

RUN echo "<h1>Hello Dion Global Solutions!</h1>" > /usr/share/nginx/html/index.html

EXPOSE 80

CMD [ "nginx", "-g", "daemon off;" ]
