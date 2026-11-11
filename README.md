# Encrypt Data with AWS KMS

**Project Link:** [View Project](https://nextwork.ai/projects/716e7f81-84d1-51d6-8945-d4860caebf77)

**Author:** Anthony Marizu

---

## Introducing Today's Project!

In this project, I will demonstrate using encryption to secure data.  The goal is to create encryption keys with AWS KMS (Key Management System), encrypt a DynamoDB Table using that key then test access using IAM Users.

### ✍️ What are we doing in this step?

In this step, I will use AWS KMS(Key Management Service) to create an encryption key and make ourselves the administrator/user of that key

### Tools and concepts

Services I used include AWS KMS(Key management service), DynamoDB, AWS IAM. Key concepts I learnt include encryption, database tables, KMS using permission to actions rather than just access to the key itself, creating a user to test access, difference between layers of security for data access like Security groups (IAM), permission polices (IAM) encryption keys(KMS).

### Project reflection

This project took me approximately 35 minutes. It was most rewarding to see our test user regain access,

I chose to do this project today because I wanted to showcase the brilliance of AWS so that interested individuals can have an clear guide to basic AWS concepts. This project showed us about encyption, securing our data and how it actually works as well as showing us the foundation of encryption keys and managing access as an Admin.

## Encryption and KMS

Encryption is the process of turning original/plain text data into a secure fomat. Companies and developers do this to secure their data from unauthorised users. Encryption keys are the secure code that informs an algorithim on how it should encrypt.

AWS KMS is a vault for our encryption keys. Key management services like KMS are important because they help us secure and manage the keys we use to encrypt data, unauthorised access to the key=exposing our encrypted data which puts our security at risk.

Encryption keys are broadly categorized as symmetric and asymmetric. I set up a symmetric key because we will be using the exact same key to encrypt and decrypt our data. Asymmetric Keys will be a good choice if we need different key to encyption or decryption

![Encryption and KMS](https://nextwork.ai/anthony-marizu/uploads/716e7f81-84d1-51d6-8945-d4860caebf77_a2b3c4d5)

### ✍️ What are we doing in this step?

In this step, I will create a DynamoDB table. This will be the resource that we secure using encryption keys.

## Encrypting Data

My encryption key will safeguard data in DynamoDB, which is a fast and flexible AWS Database service. If you will like to know more about DynamoDB, heres a little tip, DynamoDB is great for applications that need fast access to large amounts of data, an example is Gaming.

The different encryption options in DynamoDB include DynamoDB owned, AWS managed and Customer managed. Their differences are based on who creates and manages the key and wether we have visibility. We selected CMK to use our created KMS key.

### ✍️ What are we doing in this step?

In this step, We will be adding data to the DynamoDB table and testing our access to the encrypted data.

![Encrypting Data](https://nextwork.ai/anthony-marizu/uploads/716e7f81-84d1-51d6-8945-d4860caebf77_q8r9s0t1)

## Data Visibility

Rather than controlling who has access to the key, KMS manages user permissions by controlling the actions that people can do with that key. In our case, even if we gave the test user the permission to see our key, it will still need permission to decrypt.

Despite encrypting my DynamoDB table, I could still see the table's items because we are users of the key. DynamoDB uses transparent data encryption, which means it does the encryption and decryption process for us because it knows we are authorised

### ✍️ What are we doing in this step?

In this step, I will create a test user does not have the permission to encrypt or decrypt the key. This will help us validate wether our encrypted data will still show to unauthorised users

![Data Visibility](https://nextwork.ai/anthony-marizu/uploads/716e7f81-84d1-51d6-8945-d4860caebf77_c0d1e2f3)

## Denying Access

I configured a new IAM user to validate wether unauthorised users can still access encrypted data. The permission policies I granted this user are DynamoDB full access but NOT encryption or decryption access to AWS KMS.

### ✍️ What are we doing in this step?

In this step, I will try to access our encrypted data using the test IAM user because we want to validate that they wont get to see data that should still be encrypted to them.

After accessing the DynamoDB table as the test user, I encountered an access denied message because our test user has no access to decryption with the key. This confirmed that encryption keys can be used to secure data.

![Denying Access](https://nextwork.ai/anthony-marizu/uploads/716e7f81-84d1-51d6-8945-d4860caebf77_w0x1y2z3)

## EXTRA: Granting Access

To let my test user use the encryption key, I made it a key user in the KMS. My key's policy was updated to allow the test user to encrypt, decrypt, re-encrypt etc using the key.

Using the test user, I retried accessing the DynamoDD table. I observed that the user can now see the data inside, which confirmed that making it a key user is an effective way to authorise someone to see encrypted data.

Encryption secures data instead of an entire resource or service. I could combine encryption with other access control tools and permission policies to have two layers of security- the resource level and then the data level.

![EXTRA: Granting Access](https://nextwork.ai/anthony-marizu/uploads/716e7f81-84d1-51d6-8945-d4860caebf77_feffb2fb8)
