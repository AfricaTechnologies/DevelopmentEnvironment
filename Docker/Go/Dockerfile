FROM amd64/fedora:latest
FROM amd64/golang:latest

WORKDIR /go_application

COPY ./ ./

RUN go doc ./
RUN go env
RUN go fix ./lib
RUN go fmt ./lib
RUN go get
RUN go list
RUN go list -m
RUN go mod download
RUN go mod tidy
RUN go mod verify
RUN go run ./lib/main.go
RUN go test ./test/gotest.go
RUN go version
RUN go vet ./lib
RUN go work sync
RUN go work use ./
RUN GOOS=darwin GOARCH=amd64 go build -o ./bin/darwin/amd64/go_application ./lib/main.go
RUN GOOS=darwin GOARCH=arm64 go build -o ./bin/darwin/arm64/go_application ./lib/main.go
RUN GOOS=linux GOARCH=amd64 go build -o ./bin/linux/amd64/go_application ./lib/main.go
RUN GOOS=linux GOARCH=arm64 go build -o ./bin/linux/arm64/go_application ./lib/main.go
RUN GOOS=windows GOARCH=amd64 go build -o ./bin/windows/amd64/go_application.exe ./lib/main.go
RUN GOOS=windows GOARCH=arm64 go build -o ./bin/windows/arm64/go_application.exe ./lib/main.go

CMD ["/go_application"]
