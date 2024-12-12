![Screenshot (530)](https://github.com/user-attachments/assets/7dcc9916-2ee5-4216-a2dc-209cf84fb49b)
![Screenshot (531)](https://github.com/user-attachments/assets/641fc748-27c1-448a-84b6-8e6a6f94d8e9)

---

### **Task 1: Explore the Users and Groups**
1. **Sign into the AWS Console**:
   - Start the lab, ensure the lab status is ready, and then click on **AWS** to open the Management Console. The system automatically signs you in.

2. **Navigate to IAM**:
   - In the AWS Management Console, go to **Services** → **Security, Identity, & Compliance** → **IAM**.

3. **View IAM Users**:
   - In the IAM dashboard, click **Users** from the left navigation pane.
   - Note the three users (`user-1`, `user-2`, `user-3`).

4. **Inspect User-1**:
   - Click on `user-1` and review the following:
     - **Permissions Tab**: Notice no permissions are assigned.
     - **Groups Tab**: Notice no group memberships.
     - **Security Credentials Tab**: Verify that `user-1` has a console password.

5. **Inspect Pre-Created Groups**:
   - In the left navigation pane, choose **User groups**.
   - Review the following groups:
     - `EC2-Admin` (contains an inline policy `EC2-Admin-Policy`).
     - `EC2-Support` (attached managed policy `AmazonEC2ReadOnlyAccess`).
     - `S3-Support` (attached managed policy `AmazonS3ReadOnlyAccess`).

6. **Review Permissions**:
   - Open each group and review their attached policies under the **Permissions tab**. Use the JSON view to understand the actions (`Action`) and resources (`Resource`) allowed or denied.

---

### **Task 2: Add Users to Groups**
You will now assign each user to their respective groups based on their roles.

1. **Add `user-1` to `S3-Support`**:
   - Navigate to **User groups** in the left pane.
   - Click on `S3-Support`.
   - Go to the **Users tab** → **Add users** → Select `user-1` → Click **Add users**.

2. **Add `user-2` to `EC2-Support`**:
   - Repeat the same process for the `EC2-Support` group and add `user-2`.

3. **Add `user-3` to `EC2-Admin`**:
   - Repeat the process for the `EC2-Admin` group and add `user-3`.

4. **Verify Group Memberships**:
   - Navigate back to **User groups**. Ensure each group shows **1** in the **Users column** to confirm membership.

---

### **Task 3: Sign in and Test Users**
You will now test the permissions of each user to confirm that the correct policies are applied.

#### **Get the IAM Console Sign-In URL**:
1. Go to **Dashboard** in IAM and copy the **Sign-in URL for IAM users**.
2. Open a private/incognito browser window and use the link to sign in.

#### **Test `user-1` Permissions**:
1. Sign in as `user-1` with the credentials:
   - IAM user name: `user-1`
   - Password: `Lab-Password1`
2. Go to **Services** → **S3**:
   - Confirm you can view bucket contents (read-only access).
3. Go to **Services** → **EC2**:
   - Verify that you cannot view EC2 instances (no permissions for EC2).

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
3. Confirm that the lab is terminated.

---

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

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
- [x] Use the IAM credential report to perform audits.  
- [x] Use the IAM Access Analyzer to help fine-grain the IAM users' permissions.  
- [ ] Provide the IAM user with a limited set of permissions and increase as needed.  
- [ ] Provide the IAM user with a broad set of permissions and scale back as needed.  
- [ ] Create a single IAM user and provide the login credentials to users with the same job functions.  

**Explanation:**  
The **IAM credential report** provides details on users and their access patterns. **IAM Access Analyzer** helps identify overly permissive policies and refine them.

---

