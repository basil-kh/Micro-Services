# Use the MongoDB image as base
FROM mongo:4.4

# Change bindIp in mongod.conf.orig
RUN sed -i 's/bindIp: 127.0.0.1/bindIp: 0.0.0.0/g' /etc/mongod.conf.orig


EXPOSE 27017