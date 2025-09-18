To Install PostgreSQL:
``` Bash
sudo apt install postgresql postgresql-contrib
```

To check if PostgreSQL is running in the background:
``` bash
sudo systemctl status postgresql
```

Connect to PostgreSQL:
```bash
sudo -su postgres psql 
```

Creating User: 
```Bash
sudo -u postgres createuser <username>
```

Creating Database:
```bash 
sudo -u postgres createdb <dbname>
```

Giving the user a password:
```bash
sudo -u postgres psql
```

```postgres
alter user <username> with encrypted password '<password>';
```

```
alter user anurag with encrypted password asrblaze;
```

**Granting privileges' on Database:**

```bash
sudo -u postgres psql
```

```sql
GRANT ALL PRIVILEGES ON DATABASE "<dbname>" TO <username>;
```

eg,
```sql
GRANT ALL PRIVILEGES ON DATABASE "tourismDB" TO anurag;
```

Let's say you still are not able to create the schema and PgAdmin4 gives you this error stating that "Permission denied", then follow this:
![[Pasted image 20250709095523.png]]

Command to list all PostgreSQL users (roles)
```bash
sudo -u postgres psql -c "\du"
```

Output:
![[Pasted image 20250708212720.png]]

Command to list all Databases: 
```bash
sudo -u postgres psql -c "\list"
```

Output:
![[Pasted image 20250708212943.png]]

### Should I delete dbs like postgres, template0 or template1 ?

❌ **No, you should NOT delete the default PostgreSQL databases** like `postgres`, `template0`, or `template1`.
Here’s why:

### 🔍 Default PostgreSQL Databases:

| Database    | Purpose                                                                                   |
| ----------- | ----------------------------------------------------------------------------------------- |
| `postgres`  | A default administrative database — often used for initial connections.                   |
| `template0` | A pristine template DB. Used when creating a new DB with no customizations.               |
| `template1` | The default template used when you run `createdb`. Customizations to this affect new DBs. |

### ⚠️ What happens if you delete them?

- **Deleting `postgres`** might break scripts or tools that assume it's there.
- **Deleting `template1` or `template0`** will break the ability to create new databases normally.    
- You could cause PostgreSQL to malfunction or prevent new DB creation.

### ❌Command to delete a database

Deleting a database is **permanent** — all data inside it will be lost.  
Make sure to back up anything important before proceeding.
```bash
sudo -u postgres dropdb mydb
```

### ❗ If You Get an Error Like:

> `ERROR: database "mydb" is being accessed by other users`

It means someone (maybe you) is connected to the database.

✅ To forcefully disconnect users and drop it:
```bash
sudo -u postgres psql -c "SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname = 'anurag-dbs';"
sudo -u postgres dropdb anurag-dbs
```

Command to list all users connected to a database:
```bash
sudo -u postgres psql -c "SELECT pid, usename, application_name, client_addr, backend_start FROM pg_stat_activity WHERE datname = 'anurag-dbs';"
```
