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

### IAM Identity Center - Best Practice for Companies
- Allows users to access AWS using temporary credentials with limited permissions based on roles
- Require Multi-factor authentication MFA 
- Safeguard root user credentials - Not to be used for daily tasks
- Apply least permissions
- Search for IAM Identity Center in Console
- Can configure MFA here: Go to Confirm identity source -> Authentication 
- Can manage permissions for multiple accounts:
    1. Create permission set 
    2. Choose predefined or custom set
    3. Select policy for predefined permission set
- Create Group in Group Section
- Create User in User Section:
    1. Add name, email and any other user information 
    2. Can add user into a group
- To assign users/groups to account:
    1. Go to AWS Accounts -> Select the account
    2. Assign users and groups to account
    3. Allow permission sets to groups or users
    4. Users will get an email to accept invitation to account 
    5. Users can directly signup into AWS account and can access permissions set for them 