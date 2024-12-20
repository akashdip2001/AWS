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

Installing Jenkins on an AWS EC2 instance :

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

#### **Step 3: [Add the Jenkins Repository](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu)**

![Screenshot (740)](https://github.com/user-attachments/assets/ccf5a248-31d0-46e4-8419-7e2e5ee12f46)

#### **Step 4: Install Jenkins**
- Install Jenkins using the package manager:
  - **Ubuntu**:
    ```bash
    sudo apt-get install jenkins
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
![Screenshot (741)](https://github.com/user-attachments/assets/8376c685-8542-4235-a22f-835165ac6855)

#### SOLUTION ✅

<details aline="center">
  
🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
```
sudo journalctl -xeu jenkins.service
```
![Screenshot (742)](https://github.com/user-attachments/assets/7fd5c381-b569-4c56-a196-5956d0b80576)
```
sudo ls -l /var/log/jenkins
sudo cat /var/log/jenkins/jenkins.log
df -h
JAVA_ARGS="-Djava.awt.headless=true"
sudo systemctl restart jenkins
systemctl daemon-reload
```
![Screenshot (743)](https://github.com/user-attachments/assets/15264f9a-33d7-4e4e-8641-56f922c98428)

```
sudo systemctl restart jenkins
sudo systemctl status jenkins
```
![Screenshot (744)](https://github.com/user-attachments/assets/ad3de3c6-6262-46aa-8539-e59e61916fe5)
![Screenshot (745)](https://github.com/user-attachments/assets/1ac484fd-a667-4d3f-b4a6-4ee5f6460553)

🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
</details>

---

### **4. Open Firewall Ports**
#### ✅ Update Security Group:
- Allow inbound traffic on port `8080` (for Jenkins).
- Go to **EC2 > Security Groups > Edit Inbound Rules** and add:
  - Type: **Custom TCP Rule**
  - Port Range: **8080**
  - Source: **0.0.0.0/0** (or restrict to your IP for better security).

    <details aline="center">
     <summary><b> ✅ process in AWS</b></summary><br>
      
    ![Screenshot (747)](https://github.com/user-attachments/assets/2ff3f4a9-ea0c-4aae-b054-d3b5625024f7)
    ![Screenshot (748)](https://github.com/user-attachments/assets/45f99861-0c9d-42f7-9a03-7b0f1b83ff47)
    ![Screenshot (750)](https://github.com/user-attachments/assets/507f4d3b-1599-458d-8901-9aa11d92c7d5)

    </details>
    
  ![Screenshot (751)](https://github.com/user-attachments/assets/ea1fda05-19f9-4295-8784-e021aca0a714)

  ##### 🔑 passward: in this file
  ```
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  ```
  install suggested Plugins
  ![Screenshot (752)](https://github.com/user-attachments/assets/340af1d4-ed0a-4a9e-99e4-6dd63ace2ba2)
  ![Screenshot (753)](https://github.com/user-attachments/assets/de02a60e-4a9f-4e59-83cb-287372a73e85)

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
