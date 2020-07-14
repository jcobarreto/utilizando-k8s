##################################
# STEP 1 build executable binary #
##################################
FROM golang:alpine AS builder

WORKDIR /go/src/app
COPY ws.go .

#RUN go build ws.go
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags="-w -s" -o /go/bin/ws .

##################################
# STEP 2 build a small image     #
##################################
FROM scratch

# Copy our static executable.
COPY --from=builder /go/bin/ws .

EXPOSE 8000

# Run the ws binary.
CMD ["./ws"]
