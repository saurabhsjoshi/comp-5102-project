FROM alpine:3.15

RUN apk add --no-cache fio

CMD ["/bin/sh", "-c", "--", "trap : TERM INT; sleep infinity & wait"]
