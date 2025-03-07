# Server Setup

## Install Packages

```bash
# Debian
sudo dpkg -i <package_name>.deb
```

```bash
# using alien RPM
sudo apt install alien
sudo alien -i tabby-1.0.207-linux-x64.rpm
```

## Java

```bash
wget https://download.oracle.com/java/17/archive/jdk-17.0.12_linux-x64_bin.deb
```

```bash
sudo apt install jdk-17.0.12_linux-x64_bin.deb
```

```bash
java --version
```

---

## Maven

```bash
wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz
```

```bash
tar -xvf apache-maven-3.9.9-bin.tar.gz
```

```bash
sudo mv apache-maven-3.9.9 /opt/
```

```bash
vim ~/.bashrc
```

```bash
M2_HOME='/opt/apache-maven-3.9.9'
PATH="$M2_HOME/bin:$PATH"
```

```bash
source ~/.bashrc
```

---

## Git

```bash
sudo apt install git-all
```

```bash
git --version
```

---

## Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
```

```bash
sudo sh get-docker.sh
```

```bash
sudo usermod -aG docker $USER
```

```bash
newgrp docker
```

```bash
sudo systemctl enable docker
```

```bash
sudo systemctl status docker
```