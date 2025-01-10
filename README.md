# Golang Snippetbox

## app start

- Start mysql
```
/opt/homebrew/opt/mysql/bin/mysqld_safe --datadir\=/opt/homebrew/var/mysql
```

- Start application
```
go run ./cmd/web
```

## Local dev

- Log into DB
```
mysql -D snippetbox -u web -p
```

- URLs
```
curl -i -X POST "localhost:4000/snippet/create"
curl -L -i "localhost:4000/snippet/view?id=4"
```