![Screenshot (530)](https://github.com/user-attachments/assets/7dcc9916-2ee5-4216-a2dc-209cf84fb49b)
![Screenshot (531)](https://github.com/user-attachments/assets/641fc748-27c1-448a-84b6-8e6a6f94d8e9)

[<img align="right" alt="GitHub Foundations exam logo" width="300" src="https://github.com/akashdip2001/akashdip2001/raw/main/img/Badge/aws-educate-getting-started-with-security.png">](https://www.credly.com/badges/6ea09b08-c1f7-4035-ae3b-bf921004d224/public_url) 

---

### **Task 1: Explore the Users and Groups**
1. **Sign into the AWS Console**:
   - Start the lab, ensure the lab status is ready, and then click on **AWS** to open the Management Console. The system automatically signs you in.

     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
              
        ![Screenshot (558)](https://github.com/user-attachments/assets/29863efc-8dc7-41b6-8cf1-e71979580237)
        ![Screenshot (533)](https://github.com/user-attachments/assets/73edddec-eb9e-406e-abdc-bec73c412810)
        ![Screenshot (534)](https://github.com/user-attachments/assets/34cfc6f1-e637-4b98-9322-5ce552157c42)
      </details>

2. **Navigate to IAM**:
   - In the AWS Management Console, go to **Services** → **Security, Identity, & Compliance** → **IAM**.

     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
        
        ![Screenshot (535)](https://github.com/user-attachments/assets/a355d64e-f5e8-4378-a04e-d2e8cd0a718a)
        ![Screenshot (536)](https://github.com/user-attachments/assets/752035ae-6419-4b81-8e56-bf0ac22454dc)
      </details>        

3. **View IAM Users**:
   - In the IAM dashboard, click **Users** from the left navigation pane.
   - Note the three users (`user-1`, `user-2`, `user-3`).
  
     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
     
        ![Screenshot (537)](https://github.com/user-attachments/assets/e86c439a-90f9-4619-bcb4-45978b8c5034)
      </details> 

4. **Inspect User-1**:
   - Click on `user-1` and review the following:
     - **Permissions Tab**: Notice no permissions are assigned.
     - **Groups Tab**: Notice no group memberships.
     - **Security Credentials Tab**: Verify that `user-1` has a console password.
    
       <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
          
          ![Screenshot (538)](https://github.com/user-attachments/assets/bf9e6f85-55d4-46fe-a37b-8f2d18520a58)
          ![Screenshot (539)](https://github.com/user-attachments/assets/d4fec680-7c74-4226-9a6c-a7e25464a300)
          ![Screenshot (540)](https://github.com/user-attachments/assets/0ac2f4e3-7f5b-476a-b6cf-857988190d77)
      </details> 

5. **Inspect Pre-Created Groups**:
   - In the left navigation pane, choose **User groups**.
   - Review the following groups:
     - `EC2-Admin` (contains an inline policy `EC2-Admin-Policy`).
     - `EC2-Support` (attached managed policy `AmazonEC2ReadOnlyAccess`).
     - `S3-Support` (attached managed policy `AmazonS3ReadOnlyAccess`).
    
       <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
          
          ![Screenshot (541)](https://github.com/user-attachments/assets/8108840c-fb68-4949-94db-c4e19f9ff869)
      </details> 

6. **Review Permissions**:
   - Open each group and review their attached policies under the **Permissions tab**. Use the JSON view to understand the actions (`Action`) and resources (`Resource`) allowed or denied.
  
     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
        
        ![Screenshot (542)](https://github.com/user-attachments/assets/0065e173-8f6f-461a-b485-a2dc45130b92)
      </details> 

---

### **Task 2: Add Users to Groups**
You will now assign each user to their respective groups based on their roles.

1. **Add `user-1` to `S3-Support`**:
   - Navigate to **User groups** in the left pane.
   - Click on `S3-Support`.
   - Go to the **Users tab** → **Add users** → Select `user-1` → Click **Add users**.
  
     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
        
        ![Screenshot (543)](https://github.com/user-attachments/assets/60cffdff-bba8-4d3b-a63c-3c75fb4440f1)
        ![Screenshot (544)](https://github.com/user-attachments/assets/3ce2f691-bb25-4ee3-b284-c30bfe879ad1)
        ![Screenshot (545)](https://github.com/user-attachments/assets/1dbb4300-21e3-4b35-a3b0-bddcfc51b664)
      </details> 

2. **Add `user-2` to `EC2-Support`**:
   - Repeat the same process for the `EC2-Support` group and add `user-2`.
  
     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
        
        ![Screenshot (541)](https://github.com/user-attachments/assets/bf2eebc4-d653-4789-880e-b1be32d7d87a)
        ![Screenshot (543 1)](https://github.com/user-attachments/assets/1829f877-e136-4bb1-ab62-399768c6d7e0)
        ![Screenshot (546)](https://github.com/user-attachments/assets/0d64a6c5-9f00-484d-a564-6713c90c311c)
      </details> 

3. **Add `user-3` to `EC2-Admin`**:
   - Repeat the process for the `EC2-Admin` group and add `user-3`.

4. **Verify Group Memberships**:
   - Navigate back to **User groups**. Ensure each group shows **1** in the **Users column** to confirm membership.
  
     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
         
        ![Screenshot (548)](https://github.com/user-attachments/assets/3cd946e5-b18f-41d6-b1c6-a1c0bdff3f74)
      </details> 

---

### **Task 3: Sign in and Test Users**
You will now test the permissions of each user to confirm that the correct policies are applied.

#### **Get the IAM Console Sign-In URL**:
1. Go to **Dashboard** in IAM and copy the **Sign-in URL for IAM users**.
   <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
      
      ![Screenshot (550)](https://github.com/user-attachments/assets/1e6e104c-4d01-4e3b-9f30-0a0c37573ce6)
      </details> 
2. Open a private/incognito browser window and use the link to sign in.
   <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary> 
      
      ![Screenshot (552)](https://github.com/user-attachments/assets/e85d8825-c180-4032-a95e-a046b6bf81d7)
      </details> 

#### **Test `user-1` Permissions**:
1. Sign in as `user-1` with the credentials:
   - IAM user name: `user-1`
   - Password: `Lab-Password1`
     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
        
        ![Screenshot (553)](https://github.com/user-attachments/assets/09e6ed8b-3212-44c3-9a70-fab4b085d5b8)
      </details> 
2. Go to **Services** → **S3**:
   - Confirm you can view bucket contents (read-only access).
     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
        
        ![Screenshot (554)](https://github.com/user-attachments/assets/d6c9eed2-0072-4e5f-8390-dfc910af2a0f)
        ![Screenshot (555)](https://github.com/user-attachments/assets/65393d44-3898-49d1-97f5-0577f82a91c8)
      </details> 
3. Go to **Services** → **EC2**:
   - Verify that you cannot view EC2 instances (no permissions for EC2).
     <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
        
        ![Screenshot (556)](https://github.com/user-attachments/assets/6058ddf8-50fa-4a03-a680-7d115806e012)
        ![Screenshot (557)](https://github.com/user-attachments/assets/820432ac-c493-454b-afa4-6f4f8c21d376)
      </details> 

#### **Test `user-2` Permissions**:
1. Sign out `user-1` and sign in as `user-2`:
   - IAM user name: `user-2`
   - Password: `Lab-Password2`
2. Go to **Services** → **EC2**:
   - Confirm you can view instances but cannot perform actions like stopping them.
3. Go to **Services** → **S3**:
   - Confirm that you do not have access to any buckets.

#### **Test `user-3` Permissions**:
1. Sign out `user-2` and sign in as `user-3`:
   - IAM user name: `user-3`
   - Password: `Lab-Password3`
2. Go to **Services** → **EC2**:
   - Confirm you can view instances and successfully stop an instance (admin permissions).
3. Go to **Services** → **S3**:
   - Confirm that you do not have access to any buckets.

---

### **End the Lab**
1. After testing all users, close the private browser window.
2. Return to the lab instructions tab and select **End Lab**.
   <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
      
      ![Screenshot (559)](https://github.com/user-attachments/assets/a1412bee-27b0-42fa-964e-2e4c416ae983)
      </details> 
3. Confirm that the lab is terminated.
   <details>	
          <summary><b><img src="https://github.com/akashdip2001/git-github/raw/main/source/img_logo.png" width="20"/> img guide.</b></summary>
      
      ![Screenshot (560)](https://github.com/user-attachments/assets/73b5f204-9acf-4e99-a296-65ed2a3ee32f)
      </details> 

---

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

[<img align="right" alt="GitHub Foundations exam logo" width="300" src="https://github.com/akashdip2001/akashdip2001/raw/main/img/Badge/aws-educate-getting-started-with-security.png">](https://www.credly.com/badges/6ea09b08-c1f7-4035-ae3b-bf921004d224/public_url) 

### **Question 1**  
Which is AWS's responsibility under the AWS shared responsibility model?  
- [ ] Granting access to customer data  
- [ ] Configuring for public or private access for VPCs  
- [ ] Security group configurations  
- [x] Maintaining physical hardware  

**Explanation:**  
AWS is responsible for maintaining the physical hardware and infrastructure that underpins the cloud services. Customers handle configurations and data management.

---

### **Question 2**  
Which is a best practice in IAM concerning the root user?  
- [ ] Do not enable MFA for the root user.  
- [ ] Share the root user account login credentials with at least one other administrator.  
- [ ] Use the root user for daily administration tasks.  
- [x] Do not use root account credentials for day-to-day interactions with AWS.  

**Explanation:**  
The root user is powerful and should only be used for critical account-wide tasks. For daily tasks, create individual IAM users with the necessary permissions.

---

### **Question 3**  
An IAM policy that allows access to an Amazon S3 bucket is attached to an IAM user. The Amazon S3 bucket has a bucket policy that denies the IAM user access to the bucket.  
Which statement is true about the conflicting IAM and resource policies?  
- [ ] A resource policy always overrides an IAM policy. The IAM user cannot access the bucket.  
- [ ] A policy with an allow statement overrides an allow statement. The IAM user can access the bucket.  
- [x] A policy with a deny statement overrides an allow statement. The IAM user cannot access the bucket.  
- [ ] An IAM policy always overrides a resource policy. The IAM user can access the bucket.  

**Explanation:**  
In AWS, **deny** statements always take precedence over allow statements. Even if an IAM policy allows access, a deny in the resource policy will block access.

---

### **Question 4**  
Which service would you use to authenticate and authorize users on your web application?  
- [ ] Amazon KMS  
- [x] Amazon Cognito  
- [ ] Amazon Secrets Manager  
- [ ] IAM  

**Explanation:**  
Amazon Cognito provides authentication, authorization, and user management for your web and mobile apps. You can use it to allow users to sign in and control their access to resources.

---

### **Question 5**  
Which section on the IAM policy statement determines whether the user's access is being allowed or denied?  
- [ ] Statement  
- [ ] Action  
- [x] Effect  
- [ ] Resource  

**Explanation:**  
The **Effect** field in a policy explicitly states whether the policy allows or denies the specified action. Example: `"Effect": "Allow"`.

---

### **Question 6**  
Which two services are designed specifically for data protection? (Choose TWO)  
- [ ] GuardDuty  
- [ ] Amazon Inspector  
- [ ] Amazon Cognito  
- [x] Secrets Manager  
- [x] AWS KMS  

**Explanation:**  
AWS KMS (Key Management Service) manages encryption keys, and Secrets Manager stores sensitive information like passwords securely.

---

### **Question 7**  
Which statement is true in regards to what is required for a user to assume a role?  
- [ ] All IAM users can assume roles in an AWS account, unless a deny policy specifies that they cannot.  
- [x] The user needs to be defined as the principal that you trust to assume the role in the trust policy.  
- [ ] The user needs to be defined as the principal that you trust to assume the role in the user's IAM policy.  
- [ ] All IAM users can assume roles in an AWS account.  

**Explanation:**  
A trust policy on the role specifies who (which principal) can assume it. This is a critical component of cross-account access.

---

### **Question 8**  
You want an added layer of security to authenticate a user when the user logs in. What should you do?  
- [ ] Place the IAM user in a specific IAM group  
- [x] Enable multi-factor authentication (MFA) on the IAM user's account  
- [ ] Delete the IAM user's access keys  
- [ ] Use Amazon Inspector  

**Explanation:**  
Enabling **MFA** provides an additional layer of security by requiring a one-time password (OTP) or similar token for login.

---

### **Question 9**  
Which service helps protect your application on AWS from DDoS attacks?  
- [x] Shield  
- [ ] GuardDuty  
- [ ] Secrets Manager  
- [ ] Amazon Inspector  

**Explanation:**  
AWS Shield offers managed protection against distributed denial-of-service (DDoS) attacks, ensuring availability of your applications.

---

### **Question 10**  
What can you do in IAM to help you evaluate whether the principle of least privilege is being enforced? (Choose TWO)  
- [ ] Use the IAM credential report to perform audits.  
- [x] Use the IAM Access Analyzer to help fine-grain the IAM users' permissions.  
- [x] Provide the IAM user with a limited set of permissions and increase as needed.  
- [ ] Provide the IAM user with a broad set of permissions and scale back as needed.  
- [ ] Create a single IAM user and provide the login credentials to users with the same job functions.
 
</br>

**Explanation:**  

AWS emphasizes **least privilege** as a best practice to secure cloud environments. Let’s break down why **"Use the IAM Access Analyzer"** and **"Provide the IAM user with a limited set of permissions and increase as needed"** are the correct answers.

</br>

### ✈️ **Correct Answer 1: Use the IAM Access Analyzer to help fine-grain the IAM users' permissions**

**Explanation:**
The IAM Access Analyzer evaluates permissions policies to help identify resources that are shared with external entities or may have excessive permissions. It provides insights that help refine policies to ensure only necessary permissions are granted.

**Example and Process:**
1. Navigate to the IAM Management Console.
2. Open **Access Analyzer** under the IAM section.
3. Review the findings, which highlight policies that are overly permissive or expose resources unnecessarily.
4. Modify the identified policies to restrict access based on the findings.

This tool directly supports the principle of least privilege by making it easier to identify and mitigate unnecessary access.

</br>

### ✈️ **Correct Answer 2: Provide the IAM user with a limited set of permissions and increase as needed**
**Explanation:**
Instead of granting broad permissions and later scaling them back (which can lead to potential misuse or security risks), it's safer to start with minimal permissions and add more as required.

**Example and Process:**
1. **Step 1: Create a policy with minimal permissions.**
   - For example, if the user only needs access to an S3 bucket for read-only purposes, create a policy like:
     ```json
     {
       "Version": "2012-10-17",
       "Statement": [
         {
           "Effect": "Allow",
           "Action": "s3:GetObject",
           "Resource": "arn:aws:s3:::example-bucket/*"
         }
       ]
     }
     ```
2. **Step 2: Monitor activity.**
   - Use CloudTrail logs to assess which actions the user attempts that might be blocked by the limited policy.
3. **Step 3: Incrementally add permissions.**
   - As the user's needs grow, append additional actions or resources to the policy.

This ensures the user has only the permissions necessary for their role at any given time.

</br>

### ✈️ Why Not Start with Broad Permissions?
Granting broad permissions and scaling back later risks creating security gaps. It may allow the user to perform actions unintentionally during the interim period before restrictions are applied.

By starting small and using tools like **IAM Access Analyzer**, you maintain a secure and controlled environment, gradually refining permissions as actual needs are identified.

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">


