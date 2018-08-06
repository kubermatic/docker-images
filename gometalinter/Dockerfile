FROM golang:1.10-alpine3.8 as buildstep

RUN ["apk", "add", "--no-cache", "git"]

# WORKDIR /go/bin

RUN go get -d github.com/alecthomas/gometalinter
WORKDIR /go/src/github.com/alecthomas/gometalinter
RUN git checkout v2.0.6
RUN go install -v github.com/alecthomas/gometalinter

RUN go get -d golang.org/x/lint/golint
WORKDIR /go/src/golang.org/x/lint/golint
RUN git checkout 06c8688daad7faa9da5a0c2f163a3d14aac986ca # July 2nd 2018
RUN go install -v golang.org/x/lint/golint

RUN go get -d github.com/opennota/check
WORKDIR /go/src/github.com/opennota/check
RUN git checkout d583513b5d849e66ee7c5d03c631ed2f03253680 # July 31st 2018
RUN go install -v github.com/opennota/check/cmd/...

RUN go get -d honnef.co/go/tools/cmd/...
WORKDIR /go/src/honnef.co/go/tools
RUN git checkout 88497007e8588ea5b6baee991f74a1607e809487 # July 28st 2018
RUN go install -v honnef.co/go/tools/cmd/...

RUN go get -d github.com/kisielk/errcheck
WORKDIR /go/src/github.com/kisielk/errcheck
RUN git checkout v1.1.0
RUN go install -v github.com/kisielk/errcheck

RUN go get -d github.com/securego/gosec/cmd/...
WORKDIR /go/src/github.com/securego/gosec
RUN git checkout 1.0.0
RUN go install -v github.com/securego/gosec/cmd/...

FROM golang:1.10-alpine3.8
COPY --from=buildstep /go/bin/* /usr/local/bin/
