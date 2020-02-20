## Solution to Peer Authentication Failed:

 1. Open the file: ``/etc/postgresql/9.1/main/pg_hba.conf*`` on nano.
 2. Modify:
 
 ```local   all             postgres                                peer```
 
 **AS**
 
 ```local   all             postgres                                md5```

## Accessing Postgres through terminal
``sudo -u postgres psql``


## Import Sql File

``sudo -u postgres psql db_name < 'file_path'
``

[Details](https://stackoverflow.com/a/26610212/10901575)

[Use This tool for database conversion](https://www.rebasedata.com/)



