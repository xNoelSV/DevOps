FROM nginx:stable-alpine

# use a volume is more efficient than copying files
VOLUME /tmp

# Copy the nginx configuration file
COPY nginx.conf /etc/nginx/nginx.conf
COPY dist/billingApp /usr/share/nginx/html
COPY mime.types /etc/nginx/mime.types

# Install OpenJDK 17
RUN apk add --no-cache openjdk17-jre

# Define the envoirment variable for the Java application
ENV JAVA_HOME /usr/lib/jvm/java-17-openjdk
ENV PATH $JAVA_HOME/bin:$PATH

# Verify the installation
RUN java -version

# Install java microservice
ENV JAVA_OPTS=""
ARG JAR_FILE
ADD ${JAR_FILE} /app.jar

# Copy into containter
COPY appshell.sh appshell.sh

# The ports 7080 for backend-app and 80 for the webapp
EXPOSE 80 7080

ENTRYPOINT [ "sh", "/appshell.sh" ]