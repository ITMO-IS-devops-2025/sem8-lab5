# system-runtime
FROM alpine:3.21.3 AS system-runtime

RUN apk add aspnetcore8-runtime

## Copied from https://github.com/dotnet/dotnet-docker/blob/main/src/runtime-deps/8.0/alpine3.21-extra/amd64/Dockerfile
ENV APP_UID=1654
RUN addgroup --gid=$APP_UID app && \
    adduser --uid=$APP_UID --ingroup=app --disabled-password app


    
# system-sdk
FROM alpine:3.21.3 AS system-sdk

RUN apk add dotnet8-sdk



# build
FROM system-sdk AS build

WORKDIR /src

COPY src/Panpipe/*.csproj ./Panpipe/
RUN dotnet restore ./Panpipe/

COPY src/ ./
RUN dotnet publish -c Release -o /app ./Panpipe/



# final
FROM system-runtime AS final

WORKDIR /app

COPY --from=build /app ./

USER app

ENTRYPOINT [ "dotnet", "Panpipe.dll" ]
