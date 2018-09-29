# Connect the Server with SSH + Python

## Install the Site-Packages

```
pip install ssh
pip install paramiko
pip install scpclient
```

## Establish the SSH with Python

```python
import ssh
myclient = ssh.SSHClient()
# Generate a key
myclient.set_missing_host_key_policy(ssh.AutoAddPolicy())
# Connect the server
myclient.connect(hostname, port=2222, username=username, password=password)
```

## Run the Shell Command with Python
```python
stdin, stdout, stderr = myclient.exec_command("ls")
print stdout.read()
```

## Upload File with SCP+Python

```python
ssh = paramiko.SSHClient()
# Load or generate the host key 
ssh.load_system_host_keys()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
# Connect the server
ssh.connect(hostname, port=2222, username=username, password=password)

with closing(scpclient.Write(ssh.get_transport(), remote_path=remote_path)) as scp:
    scp.send_file(local_filename, preserve_times=True, remote_filename=remote_filename)
```
