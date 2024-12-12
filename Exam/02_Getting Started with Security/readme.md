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
