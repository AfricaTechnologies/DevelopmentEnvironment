FROM amd64/fedora:latest
FROM amd64/dart:latest

WORKDIR /dart_application

COPY ./ ./

RUN dart analyze lib
RUN dart doc / --output /doc/api
RUN dart fix lib --dry-run
RUN dart fix lib --apply
RUN dart format lib
RUN dart pub get
RUN dart pub deps
RUN dart pub upgrade
RUN dart run lib/main.dart
RUN dart test test/darttest.dart
RUN dart compile exe lib/main.dart -o /bin/linux/dart_application

CMD ["/dart_application"]
