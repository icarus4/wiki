# Graph of Architecture
```
user -> nginx -> multi rails app server (puma or passenger) -> redis
     -> multi faye nodejs server -> redis
```

- using redis to sync multiple faye server
  - syn JWT ([JSON web token](http://jwt.io/)) for the users connecting to different faye server with the same channel

- using [gon](https://github.com/gazay/gon) in ?

- using [Rabl](https://github.com/nesquena/rabl) in?

- Instead of passing to Faye directly, message tasks (sent to user by Faye) are queued in RabbitMQ and AMQ (ActiveMQ?)
  - non-important tasks are queued in RabbitMQ
  - important tasks are queued in AMQ
