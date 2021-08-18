FROM node:15.14.0-alpine3.10
WORKDIR /usr/src/app
COPY package.json .
COPY yarn.lock .
RUN apk add bash
CMD ["tail","-f","/dev/null"] 
