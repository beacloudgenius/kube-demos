all: serve-hostname

serve-hostname:
	CGO_ENABLED=0 GOOS=linux go build -a -tags netgo -ldflags '-w' serve-hostname.go

clean:
	rm -f serve-hostname

push:
	docker build --tag cloudgenius/serve-hostname:latest . && docker push cloudgenius/serve-hostname:latest
