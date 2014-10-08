# 參考文件
- 8.0 中文文擋 http://twpug.net/docs/postgresql-doc-8.0-zh_TW/

# Setup (MAC)
- Init
```
initdb /usr/local/var/postgres -E utf8
```

- 設為開機啟動
```
ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgentslaunchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
```

- 啟動 server daemon
```
pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start
```

- 關閉 server daemon
```
pg_ctl -D /usr/local/var/postgres stop -s -m fast
```

# Management
建立一般 user
```
createuser [username] -P    # (-P for password prompt)
```
```
CREATE USER [username]
```

建立有建立 DB 權限的 user
```
CREATE USER name CREATEDB
```
```
createuser username -P
```

刪除 user
```
DROP USER name
```
```
dropuser username
```

建立 DB
```
createdb [DB name] -O [user name] -E UTF8 -e
```

刪除 DB
```
dropdb [DB name]
```

以預設 username (postgres) 連上 DB
```
sudo -u postgres psql postgres
```

連接 DB
```
psql -U username -d dbname -h 127.0.0.1
```

## 常用指令
- list all DBs `\l`

- list all tables `\dt`

- 連接DB `\c [db name]`

- SHOW TABLES `\d`

- SHOW DATABASES `\l`

- SHOW COLUMNS `\d table`

- DESCRIBE TABLE `\d+ table`

### ROLE 操作
- Reference
  - [How To Use Roles and Manage Grant Permissions in PostgreSQL on a VPS](https://www.digitalocean.com/community/tutorials/how-to-use-roles-and-manage-grant-permissions-in-postgresql-on-a-vps--2)

賦予 user 操作某 db 的所有權限 `GRANT ALL PRIVILEGES ON DATABASE [DB name] to [user name];`

查看 role 權限 `\du`

砍掉 role `DROP ROLE role_name;`

# Reference
- [Mac 下 PostgreSQL 的安裝與使用](http://dhq.me/mac-postgresql-install-usage)
- [Install PostgreSQL on Ubuntu](https://help.ubuntu.com/community/PostgreSQL)
