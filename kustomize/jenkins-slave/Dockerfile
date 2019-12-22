FROM jenkins/slave:3.35-3-alpine

ARG user=jenkins

USER root
RUN addgroup -g 998 docker
RUN apk update && apk add --no-cache docker
RUN addgroup jenkins docker
COPY jenkins-agent /usr/local/bin/jenkins-agent
ADD https://storage.googleapis.com/kubernetes-release/release/v1.14.0/bin/linux/amd64/kubectl /usr/local/bin/
RUN chmod +x /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/jenkins-agent &&\
    ln -s /usr/local/bin/jenkins-agent /usr/local/bin/jenkins-slave
USER ${user}
RUN mkdir /home/jenkins/.kube
ENTRYPOINT ["jenkins-slave"]
