### Install `.deb` Packages (Debian-based)

```sh
sudo dpkg -i <package_name>.deb
```

### Install `.rpm` Packages using `alien`

```sh
sudo apt install alien
sudo alien -i <package_name>.rpm
```

---

## Download Java (Oracle JDK 17)

```sh
wget https://download.oracle.com/java/17/archive/jdk-17.0.12_linux-x64_bin.deb

sudo apt install ./jdk-17.0.12_linux-x64_bin.deb

java --version
```

---

## Download Maven

```sh
wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz

tar -xvf apache-maven-3.9.9-bin.tar.gz
sudo mv apache-maven-3.9.9 /opt/
```

## Configure Environment Variables

```sh
vim ~/.bashrc

export M2_HOME='/opt/apache-maven-3.9.9'
export PATH="$M2_HOME/bin:$PATH"

source ~/.bashrc
```

---

## Install Git

```sh
sudo apt install git-all

git --version
```

---

## Download & Install Docker

```sh
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

sudo usermod -aG docker $USER
newgrp docker

sudo systemctl enable docker
sudo systemctl start docker

sudo systemctl status docker
```
