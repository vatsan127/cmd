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

### Install Java (Oracle JDK 17)

```sh
wget https://download.oracle.com/java/17/archive/jdk-17.0.12_linux-x64_bin.deb

sudo apt install ./jdk-17.0.12_linux-x64_bin.deb

java --version
```

---

### Install Maven

```sh
wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz

tar -xvf apache-maven-3.9.9-bin.tar.gz
sudo mv apache-maven-3.9.9 /opt/
```

```sh
vim ~/.bashrc

export M2_HOME='/opt/apache-maven-3.9.9'
export PATH="$M2_HOME/bin:$PATH"

source ~/.bashrc
```

---

### Install Git

```sh
sudo apt install git-all

git --version
```

---

### Install Docker

```sh
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

sudo usermod -aG docker $USER
newgrp docker

sudo systemctl enable docker
sudo systemctl start docker

sudo systemctl status docker
```

### Postgres installation

```
sudo apt install curl ca-certificates
```

```
sudo install -d /usr/share/postgresql-common/pgdg
```

```
sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc
```

```
sudo sh -c 'echo "deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```

```
sudo apt update
```

```
sudo apt -y install postgresql-17
```

#### user setting

```
sudo -i -u postgres
psql -d
CREATE ROLE steve WITH LOGIN SUPERUSER PASSWORD 'password';
```

---