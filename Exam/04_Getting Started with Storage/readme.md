# Getting Started with Storage

## ✈️ Requirements

It would be helpful for your learning if you have a basic understanding of cloud computing concepts and the AWS Management Console. AWS Educate supports this background with courses, which include the following:

1. **AWS Educate Introduction to the AWS Management Console**
2. **AWS Educate Introduction to Cloud 101**

---

<details>	
          <summary><b>about the cource & Requirements</b></summary>
<div>
🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
  
When you consider running your workloads on Amazon Web Services (AWS), you might first consider your storage options. AWS storage provides the services that you need to build the storage solution that’s right for your business. You will review the primary storage types and the differences between them. You will also learn how to identify the right solution in the cloud based on your requirements. 

You will then focus on Amazon Simple Storage Service (Amazon S3), an object storage service that offers industry-leading scalability, data availability, security, and performance.  Customers of all sizes and industries can use Amazon S3 to store and protect any amount of data for a range of use cases. These use cases include websites, mobile applications, backup and restore, archive, enterprise applications, Internet of Things (IoT) devices, and big data analytics. 

In this course, you acquire the knowledge that you need to start using Amazon S3. You learn about the key elements of Amazon S3 and explore how to configure them. You learn how to upload data to Amazon S3 and what additional AWS services you can use to transfer data to Amazon S3 at scale. You also learn the basic elements of security within Amazon S3. 

## Course Level 
This course is a foundational level course that is written for learners beginning with cloud computing and AWS services. When you start this course, you don’t need to have a deep knowledge of cloud computing. If you have more knowledge of cloud computing, you might still find this course helpful in refreshing your knowledge and practicing your skills. 

It would be helpful for your learning if you have a basic understanding of cloud computing concepts and the AWS Management Console. AWS Educate supports this background with courses, which include the following:

1. AWS Educate Introduction to the AWS Management Console
2. AWS Educate Introduction to Cloud 101

## Objectives
By the end of this course you will be able to do the following:

- Discuss different types of storage solutions and their features and benefits.
- Discuss the features and concepts of Amazon S3.
- Describe Amazon S3 storage classes and associated use cases.
- Discuss how to use Amazon S3 to create a bucket, upload objects, and work with objects.
- Describe Amazon S3 configurations for cost savings and security.
- Identify other AWS storage solutions and their use cases.
- Use Amazon S3 to create a static website.

## Course Layout
This course is self-paced, and you can take it in as many sessions as you would like. You can stop and come back at any time. The course will hold your progress. 

The course is laid out in three main sections.  

1. The first section is the content module. In this section, you will acquire knowledge and skills related to the content. You should expect to spend about 45 minutes on the content. 
2. The second section is the hands-on simulation where you will get to practice your new skills. The simulation is aligned to the content, and you should know everything that you need in order to complete the simulation. Pay special attention to the simulation directions. You should expect to spend about 45 minutes completing the simulation. 
3. The third section is the final assessment. You must pass the final assessment with a score of 70 percent or better to complete the course and earn a badge. You should expect to spend about 20 minutes completing the final assessment. 

## Getting Started Learning Pathway
This course is part of a series of courses designed to give you a solid foundation in cloud computing. Each course focuses on a specific domain of cloud computing.

Though you can take any of the courses at any time, it is suggested that you take the courses in the following order:

1. Getting Started with Storage
2. Getting Started with Compute
3. Getting Started with Networking
4. Getting Started with Databases 
5. Getting Started with Cloud Operations
6. Getting Started with Security
7. Getting Started with Serverless

## How to Get Help
If you need help when you are taking a course, you can get help from the panel on the left side of the Canvas page. The Help icon will direct you to a page that includes helpful material about courses and badges, FAQ, and a link to support requests.

🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
</div>
</details>

<details>	
          <summary><b>What to Do in the Terminal (or AWS Console)</b></summary>
<div>
🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
  
This course offers a great opportunity to build a foundational understanding of AWS storage services, particularly **Amazon S3**. Here's how you can approach the practical lab portion step by step, based on the guidelines you've shared:

---

### **What to Expect in the Lab**
1. **Create an Amazon S3 Bucket**  
   - A bucket is where you store your data in Amazon S3. You'll create one and configure its properties.

2. **Upload Objects**  
   - You'll upload files or data into the S3 bucket you create.

3. **Configure Security and Access**  
   - You'll work with permissions to secure your bucket and its contents.

4. **Set Up a Static Website (Optional)**  
   - You might turn your bucket into a static website by enabling a special configuration.

---

### **What to Do in the Terminal (or AWS Console)**
The lab instructions likely include working with the **AWS Management Console** or using **AWS CLI** (Command Line Interface). I'll guide you for both approaches. Let’s begin with CLI.

---

### **1. Create an Amazon S3 Bucket**
**Command:**
```bash
aws s3 mb s3://your-bucket-name --region your-region
```

**Explanation:**
- Replace `your-bucket-name` with a unique name (e.g., `my-first-s3-bucket`).
- Replace `your-region` with the AWS region where you want to create the bucket (e.g., `us-east-1`).

Example:
```bash
aws s3 mb s3://my-first-s3-bucket --region us-east-1
```

This creates an S3 bucket in the specified region.

---

### **2. Upload an Object**
**Command:**
```bash
aws s3 cp /path/to/your/file.txt s3://your-bucket-name/
```

**Explanation:**
- Replace `/path/to/your/file.txt` with the path to a file on your local machine.
- Replace `your-bucket-name` with your S3 bucket's name.

Example:
```bash
aws s3 cp my-file.txt s3://my-first-s3-bucket/
```

This uploads the file `my-file.txt` to your bucket.

---

### **3. List Objects in the Bucket**
**Command:**
```bash
aws s3 ls s3://your-bucket-name/
```

**Explanation:**
- This command lists all objects in the specified bucket.

Example Output:
```plaintext
2024-12-13 12:00:00       12345 my-file.txt
```

---

### **4. Secure Your Bucket**
Use **Bucket Policies** to control access. Here's an example policy that makes the bucket read-only:

**Command:**
```bash
aws s3api put-bucket-policy --bucket your-bucket-name --policy file://policy.json
```

**Explanation:**
1. Create a file named `policy.json` with the following content:
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::your-bucket-name/*"
            }
        ]
    }
    ```
2. Replace `your-bucket-name` with your bucket name.
3. Save the file and run the command above.

This makes the bucket publicly readable. For stricter security, modify the policy to allow access only to specific AWS accounts or users.

---

### **5. (Optional) Host a Static Website**
1. **Enable Static Website Hosting**
   **Command:**
   ```bash
   aws s3 website s3://your-bucket-name/ --index-document index.html --error-document error.html
   ```
   This configures your bucket to serve as a website.

2. **Upload Your Website Files**
   - Ensure you have an `index.html` file and an `error.html` file.
   - Use the `aws s3 cp` command to upload these files to your bucket.

3. **Access the Website**
   - Open the URL: `http://your-bucket-name.s3-website-your-region.amazonaws.com`.

🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
</div>
</details>

---

