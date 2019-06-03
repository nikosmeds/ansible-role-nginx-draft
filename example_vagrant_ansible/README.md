# Example Vagrant and Ansible deployment

Deploy Prometheus monitoring and Grafana dashboard systems.

## 1. Install Vagrant

Visit https://www.vagrantup.com/ and install latest version of `vagrant`.

## 2. Install required packages

Create a Python virtual environment and install required packages.
Ensure you are working from the project directory.

```
cd example_vagrant_ansible/
```

Install Python virtual environments package.

```
pip install virtualenv
```

Create a virtual environment in the project.

Note that ideally we would not include `--system-site-packages` in the following command, however there seems to be a bug with certain Ansible modules when running in a Python virtual environment on CentOS 7 hosts. Feel free to experiment both with and without this flag. See https://github.com/trailofbits/algo/issues/356.

```
virtualenv -p /usr/bin/python --system-site-packages venv
source venv/bin/activate
```

Install required packages.

```
pip install -r requirements.txt
```

Install required Ansible roles.

```
ansible-galaxy install -r roles/requirements.yml
```

If deploying from a MacOS host, install gnu-tar (required by a number of cloudalchemy Ansible roles).

```
brew install gnu-tar
```

## 3. Deploy

Spin up VMs and configure services (takes ~10 minutes).

```
vagrant up
```

## 4. View

You can now checkout the Prometheus and Grafana UIs using the following links.

| Service | URL
| --- | ---
| Grafana | http://10.100.0.2:3000
| Prometheus | http://10.100.0.3:9090/targets

## 5. Access

You can also access these systems via SSH.

```
vagrant ssh [grafana|prometheus].test
```

## 6. Clean up

Once you are ready, delete the virtual machines.

```
vagrant destroy
```

Exit the Python virtual environment.

```
deactivate
```
