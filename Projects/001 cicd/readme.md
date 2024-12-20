## CI
#### continius Intregation
1. Docker: check & Run the code
2. GitHub: Take from Devloper
3. AWS-EC2 : run in Cloud

## CD
#### automate the above process using pipe-line (continous Deployment)
4. jenkins

# ========================= Process

# 1. Create EC2 instance (ap-south-1 : Mumbai)
  <details aline="center">
       
  ![Screenshot (722)](https://github.com/user-attachments/assets/5da24da5-a6ec-4c30-a180-3aeadf1af7be)  
  ![Screenshot (723)](https://github.com/user-attachments/assets/eaae6b0b-ce20-4f92-82f2-6214df0ce16c)
  ![Screenshot (724)](https://github.com/user-attachments/assets/1bc8dac4-49b1-43e9-843e-02ba657b28fa)
  ![Screenshot (725)](https://github.com/user-attachments/assets/5d551320-3f19-42ef-8384-253cfb1d6c3b)
  ![Screenshot (726)](https://github.com/user-attachments/assets/d67416f5-fb96-415b-8e8c-477b20325b2e)
  ![Screenshot (727)](https://github.com/user-attachments/assets/e8f5efc5-e2ac-4474-9d0d-ecac4d4fcbc6)
  </details>
  
# 2. Copy the `.pem` from Windows-11 to Linux/Docoments

  <details aline="center">
    
  ![Screenshot (728)](https://github.com/user-attachments/assets/be707424-cd0f-4521-a1a4-76a349a6c93b)
  ![Screenshot (729)](https://github.com/user-attachments/assets/e1b14964-a661-455a-bb68-da5c86078e15)
  </details>
  
# 3. SSH connect

```
ssh -i <name>.pem ubuntu@<ip>
```
<details aline="center">
  
![Screenshot (730)](https://github.com/user-attachments/assets/d2ef2a28-8e8b-4fd3-b793-54991fbaf7bd)
![Screenshot (731)](https://github.com/user-attachments/assets/c5ccdd58-78ed-408f-94ac-991caad0720a)
</details>

# 4. install Jenkins

<details aline="center">
Installing Jenkins on an AWS EC2 instance :

### **1. Launch an AWS EC2 Instance**
1. **Log in to AWS Management Console**:
   - Navigate to the EC2 dashboard and click **Launch Instance**.
2. **Choose an AMI**:
   - Select an appropriate AMI, such as **Amazon Linux 2**, **Ubuntu 20.04/22.04**, or **CentOS**.
3. **Select Instance Type**:
   - Choose an instance type like `t2.micro` for testing or small-scale use (eligible for the free tier).
4. **Configure Instance Details**:
   - Ensure your instance is in a public subnet and has a public IP address.
5. **Add Storage**:
   - Use the default settings unless additional storage is needed.
6. **Configure Security Groups**:
   - Allow inbound traffic for:
     - **SSH** (port `22`) for connecting to the instance.
     - **HTTP** (port `80`) for accessing Jenkins on a web browser.
     - **Custom TCP** (port `8080`) for Jenkins (optional, if required).
7. **Launch and Connect**:
   - Launch the instance with an existing key pair or create a new one.
   - Connect to the instance using SSH:
     ```bash
     ssh -i /path/to/key.pem ec2-user@<public-ip>
     ```
</details>
---

### **2. Install Jenkins**
#### **Step 1: Update the System**
Run the following commands to update the system packages:

```bash
sudo apt update && sudo apt upgrade -y    # For Ubuntu
sudo yum update -y                        # For Amazon Linux
```

#### **Step 2: Install Java**
Jenkins requires Java. Install it based on your operating system:

- **Ubuntu**:
  ```bash
  sudo apt install -y openjdk-11-jdk
  ```

- **Amazon Linux**:
  ```bash
  sudo yum install -y java-11-openjdk
  ```

Verify Java installation:

```bash
java -version
```

#### **Step 3: Add the Jenkins Repository**
- **Ubuntu**:
  ```bash
  curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
  sudo apt update
  ```

- **Amazon Linux**:
  ```bash
  sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
  sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
  ```

#### **Step 4: Install Jenkins**
- Install Jenkins using the package manager:
  - **Ubuntu**:
    ```bash
    sudo apt install -y jenkins
    ```
  - **Amazon Linux**:
    ```bash
    sudo yum install -y jenkins
    ```

---

### **3. Start and Enable Jenkins**
1. Start the Jenkins service:
   ```bash
   sudo systemctl start jenkins
   ```
2. Enable Jenkins to start on boot:
   ```bash
   sudo systemctl enable jenkins
   ```

3. Check Jenkins' status:
   ```bash
   sudo systemctl status jenkins
   ```

---

### **4. Open Firewall Ports**
#### Update Security Group:
- Allow inbound traffic on port `8080` (for Jenkins).
- Go to **EC2 > Security Groups > Edit Inbound Rules** and add:
  - Type: **Custom TCP Rule**
  - Port Range: **8080**
  - Source: **0.0.0.0/0** (or restrict to your IP for better security).

#### Update Firewall (if needed):
- On the instance, use:
  ```bash
  sudo ufw allow 8080/tcp       # Ubuntu
  sudo firewall-cmd --add-port=8080/tcp --permanent  # Amazon Linux
  sudo firewall-cmd --reload
  ```

---

### **5. Access Jenkins**
1. Open a browser and navigate to:
   ```
   http://<public-ip>:8080
   ```
2. Unlock Jenkins:
   - Retrieve the initial admin password:
     ```bash
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword
     ```
   - Copy the password and paste it into the Jenkins setup page.

3. Install Recommended Plugins:
   - Follow the on-screen instructions to install plugins and create an admin user.

---

### **6. (Optional) Configure Jenkins**
- Set up **JDK** installations, Git, Maven, etc., for building projects.
- Integrate Jenkins with version control systems (e.g., GitHub, GitLab).

---

### **7. Test Jenkins**
- Create a sample job to verify that Jenkins is working properly.

