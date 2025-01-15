# Golang Snippetbox

## app start

- Start mysql
```shell
/opt/homebrew/opt/mysql/bin/mysqld_safe --datadir\=/opt/homebrew/var/mysql
```

- Start application
```shell
go run ./cmd/web
```

## Local dev

- Log into DB
```shell
mysql -D snippetbox -u web -p
```

- URLs
```shell
curl -i -X POST "localhost:4000/snippet/create"
curl -L -i "localhost:4000/snippet/view?id=4"
```

- Generate certs
```shell
go run /opt/homebrew/opt/go@1.23/libexec/src/crypto/tls/generate_cert.go --rsa-bits=2048 --host=localhost 
```