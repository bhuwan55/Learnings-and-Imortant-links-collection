# Some important linux commands:

- **Zip multiple folders:** ``zip -r <resulting_file.zip> folder1 folder2 .... foldern``


# Connect to ssh server using ssh keys + bin bash Script:

1. Create a SSH key pair: ``ssh-keygen -t rsa``. By default key is saved at /home/user/.ssh/id_rsa
2. Copy the identification to server: ``ssh-copy-id -i ~/.ssh/path/to/file user@ip`` and enter the server password
3. Test acccess using: ``ssh user@ip``
4. Create a bash script:
```bash
#!/bin/bash
ssh root@ip
```
5. sudo chmod u+x filename
6. Now you can access executing the bash file as ``./filename``


