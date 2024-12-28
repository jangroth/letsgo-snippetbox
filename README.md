## Golang Snippetbox

### mysql

- Start mysql
```
/opt/homebrew/opt/mysql/bin/mysqld_safe --datadir\=/opt/homebrew/var/mysql
```

- Start application
```
go run ./cmd/web
```
- Log into DB
```
mysql -D snippetbox -u web -p
```