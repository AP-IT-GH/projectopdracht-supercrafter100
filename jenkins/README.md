# Add user on machine for jenkins
```bash
sudo useradd -m -s /bin/bash jenkins
sudo usermod -aG docker jenkins
sudo su jenkins
cd
mkdir .ssh
touch .ssh/authorized_keys
cat id_rsa.pub | sudo tee -a /home/jenkins/.ssh/authorized_keys
```

# Note of issue happened during project deployment
The `env_file` section of the database and backend service made it so the .env file was required to exist during deployment. However, Jenkins doesn't supply the .env file but rather directly sets them instead. By looking at the [docker compose documentation](https://docs.docker.com/compose/environment-variables/set-environment-variables/) I realized that if you don't include the env_file section, it will still load environmental variables straight out of the .env file. So this could be left out making the build succeed.