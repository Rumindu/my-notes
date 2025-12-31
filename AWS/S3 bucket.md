## Create a S3 Bucket Policy for Public Read Access

You need to add a bucket policy that allows public read access to your images. Here's the policy you should apply:

``` json 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
        }
    ]
}
```

**To apply this policy:**

1. Go to your S3 bucket in the AWS Console
2. Click on the "Permissions" tab
3. Scroll down to "Bucket policy"
4. Click "Edit" and paste the policy above
5. Replace `YOUR_BUCKET_NAME` with your actual bucket name
6. Click "Save changes"

## S3 bucket industry best parties.
- [Is your S3 bucket leaking right now?](https://www.facebook.com/reel/837806325788145)
- 