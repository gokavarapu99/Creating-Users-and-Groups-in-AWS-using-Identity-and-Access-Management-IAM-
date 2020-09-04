# Creating-Users-and-Groups-in-AWS-using-Identity-and-Access-Management-IAM-
Creating Users and Groups and attaching policies to Groups and adding users to the groups in AWS

# This Hands on lab is done using Linux academy provided credentials using Cloud Playground.
Introduction to AWS Identity and Access Management (IAM)
AWS Identity and Access Management (IAM) is a service that allows AWS customers to manage users' access and permissions to the AWS accounts and available APIs/Services within AWS. IAM can manage users, security credentials (such as API access keys), and allow users to access AWS resources. In this lab, we will be walking through the foundations of IAM. We'll focus on user and group management, and how to assign access to specific resources using IAM managed policies. We'll learn how to find the login URL where AWS users can log in to account, and explore this from a real-world use case perspective.

Solution
Log in to the live AWS environment using the credentials provided. Make sure you're in the N. Virginia (us-east-1) region throughout the lab.

Environment Walkthrough
Explore the Users
Navigate to IAM > Users.
Click user-1.
At the top, under Summary, observe the user’s ARN (Amazon Resource Name), path, and creation time.
Select the Permissions and Groups tabs, where we'll see user-1 does not have any permissions assigned to it and does not belong to any groups.
Select the Security credentials tab to see its access keys, SSH public keys, and HTTPS Git credentials for AWS CodeCommit.
Select the Access Advisor tab to see which services the user has accessed and when.
Click Users in the left-hand menu, and select user-2 and user-3 to check out their permissions, groups, security credentials, and services.
Explore the Groups
Click Groups in the left-hand menu.
There are three groups we're going to focus on:
EC2-Admin: Provides permissions to view, start, and stop EC2 instances
EC2-Support: Provides read-only access to EC2
S3-Support: Provides read-only access to S3
Click any of the groups to see which policy is attached to it.

Note: There are two different kinds of policies for these groups:

Managed policies: Policies shared among users and/or groups that are prebuilt either by AWS or an administrator within the AWS account. When it's updated, the changes to this policy are immediately applied for all users and groups to which it's attached.
Inline policies: Policies assigned to just one user or group that are typically used in one-off situations.
Click the EC2-Admin group

Click the Permissions tab, where we'll see it has a set of permissions associated with it: an inline policy.
Click Edit Policy to see the actions the group is allowed to take (and which resources the action can be taken on) or if it has read-only access. This policy displays JSON access control policy language and provides access on a granular level to AWS resources.
From this, we can see we have permission to view all of our elastic load balancers, list metrics, get metric statistics, and describe metrics (which our CloudWatch metrics automatically configured with our EC2 instance). The same permissions apply to our Auto Scaling service. All of these allow us to do it on any resource.
Click Cancel.
Click Groups in the left-hand menu.
Click the EC2-Support group.
Click the Permissions tab, where we'll see it has a managed policy.
Click Show Policy.
We'll see this group can describe EC2 instances, describe elastic load balancers, describe and list CloudWatch metrics, and describe our autoscaling configurations. What it doesn’t allow us to do is stop, start, create, or pretty much anything else. It’s essentially read-only, which means we can view what’s happening inside EC2, but we can’t do anything inside it.
Click Cancel.
Click Groups in the left-hand menu.
Click the S3-Support group.
Click the Permissions tab. In this scenario, our S3-Support group is only allowed read-only access.
Click Show Policy, where we'll see the Get and List actions, which allow us to view the objects in an S3 bucket as well as view the S3 bucket itself.
Click Cancel.
Adding Users to Groups and Testing
Add Users to Groups
Still on the S3-Support group page, click the Users tab.
Click the Add Users to Group button.
Select user-1, and click Add Users.
Click Groups in the left-hand menu.
Click EC2-Support.
In the Users tab, click Add Users to Group.
Select user-2, and click Add Users.
Click Groups in the left-hand menu.
Click EC2-Admin.
In the Users tab, click Add Users to Group.
Select user-3, and click Add Users.
Log in as user-1
Click Dashboard in the left-hand menu.
Click the double-papers icon next to the IAM users sign-in link at the top.
Open an incognito-mode browser window, and paste the link into the browser.
Log in as user-1 using the password 123456.
Navigate to S3.
Click Create bucket.
Enter a random bucket name.
Click Create bucket.
In the error message, click to expand API response. We'll see an "Access Denied" message.
Click Cancel.
Navigate to EC2 > Instances. We'll find we don’t have the authorized permissions to view any information here because this user doesn’t need these permissions for their job role.
Log out by clicking user-1 in the top right corner, and then click Sign Out.
Log in as user-2
Click the Sign In to Console button in the top right corner.
Log in as user-2 using the password 123456.
Navigate to EC2 > Instances. We should immediately notice user-2 has more permissions than user-1, as we'll be able to view the running instance.
With the running instance selected, click Actions > Instance State > Stop.
Click Yes, Stop in the dialog. We'll then receive a message saying "Error stopping instances," as this user does not have permission to stop instances.
Click Cancel.
With the running instance still selected, click Actions > Instance State > Terminate.
Click Yes, Terminate in the dialog. We'll then receive a message saying "Error terminating instances."
Click Cancel.
Navigate to S3. We'll then see an error message saying "Insufficient permissions to list buckets," as this user doesn't have the right permissions to view anything here.
Log out by clicking user-2 in the top right corner, and then click Sign Out.
Log in as user-3
Click the Sign In to Console button in the top right corner.
Log in as user-3 using the password 123456.
Navigate to EC2 > Instances.
With the running instance selected, click Actions > Instance State > Stop.
Click Yes, Stop in the dialog. This time, it will let us stop it, and we'll see the instance enter a stopping state. (It will take a few minutes for the instance to finally stop.)
Once it’s stopped, click Actions > Instance State > Start.
Click Yes, Start in the dialog. It will then show a pending status as it moves back into a running status.
Conclusion

Completed this lab in Linux academy using Linux academy Cloud Playground.
