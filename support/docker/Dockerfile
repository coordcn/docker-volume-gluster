FROM golang AS build-env

COPY . /go/src/app
WORKDIR /go/src/app

RUN make build

FROM centos:7.3.1611

RUN yum update -y \
    && yum install -y centos-release-gluster \
    && yum install -y gluster*\
    && mkdir -p /var/lib/docker-volumes/gluster \
    && yum clean all

COPY --from=build-env /go/src/app/docker-volume-gluster /usr/bin/docker-volume-gluster

RUN /usr/bin/docker-volume-gluster version

ENTRYPOINT [ "/usr/bin/docker-volume-gluster" ]
CMD [ "daemon" ]
