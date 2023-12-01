[Return](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/README.md) | [The Tolkien Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheTolkienRing.md) | [The Elfen Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheElfenRing.md) | [The Web Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheWebRing.md) | [The Cloud Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheCloudRing.md) | [The Burning Ring of Fire](#suricata) | [Kringlecon](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/Kringlecon.md)

<h1 id="top">The Cloud Ring</h1>

#### Table of Contents
- [AWS CLI Intro](#aws)
- [Trufflehog Search](#search)
- [Exploitation via AWS CLI](#exploit)

<h3 id="aws">AWS CLI Intro</h3>

You may not know this, but AWS CLI help messages are very easy to access. First, try typing: aws help. Next, please configure the default aws cli credentials: From here I would reference __AWS website__ for steps on configuring the console. The command used would be aws configure.

No alt text provided for this image
Command: aws configure

Excellent! To finish, please get your caller identity using the aws command line. The command used would be `aws sts get-caller-identity`.

No alt text provided for this image
Command: aws sts get-caller-identity

<h3 id="search">Trufflehog Search</h3>

Use Trufflehog to find secrets in a Git Repo. Work with Jill Underpole in the Cloud Ring. What's the name of the file that has AWS Credentials? After some searching on the Gitlab websites repo I was able to find the file that had the credentials which is `put_policy.py`.

No alt text provided for this image
AWS Credentials | put_policy.py

<h3 id="exploit">Exploitation via AWS CLI</h3>

Use Trufflehog to find credentials in the Gitlab instance at __asnowball__. Configure these credentials for `us-east-1` and then run the command. The command that I used was `git clone https://haugfactory.com/asnowball/aws_scripts.git`. I was able to clone the repo with git clone and open the directory showing the files inside.

No alt text provided for this image
Commands: git clone https://haugfactory.com/asnowball/aws_scripts.git | cd aws_scripts | ls

This is the syntex on how to use Trufflehog: `trufflehog git <repo>`. Next would be using the command `trufflehog git https://haugfactory.com/asnowball/aws_scripts.git` and see what response we will get from the command. 

No alt text provided for this image
Command: trufflehog git https://haugfactory.com/asnowball/aws_scripts.git

After using Trufflehog, I ended up using the Gitlab site that was provided in order to find the commit history that was needed.

No alt text provided for this image
added commit by orc admin 

No alt text provided for this image
put_policy.py credentials need for configuring aws

After finding the commit put_policy.py I was able to get the `aws_access_key_id="AKIAAIDAYRANYAHGQOHD”` and `aws_secret_access_key="e95qToloszIgO9dNBsQMQsc5/foiPdKunPJwc1rL"`. With this information I will be able to configure the aws. With the command aws configure. From here I would input the AWS Access Key ID, AWS Secret Access Key, Default region name, and Default output format. Once that was done the next command, I will need to use is `aws sts get-caller-identity` to verify that the information was inputted correctly.

No alt text provided for this image
Command: aws configure | input informatoin | aws sts get-caller-identity

Managed (think:shared) policies can be attached to multiple users. Use the AWS CLI to find any policies attached to your user. The command that I used was `aws iam list-user-policies --user-name haug`.

No alt text provided for this image
Command: aws iam list-user-policies --user-name haug

The following command used to get the policy for the user haug with the policy named `S3Perms`. `aws iam get-user-policy --user-name haug --policy-name S3Perms`.

No alt text provided for this image
Command: aws iam get-user-policy --user-name haug --policy-name S3Perms

The next command used is to get a list of attached user policies under the name of haug. `aws iam list-attached-user-policies --user-name haug`.

No alt text provided for this image
Command: aws iam list-attached-user-policies --user-name haug

After some digging around on __AWS Command Reference__, I was able to come up with a command to spit out the policy needed. The command used was `aws iam list-attached-user-policies --user-name haug`. Now we can view the git policy that is attached to the user haug. The command that was used to get policy was `aws iam get-policy --policy-arn arn:aws:iam::602123424321:policy/TIER1_READONLY_POLICY`

No alt text provided for this image
Command: aws iam get-policy --policy-arn arn:aws:iam::602123424321:policy/TIER1_READONLY_POLICY

Attached policies can have multiple versions. View the default version of this policy. The command that I was able to come with the get the version of the policy from the prior information I was able to use this command. `aws iam get-policy-version --policy-arn arn:aws:iam::602123424321:policy/TIER1_READONLY_POLICY --version-id v1 | less`

No alt text provided for this image
Command: aws iam get-policy-version --policy-arn arn:aws:aim::602123424321:policy/TIER1_READONLY_POLICY --version-id v1 | less | page 1

No alt text provided for this image
Command: aws iam get-policy-version --policy-arn arn:aws:aim::602123424321:policy/TIER1_READONLY_POLICY --version-id v1 | less | page 2

The inline user policy name S3Perms disclosed the name of an S3 bucket that you have permissions to list objects. List those objects! The command used in order to get the bucket attached to S3Perms is `aws s3api list-object --bucket smogmachines3 | less`.

No alt text provided for this image
Command: aws s3api list-object --bucket smogmachines3 | less.| page 1

No alt text provided for this image
Command: aws s3api list-object --bucket smogmachines3 | less.| page 2

No alt text provided for this image
Command: aws s3api list-object --bucket smogmachines3 | less.| page 3

The attached user policy provided you several Lambda privileges. Use the AWS CLI to list Lambda functions. In order to do that I would need to use the command `aws lambda list-functions | less`.

No alt text provided for this image
Command: aws lambda list-functions | less | page 1

No alt text provided for this image
Command: aws lambda list-functions | less | page 2

Use the AWS CLI to get the configuration containing the public URL of the Lambda function. I was able to come up with a command in order to get the public URL within the function it-self using `aws lambda get-function-url-config --function-name smogmachine_lambda`.

No alt text provided for this image
Command: aws lambda get-function-url-config --function-name smogmachine_lambda

The public URL that was found is `https://rxgnav37qmvqxtakes1w5vwwjm0suhwc.lambda-url.us-east-1.on.aws/`

[Top](#top)
