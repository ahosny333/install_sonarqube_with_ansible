# SonarQube Installation with Ansible

This repository contains an Ansible playbook to automate the installation and configuration of SonarQube on a Linux machine. The playbook sets up the required dependencies, configures PostgreSQL as the database, and ensures SonarQube runs as a systemd service.

## 📌 Prerequisites

Before running the playbook, ensure you have:

- Ansible installed on your machine.
- A Linux-based system (tested on Ubuntu).
- sudo privileges for installation.
- PostgreSQL installed (handled by the playbook if missing).

## 📂 Playbook Overview

The playbook performs the following tasks:

- **Installs dependencies**: Java (OpenJDK 11), PostgreSQL, Python packages, and other required tools.
  
- **Configures PostgreSQL**:
  - Creates a dedicated SonarQube database and user.
  - Grants the necessary privileges.
  
- **Downloads and extracts SonarQube**.
  
- **Configures SonarQube**:
  - Updates database credentials in `sonar.properties`.
  - Sets the web server host to `0.0.0.0` for external access.
  - Creates a system user for SonarQube.
  - Sets proper permissions for the installation.
  
- **Creates a systemd service for managing SonarQube**.
  - Enables and starts the SonarQube service on system boot.

## 🛠 How to Use

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/yourusername/ansible-sonarqube.git
cd ansible-sonarqube
```

### 2️⃣ Update Variables (Optional)

Modify the `vars` section in the playbook if needed:

```yaml
vars:
  pw: ahmed # Change this to set your PostgreSQL password
  sonarqube_version: "9.9.0.65466" # Update to the desired SonarQube version
```

### 3️⃣ Run the Playbook

Execute the Ansible playbook:

```bash
ansible-playbook -i inventory sonar.yml
```
### 4️⃣ Verify the Installation  

Check the SonarQube service status:  

```bash
systemctl status sonarqube
```
##### SonarQube Access  

SonarQube should be running at:  

[http://localhost:9000](http://localhost:9000)  

**Default login credentials:**  

- **Username:** `admin`  
- **Password:** `admin`  

### 5️⃣ Managing SonarQube Service  

Start, stop, or restart SonarQube with:  

```bash
sudo systemctl start sonarqube
sudo systemctl stop sonarqube
sudo systemctl restart sonarqube
```

## 🔥 Troubleshooting  

#### Check logs:  
```bash
journalctl -u sonarqube -f
```

#### Ensure PostgreSQL is running:  
```bash
systemctl status postgresql
```
#### Verify Java version  
```bash
java -version
```
Ensure Java 11 is installed and set as the default.

---

## 📜 License

This project is licensed under the **MIT License**.

---

## 📧 Contact

For any issues, feel free to open an issue in the repository or contact me at **ahmed.hosny@the-diy-life.co**.

---

🚀 **Happy Coding with SonarQube!** 🎯
