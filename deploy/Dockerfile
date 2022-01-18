ARG GO_VERSION=1.17

FROM golang:${GO_VERSION} as builder
ARG APP_ROOT=/app

WORKDIR ${APP_ROOT}

# Install deps before build to re-use docker caching
COPY ./go.mod ./
COPY ./go.sum ./
RUN go mod download

# Build
COPY ./ ./
ENV CGO_ENABLED=0 GOOS=linux GOARCH=amd64
RUN go build -o hey



FROM scratch as runner
ARG APP_ROOT=/app

COPY --from=builder ${APP_ROOT}/hey /hey
ENTRYPOINT [ "/hey" ]

