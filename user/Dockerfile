FROM node:20.19.5-alpine3.21 AS build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
# this may add extra cache memory
RUN npm install 


FROM node:20.19.5-alpine3.22
WORKDIR /opt/server
#now all instruction(CMD,ENV runs under non root).give roboshop user permision to /opt/server then it can acces file/folder
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
        component="user" \
        created_by="susmitha"
ENV  MONGO="true" \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"
COPY --from=build /opt/server /opt/server 
USER roboshop
CMD ["server.js"]  
ENTRYPOINT ["node"]


# FROM node:20
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV REDIS_HOST="redis" \
#     CATALOGUE_HOST="catalogue" \
#     CATALOGUE_PORT="8080"
# CMD ["node", "server.js"]  