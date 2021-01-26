## Description
When running `./setup`, on the `Setup Zed` step, the following error occurs:

```php
Zed Exception: RuntimeException - psql: FATAL:  Peer authentication failed for user "postgres"
```

## Solution
Open the PostgreSQL configuration file :

```bash
sudo vim /etc/postgresql/9.4/main/pg_hba.conf
```

and make sure that the first line contains the following input:

```php
TYPE      DATABASE    USER      ADDRESS     METHOD
local     all         postgres              trust
```

