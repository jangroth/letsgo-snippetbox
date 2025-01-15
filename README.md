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

- db setup
```sql
CREATE DATABASE snippetbox CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

USE snippetbox;

-- Create a snippets table.
CREATE TABLE snippets (
	id INTEGER NOT NULL PRIMARY KEY AUTO_INCREMENT,
	title VARCHAR(100) NOT NULL,
	content TEXT NOT NULL,
	created DATETIME NOT NULL,
	expires DATETIME NOT NULL
);

-- Add an index on the created column.
CREATE INDEX idx_snippets_created ON snippets(created);

-- App user
CREATE USER 'web'@'localhost';
GRANT SELECT, INSERT, UPDATE, DELETE ON snippetbox.* TO 'web'@'localhost';
ALTER USER 'web'@'localhost' IDENTIFIED BY 'pass';

-- Session
CREATE TABLE sessions (
    token CHAR(43) PRIMARY KEY,
    data BLOB NOT NULL,
    expiry TIMESTAMP(6) NOT NULL
);
CREATE INDEX sessions_expiry_idx ON sessions (expiry);

-- User
CREATE TABLE users (
    id INTEGER NOT NULL PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    hashed_password CHAR(60) NOT NULL,
    created DATETIME NOT NULL
);
ALTER TABLE users ADD CONSTRAINT users_uc_email UNIQUE (email);
```