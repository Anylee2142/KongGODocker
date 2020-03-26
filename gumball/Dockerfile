FROM golang:1.13.9-alpine3.11
EXPOSE 3000
RUN mkdir /app
ADD . /app/
WORKDIR /app
ENV GOPATH /app
RUN cd /app ; go install gumball
CMD ["/app/bin/gumball"]