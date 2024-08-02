FROM alpine

WORKDIR /tmp/src

RUN apk update && apk add --no-cache gcc-avr avrdude avr-libc

COPY ./src /tmp/src

ENTRYPOINT [ "sh" ]