# CROC Cloud Ansible Dynamic Inventory

CROC Cloud Ansible Dynamic Inventory is a scripts for managing your cloud infrastructure dynamically.

## Setup

### Preparing software

1. `git clone ${THIS_REPO_URL}`
2. `cd ${THIS_REPO_NAME}`
3. `python3.6 -m venv .venv`
4. `source .venv/bin/activate`
4. `pip install -r requirements.txt`

### Setup credentials using AWS config

To use this inventory script please set up your credentials using `~/.aws/credentials` file.

Add the following to your config:

```ini
[croc]
aws_access_key_id = <YOUR_ACCESS_KEY>
aws_secret_access_key = <YOUR_SECRET_KEY>
```

Now specify your aws profile using environment variables `export AWS_PROFILE=croc`.  
Or you can pass this variable before every command `AWS_PROFILE=croc ansbile-playbook ...`

### Setup credentials using ec2.ini

You can also specify your credentials locally.  
For this modify `contrib/inventory/ec2.ini` file with:
```ini
aws_access_key_id = <YOUR_ACCESS_KEY>
aws_secret_access_key = <YOUR_SECRET_KEY>
```

## Examples

All examples located in `examples` folder.

### ansible-playbook
To execute playbook on instances marked with Tag `web_server`

__playbook.yaml__:
```yaml
- hosts: tag_Name_web_server  
  connection: local
  gather_facts: false
  tasks:
    - name: Example
      command: time
```

Use command: `ansible-playbook -i contrib/inventory/ec2.py playbook.yaml`

### ansible-inventory

To list all your hosts use  
`ansible-inventory --list -i contrib/inventory/ec2.py`
