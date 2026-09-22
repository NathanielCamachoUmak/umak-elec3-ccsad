# Lab 1 Submission

## Part B
**Error Action Name:** 
Instance launch failed
You are not authorized to perform this operation. User: arn:aws:iam::548387266019:user/ccsad-g01 is not authorized to perform: **ec2:RunInstances** on resource: arn:aws:ec2:ap-southeast-1:548387266019:instance/* because no identity-based policy allows the ec2:RunInstances action.[cite: 15]

## Part C
**Policy Statement Blanks:**
- `"Action"`: "ec2:RunInstances"
- `"Resource"`: "instance"
- `"ec2:InstanceType"`: "t3.micro"

## Part D
**Security Group Error Text:** 
You are not authorized to perform this operation. User: arn:aws:iam::548387266019:user/ccsad-g01 is not authorized to perform: ec2:CreateSecurityGroup on resource: arn:aws:ec2:ap-southeast-1:548387266019:security-group/* because no identity-based policy allows the ec2:CreateSecurityGroup action.[cite: 15]

**Running Instance Time:** 20:30 UTC+8

## Part E
**t3.small / Tokyo Denial Error:** 
Instance launch failed
You are not authorized to perform this operation. User: arn:aws:iam::548387266019:user/ccsad-g01 is not authorized to perform: ec2:RunInstances on resource: arn:aws:ec2:ap-southeast-1:548387266019:instance/* with an explicit deny in a permissions boundary: arn:aws:iam::548387266019:policy/umak-lab-boundary.[cite: 15]

The AMI ID (ami-06380d26ad7176f2c) is not valid. The AMI might no longer exist or may be specific to another account or Region.[cite: 15]
No VPCs found, either this account doesn’t have any VPCs in this region or an invalid search has been entered. Please refine the search query, create a new VPC or create a new default VPC[cite: 15]

**CloudTrail errorMessage:**
User: arn:aws:iam::548387266019:user/ccsad-g01 is not authorized to perform: ec2:RunInstances on resource: arn:aws:ec2:ap-southeast-1:548387266019:instance/* with an explicit deny in a permissions boundary: arn:aws:iam::548387266019:policy/umak-lab-boundary.[cite: 15]

## Part F Questions
1. Which action did the Part B error name?
   It named the action `ec2:RunInstances`.
2. In your policy, which condition limits `ec2:RunInstances`?
   The condition that limits it is `"ec2:InstanceType": "t3.micro"`.
3. After you attached `ec2:*` on `*`, why was `t3.small` still denied? Name the boundary statement.
   It was denied because the boundary statement `DenyAnyInstanceTypeButT3Micro` acts as an absolute limit, explicitly blocking it and overriding the wide allow policy.
4. Why is `ec2:*` on `*` a poor policy even with a boundary?
   It violates the principle of least privilege. If the account is compromised, an attacker has full control to modify or delete anything permitted within the boundary, rather than only having access to the specific resources needed for the job.
5. In two sentences: what does the boundary control that your policy cannot?
   The boundary establishes the maximum possible permissions, such as restricting actions to specific regions or instance sizes, enforced by an administrator. Your user policy can only grant permissions within that strict predefined perimeter.