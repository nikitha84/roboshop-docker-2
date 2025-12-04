#here we installaing depencies & copy final conent in 2nd step
FROM node:20.19.5-alpine3.22 AS build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.19.5-alpine3.22
WORKDIR /opt/server
#now all instruction(CMD,ENV runs under non root).give roboshop user permision to /opt/server then it can acces file/folder
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
        component="catalogue" \
        created_by="susmitha"
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
COPY --from=build /opt/server /opt/server 
USER roboshop
CMD ["server.js"]  
ENTRYPOINT ["node"]


# FROM node:20
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node", "server.js"] 