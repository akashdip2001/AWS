## CI
#### continius Intregation
1. Docker: check & Run the code
2. GitHub: Take from Devloper
3. AWS-EC2 : run in Cloud

## CD
#### automate the above process using pipe-line (continous Deployment)
4. jenkins

# ========================= Process

# ✈️ 1. Create EC2 instance (ap-south-1 : Mumbai)

  <p>
  <img width="40%" src="https://github.com/user-attachments/assets/5da24da5-a6ec-4c30-a180-3aeadf1af7be"> 
  <img width="40%" src="https://github.com/user-attachments/assets/eaae6b0b-ce20-4f92-82f2-6214df0ce16c">
  </p>
  <p>
  <img width="40%" src="https://github.com/user-attachments/assets/1bc8dac4-49b1-43e9-843e-02ba657b28fa">
  <img width="40%" src="https://github.com/user-attachments/assets/5d551320-3f19-42ef-8384-253cfb1d6c3b">
  </p>
  <p>
  <img width="40%" src="https://github.com/user-attachments/assets/d67416f5-fb96-415b-8e8c-477b20325b2e">
  <img width="40%" src="https://github.com/user-attachments/assets/e8f5efc5-e2ac-4474-9d0d-ecac4d4fcbc6">
  </p>
  
# ✈️ 2. Copy the `.pem` from Windows-11 to Linux/Docoments

  <details aline="center">
  <p>
   <img width="40%" src="https://github.com/user-attachments/assets/be707424-cd0f-4521-a1a4-76a349a6c93b">
   <img width="40%" src="https://github.com/user-attachments/assets/e1b14964-a661-455a-bb68-da5c86078e15">
  </p>
  </details>
  
# ✈️ 3. SSH connect

```
ssh -i <name>.pem ubuntu@<ip>
```
<details aline="center">
<p>  
 <img width="40%" src="https://github.com/user-attachments/assets/d2ef2a28-8e8b-4fd3-b793-54991fbaf7bd">
 <img width="40%" src="https://github.com/user-attachments/assets/c5ccdd58-78ed-408f-94ac-991caad0720a">
</p>
</details>

# ✈️ 4. install Jenkins

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

</br>

![Screenshot (751)](https://github.com/user-attachments/assets/ea1fda05-19f9-4295-8784-e021aca0a714)

  ##### 🔑 passward: in this file
  ```
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  ```
  install suggested Plugins
  <p aline="centre">
   <img width="40%" src="https://github.com/user-attachments/assets/340af1d4-ed0a-4a9e-99e4-6dd63ace2ba2">
   <img width="40%" src="https://github.com/user-attachments/assets/de02a60e-4a9f-4e59-83cb-287372a73e85">
  </p>
---

### **6. (Optional) Configure Jenkins**
- Set up **JDK** installations, Git, Maven, etc., for building projects.
- Integrate Jenkins with version control systems (e.g., GitHub, GitLab).

---

### **7. Test Jenkins**
- Create a sample job to verify that Jenkins is working properly.

<p>
 <img width="40%" src="https://github.com/user-attachments/assets/bb0a697e-0073-43fa-8ab4-57d7e5ae30f3">
 <img width="40%" src="https://github.com/user-attachments/assets/3cf53f11-5bea-49f6-a69d-694fcb56c844">
</p>

```
http://65.2.63.129:8080/
```

</br>


# ✈️ 5. Create a new Project in Jenkines

</br>

<p>
 <img width="40%" src="https://github.com/user-attachments/assets/877ef0dc-ab17-435b-a4c3-731ada92a4a9">
 <img width="40%" src="https://github.com/user-attachments/assets/686b5df9-a738-4445-930e-37c891229778">
</p>

```
https://github.com/akashdip2001/node-todo-cicd
```

</br>


# ✈️ 6. Connect GitHub with AWS using SSH

```
ssh-keygen
cd .ssh
cat id_ed25519.pub
```

</br>

<p>
 <img width="40%" src="https://github.com/user-attachments/assets/bcadd3f3-3453-4574-9a62-f6bf65989d39">
 <img width="40%" src="https://github.com/user-attachments/assets/85ed3549-d31c-4286-b4dc-fc8dfd1496c6">
</p>
<p>
 <img width="40%" src="https://github.com/user-attachments/assets/4b5974cd-ea7f-4fa9-89b5-9d0d41350ea6">
 <img width="40%" src="https://github.com/user-attachments/assets/57bd4c13-83b0-40c6-894c-525d0ad5ffd0">
</p>

</br>


# ✈️ 7. create PipeLine --> CI

</br>

<p>
 <img width="40%" src="https://github.com/user-attachments/assets/0931c062-06cf-41a8-b0d8-afa8cb6ac7ba">
 <img width="40%" src="https://github.com/user-attachments/assets/fef652ed-175c-477a-b04d-29bcceecf58f">
</p>
<p>
 <img width="40%" src="https://github.com/user-attachments/assets/d5f57ba2-5748-47cc-9509-813bc1af09aa">
 <img width="40%" src="https://github.com/user-attachments/assets/6fa7dfc2-9455-48e4-8cd1-45680e1c5c1d">
</p>
<p>
 <img width="40%" src="https://github.com/user-attachments/assets/e946cb95-f374-403e-8323-decf18da6512">
 <img width="40%" src="https://github.com/user-attachments/assets/acb91929-1953-42ee-9c7d-f933ca5fdfba">
</p>

</br>


# ✈️ 8. Run the app

</br>


![Screenshot (772)](https://github.com/user-attachments/assets/9aecfd8b-bdb1-491d-a701-01ef007a5e93)
![Screenshot (774)](https://github.com/user-attachments/assets/7e32d3a9-879e-438b-95f5-13593e58ad8f)
![Screenshot (776)](https://github.com/user-attachments/assets/3549908b-71a3-4616-98a2-1ce0f8555aad)

</br>


```
http://65.2.63.129:8000
```

</br>


![Screenshot (777)](https://github.com/user-attachments/assets/a444768b-c84c-4193-9a29-eba5fd739638)

# ✈️ 9. CD

</br>

<p aline="center">
  <img src="https://github.com/user-attachments/assets/0c4c13fa-ac64-4650-ad36-ac773a0a2e8e" width="45%">
  <img src="https://github.com/user-attachments/assets/da6b9202-ff84-49fe-a1b5-1f8ba865637d" width="45%">
</p>

### for this we setup Docker
