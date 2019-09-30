FROM jenkins/jenkins:2.187-alpine

USER jenkins

# Skip initial setup
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

# Plugins to install
COPY plugins.txt /usr/share/jenkins/plugins.txt

# Plugins installation
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

# To create a default user
COPY default-user.groovy /usr/share/jenkins/ref/init.groovy.d/

# To set environment vars
COPY default-envars.groovy /usr/share/jenkins/ref/init.groovy.d/
