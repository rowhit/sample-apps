FROM ubuntu
VOLUME /root/.jenkins
USER root
RUN apt-get update;apt-get install curl wget -y
RUN curl -o /apc.zip http://api.demo.apcera.net/v1/apc/download/linux_amd64/apc.zip
RUN wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
RUN echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list
RUN apt-get update;apt-get -y install ant openjdk-8-jre-headless tar git zip unzip jenkins
RUN curl -o cli.jar http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/2.1/swarm-client-2.1-jar-with-dependencies.jar
RUN unzip /apc.zip -d /
ADD slave.sh /
ADD startup.sh /
ENV PATH=$PATH:/
ENV TERM xterm
EXPOSE 8080
ENV JAVA_OPTS "-Dhudson.Main.development=true -Djenkins.install.runSetupWizard=false"
CMD bash /startup.sh
