FROM python:alpine

RUN apk add --update git bash openssl
RUN apk add ansible=2.9.3-r0

ENTRYPOINT ["/usr/bin/ansible-playbook"]
