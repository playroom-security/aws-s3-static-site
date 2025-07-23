## How to deploy your static web site on AWS using s3 bucket

### Requisites
- You need to have an AWS account. Click here to get your [AWS free tier account](https://signin.aws.amazon.com/signup?request_type=register) for up to six (6) months.

- No coding experience
- No previous IT knowledge

### 📢 Step 1
- Sign in to your AWS Account
(Make sure you are not using the root account user for this exercise).

If you are new to AWS, I'll suggest you read this AWS documentation for more. Click [here](https://docs.aws.amazon.com/accounts/latest/reference/getting-started-step4.html)


- On the Search bar on the top of the AWS Console page, search for ``s3`` and click on the S3 bucket on the ``Services`` panel.
You might not have any s3 bucket create, if you do, that is even better. 

- You will be automatically directed to the ``General purpose buckets`` section. Click on ``Create bucket``.

- The name of your s3 bucket has to be globally unique (No two AWS accounts should have the same s3 bucket name). I name mine ``dcyberguy.local``.
It is advisable when creating a static website to name your bucket is this format, ``<<bucket>>-<<name>>.<<someRandomStuff>>``

- Under ``Block Public Access settings for this bucket``. Uncheck the ``Block all public access`` and acknowledge at the bottom. This would make you s3 bucket access to the entire public (😧scary, right). We do have a s3 bucket that wwould only restrict the public to just "Read Access"

- Leave ``Default encryption`` as default. We would need some kind of encryption.

- Than finally, click ``Create bucket``

### 🔊 Step 2

- Once the s3 bucket has been fully provisioned. Click on the newly created bucket name

- Under the newly created bucket. You should options like``Object``, ``Metadata``, ``Properties``, ``Permissions`` and so on. Click on ``Properties``.

- Under ``Properties``, scroll all the way down till you get to ``Static website hosting``. Click on ``Edit`` to the far right and ``Enable`` Static website hosting. 

- Don't forget to ``Save changes``.


### 📯 Step 3

- Go back to the ``Object`` Options at the top of your newly created s3 bucket. It's time to upload our ``html`` files. Fun times 🎶🎶🎶

- On this Github repo under the [](/sample-html-files/) you will have an ``index.html`` and ``error.html`` files. Save them to your local machine.

- Back to your s3 bucket, Under the ``Object`` option, on the far right, click ``Upload``. Also to the far right of the Upload page, click ``Add files``. Located the ``Index.html`` files and upload it, then do the same with the ``error.html`` file. 
Remember to click ``Upload`` on the bottom of the page when you finish.

- We are not done yet, last lap 🏃‍♂️

### 🔔 Step 4

- Back at your newly created s3 bucket, Go to option ``Permissions`` at the top of the s3 bucket.

- Under ``Bucket policy``, click the ``edit`` button to the right and paste this below ``json`` file. It is also attached as part of this repo.

Mine would be something like this. Change the ``dcyberguy.local`` s3 bucket name to your s3 bucket name.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::dcyberguy.local/*" // Change this to your s3 ARN name
        }
    ]
}
```
This policy allows anyone to only view the files (like your index.html, images, CSS, etc.) but not upload, delete, or list them.

The ``Effect`` is ``Allow``
The ``Principal`` is ``*``, that means basically everyone
The ``Action`` is ``s3:GetObject`` means only being to Read (GET)
The ``Resource`` is your S3 bucket

Go to your browser and goto ``YOUR-S3-BUCKET-NAME``. Your Static website is LIVE 🔥


