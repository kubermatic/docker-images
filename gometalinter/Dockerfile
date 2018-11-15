FROM golang:1.11 as buildstep

RUN go get -d github.com/alecthomas/gometalinter
WORKDIR /go/src/github.com/alecthomas/gometalinter
RUN git checkout v2.0.6
RUN go install -v github.com/alecthomas/gometalinter

RUN go get -d golang.org/x/lint/golint
WORKDIR /go/src/golang.org/x/lint/golint
RUN git checkout c67002cb31c3a748b7688c27f20d8358b4193582 # Oct 11 2018
RUN go install -v golang.org/x/lint/golint

RUN go get -d github.com/opennota/check
WORKDIR /go/src/github.com/opennota/check
#RUN git checkout 0c771f5545ff495a81aad2916c3f16add0cd3b55 # Sep 11 2018
RUN go install -v github.com/opennota/check/cmd/...

RUN go get -d honnef.co/go/tools/cmd/...
WORKDIR /go/src/honnef.co/go/tools
#RUN git checkout 88497007e8588ea5b6baee991f74a1607e809487 # Sep 20 2018
RUN go install -v honnef.co/go/tools/cmd/...

RUN go get -d github.com/kisielk/errcheck
WORKDIR /go/src/github.com/kisielk/errcheck
RUN git checkout v1.1.0
RUN go install -v github.com/kisielk/errcheck

RUN go get -d github.com/securego/gosec/cmd/...
WORKDIR /go/src/github.com/securego/gosec
RUN git checkout 1.2.0
RUN go install -v github.com/securego/gosec/cmd/...

RUN go get -d github.com/client9/misspell
WORKDIR /go/src/github.com/client9/misspell
RUN git checkout v0.3.4
RUN go install -v github.com/client9/misspell/cmd/...


FROM golang:1.11
COPY --from=buildstep /go/bin/* /usr/local/bin/
