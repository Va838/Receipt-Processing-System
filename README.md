# 🧾 AWS Receipt Processing System using Textract

This project is a serverless application that automatically processes receipt images uploaded to an Amazon S3 bucket. It uses **Amazon Textract** to extract structured data, stores the result in **DynamoDB**, and sends email notifications using **Amazon SES**.

---

## 📌 Use Case

> A user uploads a receipt image to S3, and the system extracts data like date, total amount, vendor name, etc., then stores it and notifies the user.

---

## 🛠️ Architecture Overview

![Screenshot 2025-07-01 162202](https://github.com/user-attachments/assets/b21d3f41-9daf-4df2-a4c7-e52ce9d9f997)


### Components:

1. **Amazon S3** – Stores uploaded receipt images.
2. **AWS Lambda** – Serverless logic for orchestrating the workflow.
3. **Amazon Textract** – Extracts text and data from the receipts.
4. **Amazon DynamoDB** – Stores structured receipt data.
5. **Amazon SES** – Sends email notifications after processing.

---

## 🔁 Workflow

1. 🧑‍💼 **User uploads** the receipt image to an S3 bucket.
2. ⚡ **S3 triggers** a Lambda function upon new upload.
3. 🔍 **Lambda invokes Textract** to extract text/data from the image.
4. 📄 **Textract returns** structured JSON data back to the Lambda.
5. 🗃️ **Lambda stores** the extracted data in a DynamoDB table.
6. 📧 **Lambda uses SES** to send an email notification to the user.

---

## ⚙️ Setup Instructions

1. **Create the following AWS resources**:
   - An S3 bucket for uploads
   - A DynamoDB table (e.g., `ReceiptsTable`)
   - A verified email identity in Amazon SES
   - A Lambda function with appropriate IAM roles

2. **Configure environment variables** for the Lambda:
   ```env
   TABLE_NAME= name_of_the_table
   EMAIL_FROM=your_verified_email@example.com
   EMAIL_TO=user_email@example.com
   ```

3. **Deploy the Lambda function** and set up an S3 trigger.

---

## ✅ Example Output

Once a receipt is uploaded:
- The extracted fields (e.g., Total Amount, Vendor, Date) are stored in DynamoDB.
- An email is sent to the user with a summary.

---

## 📝 Notes

- Make sure **Amazon SES** is in **production mode** or email identities are verified.
- Textract works best with clear, high-resolution images.
- All resources should be deployed in the same region (e.g., `us-east-1`).

