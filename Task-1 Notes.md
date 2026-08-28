## Task 1: AWS Fundamentals, Account Setup & IAM

### Set up/access AWS account
- Create AWS Free Tier Account
- SignIn to AWS Management Console using root user email
- Explore AWS Console

### Create budget alerts
- Go to Account Section in the Console
- Go to Preferences and Setting, 
    1. Edit alert preferences and turn on AWS Free Tier alerts to your email and CloudWatch billing alerts.
    2. Edit Invoice delivery preferences and activate PDF invoices delivery by email 
- Go to Budgets and Planning -> Budget Section, 
    1. Create budget depending on your preference to alert your email when you have spent more than your budget.

### Create IAM user/group
- Search for IAM on Console for Identify and Access Management.
- Create IAM User Group in Group section with specific AWS services permission policies. 
- Create User in IAM User Section. Can add user into a group so that they have same permissions and policies under the group.
- If you create user without a group, they have limited access to AWS services. 

### Create Roles
- Search for IAM on Console, Go to Roles Section
- Can create roles with permission to specific AWS services 
- Users with limited access can switch roles temporaily to access other services and switch back to their accounts after they are done.
- Can allow IAM users to temporarly swich roles by changing user's permission policies
- To change user's permission policies:
    1. Go to specific user that can switch roles.
    2. Add permissions under permissions policies
    3. Create an inline policy
    4. Change policy editor to JSON 
    5. Use code in stsAssumeRole.json for the policy editior
    5. Change Resource data to ARN value of role created earlier

### Configure MFA
-  Search for IAM on Console, Go to IAM Users Section -> Security credentials
- Assign MFA device 
- Can use Authenticator app as MFA device - Scan QR code shown on authenticator appp