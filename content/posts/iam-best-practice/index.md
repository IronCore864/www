---
title: "AWS IAM Security Best Practices"
author: "Tiexin Guo | 郭铁心"
authorLink: https://www.guotiexin.com
tags: ["security", "devsecops", "aws", "iam", "identity management", "access management", "cloud computing", "cloud"]
categories: ["Security", "DevSecOps", "AWS", "IAM", "Cloud"]
date: 2022-06-10

cover:
  image: "featured.jpg"
  alt: "iam"
---

*This blog is originally published on [GitGuardian blog](https://blog.gitguardian.com/aws-iam-security-best-practices/).*

*Disclaimer: while this blogpost refers to AWS services in particular, the best practices are mostly the same for any other IAM framework*

"Security is job zero."

When it comes to security in AWS, this is the de facto culture and standard.

It means, it's even more important than any number one priority. At AWS, new services will not launch if there are any known security issues open.

As AWS users, while we agree that the cloud is already the new norm, it is different from running security on-premise. We don't want to reinvent the wheel when it comes to cloud security operations (10 rules for securing the cloud)

So, in this article, let's go through a few top rules and best practices in AWS IAM, and let's do it the Amazon way.

---

## 1 A Quick Recap of AWS IAM

This section gives a brief overview of AWS IAM and some of its terminologies.

If you are already very familiar with AWS IAM, feel free to jump to the next section. If you are a beginner with AWS and IAM, reading [the official doc](https://aws.amazon.com/iam/) and playing with it in a sandbox environment are suggested.

### 1.1 What is IAM

AWS Identity and Access Management (IAM) provides fine-grained access control across all of AWS. With IAM, you can specify who can access which services and resources, and under which conditions.

It provides two essential functions that work together:

- **Authentication** (Authn): it validates the **identity** of a user. It's typically handled by checking credentials, such as usernames and passwords. Advanced Authn might include multifactor authentication (MFA), which couples traditional credentials with a third form of authentication, such as sending a unique code to a user's smartphone.
- **Authorization** (Authz): not every user will have **access** to every application, data set, or service across the organization. Once a user is authenticated, authorization defines the permissions for that user and limits access to only the resources permitted for that specific user.

### 1.2 IAM Identities: Users, Groups, Roles

IAM deals with a few types of different principle entities: root user, users, user groups, roles, etc.

These entities detail who a user is and what that user is allowed to do within the environment.

![Overview of access management: Permissions and policies - AWS Identity and  Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/images/iam-intro-users-and-groups.diagram.png)

-top: root user
-bottom: users
-groups

- Root user. When you first create an Amazon Web Services (AWS) account, you begin with a single sign-in identity that has complete access to all AWS services and resources in the account. This identity is called the AWS account root user and is accessed by signing in with the email address and password that you used to create the account.
- Users. An IAM user is an entity that you create in AWS. The IAM user represents the person or service who uses the IAM user to interact with AWS. A primary use for IAM users is to give people the ability to sign in to the AWS Management Console for interactive tasks and to make programmatic requests to AWS services using the API or CLI. An IAM user has **permanent long-term credentials** and is used to directly interact with AWS services.
- (User) Groups. An IAM user group is a collection of IAM users. You can use user groups to specify permissions for a collection of users, which can make those permissions easier to manage for those users.
- Roles. An IAM role is very similar to a user, in that it is an identity with permission policies that determine what the identity can and cannot do in AWS. However, **a role does not have any long-term credentials** (password or access keys) associated with it. Instead, when you assume a role, it provides you with temporary security credentials for your role session. A role isn't associated with one person, it is intended to be assumable by anyone or **any service** that needs it ( IAM users, applications, or an AWS service such as EC2).

![AWS IAM Primer. The 20% of IAM that you need 80% of the… | by George Lutz |  Trimble MAPS Engineering Blog | Medium](https://miro.medium.com/max/768/1*EWcTG4Dh_ERmv8I2clO59w.png)

### 1.3 IAM Policies

- You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources.
- A policy is an object in AWS that, when associated with an identity or resource, defines their permissions.
- Permissions in the policies determine whether the request is allowed or denied.
- Most policies are stored in AWS as JSON documents.

---

## 2 Security Principles

Before jumping to the best practices of how to use IAM, let's take a quick look at two famous security principles. Understanding these two principles is crucial because these are the foundation upon which all the other rules are built.

### 2.1 Zero Trust

Zero Trust means what the name suggests: you trust absolutely nobody, even if it's an internal user. Starting from there, then you build your security mechanism.

A Zero Trust security model relies on these core principles:

- never trust, always verify (even if it's an internal service accessing another internal service, verification is required)
- assume breach (assuming the access is a security breach and build access permissions from there)
- least privileged access (restrict access and permissions as much as possible, without interfering with users' daily workflows)

By adopting a Zero Trust model, we can reduce the risk of unintentionally allowing access to unauthorized users. IAM and a Zero Trust strategy work well together because Zero Trust ensures your IAM policies and procedures are followed whenever and wherever a user needs access.

Zero Trust's foundational rule is least privileged access.

### 2.2 Least Privilege Access

This is probably one of the most common security-related best practices.

The least privilege restricts access and permissions as much as possible, without interfering with users' normal usage.

We achieve this by defining the minimum amount of privilege users in each role need to perform their work. And, the goal is to regularly audit usage, reduce unnecessary standing permissions wherever possible.

When we create IAM policies, follow the standard security advice of granting the least privilege or granting only the permissions required to perform a task. Determine what users (and roles) need to do and then craft policies that allow them to perform only those tasks.

We can always start with the minimum set of permissions and grant additional permissions as necessary. Try, fail, try again, add more, then make it perfect. Doing so is more secure than starting with permissions that are too wide and then trying to tighten them later.

With the zero trust and least privilege principles in mind, let's get started with IAM.

---

## 3 Reducing Your IAM Operational Overhead

Let me get it straight: IAM is complicated.

It's not easy to understand, and it's certainly not easy to use. Especially so if you are in a big team with many users, groups, resources, and even AWS accounts to manage. So, first things first: let's talk about some top rules to reduce your operational overhead.

### 3.1 Centralized IAM

If you are managing more than one "environment" (like dev/test/production environments,) it's highly likely that you use a separate AWS account for each environment to achieve maximum resource and permission separation.

But defining users and roles, and policies multiple times in each account brings extra unnecessary operational overhead. Plus, it would be troublesome for users to sign out of one account and sign in to another to access resources in a different environment.

So, we can delegate access to resources in different AWS accounts. The idea is to share resources in one account with users in a different account. This is achieved by creating a role in one account and granting users from another account to assume that specific role. If you would like to know more details about it, see the [official document here](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html) and [this blog post here](https://aws.amazon.com/blogs/security/how-to-centralize-and-automate-iam-policy-creation-in-sandbox-development-and-test-environments/).

If you manage multiple AWS accounts, this would be an easy way to manage the identities and access.  Centralizing IAM allows all functionalities and configurations to reside in one central AWS account. A centralized security system will render better visibility to all the different security configurations.

### 3.2 DevSecOps - Automate Everything

Trust me, you don't want to log in to the AWS web console, go to IAM, and click some buttons to manage IAM users/groups/roles. The only cases I can think of where this could be a good idea are:

- the first time when you use a new account, 
- and when you want to experiment with some unfamiliar features.

But let me stop you right here. Other than these two scenarios, **managing your IAM resources manually, via the console, is not recommended at all.**

Why automation? Of course, automation reduces manual labor. But it's not just that.

- Automation is also for reducing human errors. We are humans, and humans make mistakes. That's what makes us humans, not robots.
- Automation makes it easy to log, audit, and generate reports on a regular schedule for compliance requirements.

If you want to get started automating your IAM stuff, [Terraform](https://www.terraform.io/) and the [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) are good places to start.

---

## 4 Basic Setup

### 4.1 DO NOT Use Root User

A company might create a single AWS account with root credentials and then establish many different users and roles with other credentials. The root account should always be the most protected and secure entity within an AWS environment.

To make programmatic requests to AWS, you need an access key (access key ID +  secret access key). **NEVER use your AWS account root user access key.** The access key for your AWS account root user gives _full_ access to all your resources for all AWS services. You ***cannot*** reduce the permissions associated with your AWS account root user access key.

Therefore, protect your root user access key like you would your credit card numbers or any other sensitive secret. Here are some ways to do that:

- Do not use the root user for your everyday tasks, even the administrative ones. Instead, use your root user credentials only to create your IAM admin user. Then securely lock away the root user credentials. For everyday tasks, do not even use your IAM admin user. Instead, use roles to delegate permissions.
- Delete the root user's access key. If you must keep it (which you don't have to) rotate (change) the access key regularly.

### 4.2 Enable Multi-Factor Authentication (MFA)

IAM supports multifactor authentication, which requires an additional credential based on a physical item that the user possesses.

For extra security, it's strongly recommended that you enable MFA for all users in your AWS account. With MFA enabled, if a user's password or access keys are compromised, your account resources are still secure because of the additional authentication requirement.

### 4.3 Use a Strong Password Policy

If you allow users to change their own passwords, create a custom password policy that requires them to create strong passwords and rotate their passwords periodically.

IAM allows IAM admins to implement a custom password policy that can force stronger passwords and require regular password changes. Stronger passwords are more difficult to crack through systematic attempts and enhanced cloud security.

### 4.4 Use IAM roles instead of long-term access keys
Access keys provide programmatic, long-term (they never expire) access to AWS. If it's leaked, it's the same as leaking your AWS account password. 
For most apps that need access to AWS, the best practice is to configure the program to retrieve **temporary** security credentials using an IAM role. 

With that in mind, do not put access keys within unencrypted code. For example, if you use your access key in your continuous integration system, do not use them as clear text. Instead, use them as "secrets." For example, in [Jenkins, you can create credentials](https://blog.gitguardian.com/how-to-setup-jenkins-with-gitguardian-kubernetes/) or in [GitHub Actions](https://blog.gitguardian.com/github-actions-security-cheat-sheet/), you can also create repo secrets.

Also, do not share these security credentials between users. To allow your users individual programmatic access, create an IAM user with personal access keys.

### 4.5 Rotate Credentials Regularly

If you never change your password and if the password or access key is compromised without you even knowing it, that credential can be used forever.

If we apply a custom password policy to your account to require all your IAM users to rotate their AWS Management Console passwords and choose how often passwords must be rotated (for example, every 90 days), we limit how long the credentials can be used to access our resources. And if the credential is compromised without us even knowing it, we know for sure that the credential is only valid for 90 days, tops.

So change your own passwords and access keys regularly, and make sure that all IAM users in your account do as well. This reduces the risks drastically.

### 4.6 Remove Outdated and Unnecessary Credentials

For example, if you created an IAM user for an application that does not use the console at all, the IAM user does not need a password.

Similarly, if a user only uses the console, remove their access keys.

Also, locate and remove IAM passwords and keys that are idle to increase security. You can find unused passwords or access keys using the console, using the CLI or API, or by downloading the credentials report.

--- 

## 5 Groups

In the real world, you have different teams, and each team requires different permissions and should be allowed to access only certain resources.

Of course, we can create each user and assign each user their permissions, but it is always easier to create groups and assign permissions to them than to define permissions for individual users. Think of user groups in AWS IAM as logical sets of users. This way, we can create multiple groups related to various job functions (Administrator, Security Auditor, etc.) and assign relevant permissions to each group before tagging users to those groups.

We can easily manage access levels for teams by creating Groups in IAM. Users in one group will have similar access levels. AWS recommends managing user access by creating groups that assign permission to the group. This makes managing user access levels easy and streamlined. In the future, if you need to change access levels for the team then you only need to make a change at the group level.

Using groups is not only easier but also more secure and manageable. For example, whenever there are inter-departmental moves, one simply needs to place the individual in another group rather than redefining the whole set of permissions.

---

## 6 Roles

### 6.1 Use Roles to Delegate Permissions

_You should not put keys into code or instances._

When writing code, it's easier to store keys in the code itself (or in the environment,) but it has potential vulnerabilities. Even if the keys are encrypted, there is a possibility that hackers can extract those keys. **The recommended practice is to use IAM roles and generated temporary security credentials.**

You can assume an IAM role by using AWS Security Token Service (STS) operations or switch to a role in the AWS Management Console to receive a temporary role session. This is more secure than using your long-term password or access keys. A session has a limited duration, which reduces your risk if your credentials are compromised.

For IAM users, **create separate roles for specific job tasks** and assume those roles for those tasks. Don't use your IAM admin user for your everyday work.

### 6.2 Use Roles for Apps on EC2 Instances

Apps that run on AWS EC2 instances need credentials to access other AWS services. For example, if you have an app running on an EC2 instance and the app needs to write to an S3 bucket. 

You could, of course, create an IAM user with access keys and then distribute these credentials to the instances, enabling the applications on those instances to sign requests _privately_.

But the problem is **distribution**: to securely distribute credentials to each instance, especially those that AWS creates on your behalf (e.g. Spot Instances or instances in Auto Scaling groups), you must also be able to update the credentials on each instance when you **rotate** your AWS credentials.

In brief, to grant access to apps more securely, use IAM roles.

Reminder: a role is an entity that has its own set of permissions, but that isn't a user or user group. Roles also don't have their own permanent set of credentials the way IAM users do. In the case of Amazon EC2, **IAM dynamically provides temporary credentials to the EC2 instance**, and these credentials are automatically rotated for you.

Details: Amazon EC2 uses an instance profile as a container for an IAM role. When you create an IAM role using the IAM console, the console creates an instance profile automatically and gives it the same name as the role to which it corresponds. If you use the Amazon EC2 console to launch an instance with an IAM role or to attach an IAM role to an instance, you choose the role based on a list of instance profile names. In this way, apps that run on the EC2 instance can use the role's credentials when they access AWS resources.

---

## 7 Policies

### 7.1 AWS Managed Policies

If you are new to the AWS world and struggle to create and maintain your own policies for different users and groups and roles, consider using AWS predefined, out-of-the-box managed policies whenever possible.

**AWS-managed policies** cover common use cases and are well-aligned to common IT functions. No matter if you are a network guy who needs to set up and configure stuff in AWS, or a data scientist trying to run some Hadoop queries, the chance is, that there already is an AWS-managed policy for you, for just that job.

Using AWS-managed policies reduces your operational overhead. Besides, there is another major benefit: auto-update. These policies are updated whenever a new AWS service or API is introduced. This saves a lot of time and really is a quality-of-life improvement. For example, AWS manages a policy called 'ReadOnlyAccess' which provides read access to all AWS services and resources. Let’s say a new service is launched by AWS. AWS will make sure that the 'ReadOnlyAccess' policy is updated with this newly launched service. Also, this change will be applied to all the entities (group, user, or role) wherever the ReadOnlyAccess policy is already attached.

Warning! Keep in mind that AWS-managed policies don't grant the least privilege permissions. You must consider the security risk of granting your principals more permissions than they need to do their job.

### 7.2 Customer Managed Policies over Inline Policies (for Most Cases)

Although AWS-managed policies are a good place to get started, it doesn't follow the least privilege principle.

Using policies with the least privilege principle is recommended. The most secure way to do so is to write a **custom policy** with only the permissions needed by your team. However, you must create a process to allow your team **to request more permissions** when necessary: you are therefore in charge of managing your policy, that's why we talk about _customer_ managed policies. It will takes time and expertise to create such policies that provide your team with only the permissions they need.

In most cases, customer-managed policies are preferred over inline policies (an inline policy is _embedded_ in a user, group or role). Managed policies provide the following features:

- reusability between users, groups, roles
- central change management (any change is automatically propagated),
- versioning and rolling back (any change can be easily rolled back), and 
- delegating permissions management (allow users in your AWS account to attach and detach policies while maintaining control over the permissions they embark). 

**If you are in doubt between managed and inline policy, choose the managed policy.**

Only prefer inline policies if you want to maintain a strict one-to-one relationship between a policy and the identity to which it is applied. For example, you want to be sure that the permissions in a policy are not inadvertently assigned to an identity other than the one they're intended for. When you use an inline policy, the permissions in the policy cannot be inadvertently attached to the wrong identity. In addition, when you use the AWS Management Console to delete that identity, the policies embedded in the identity are deleted as well. That's because they are part of the principal entity.

### 7.3 Extra Security: Policy Conditions

Context is important in security. You can leverage it by defining the conditions under which your IAM policies allow access to a resource.

For example, you can write conditions to specify a range of IP addresses that a request must come from. For another example, you can require that a user has authenticated with an MFA device in order to be allowed to terminate an Amazon EC2 instance.

**But be careful to do not overdo it so that it becomes impractical.**

### 7.4 Policy Validation

Validate the policies that you create. 

You can validate the **syntax** (JSON) and the **logic**. The first is automatic and any modern text editor can do it. 
The second is a bit more involved: you can make good use of the **IAM Access Analyzer** to check your policies and get recommendations to write safer ones. It generates security warnings when a statement in your policy allows access we consider overly permissive.

### 7.5 Generate a Policy Based on Access Activity

This is a smart one: you have no idea who uses what, but want to enforce least privilege? Easy! Generate IAM policies based on the access activity logged by AWS CloudTrail!

When given a IAM entity (user or role), IAM Access Analyzer can review your AWS CloudTrail logs and generates a policy template that contains the permissions that have been used by this entity in your specified time frame. 
This template can be used to create a managed policy with fine-grained permissions. Just attach it to the IAM entity, et voilà!

This makes it much easier to tighten permissions to just what is necessary for en entity to interact with AWS resources in a specific use case.


### 7.6 Use Access Levels to Review IAM Permissions

You should regularly review and monitor each of your IAM policies to improve the security of your AWS account. Make sure that your policies grant the least privilege that is needed to perform only the necessary actions.

You can view the policy summary that includes a summary of the access level for each service within that policy. AWS categorizes each service action into one of five access levels based on what each action does: List, Read, Write, Permissions management, or Tagging. You can use these access levels to determine which actions to include in your policies.

---

## 8 Just-In-Time Access Management

A true least privilege security model not only requires users, apps, and systems to have just enough rights and access but also grants access for **no longer than required**.

Eliminating persistent privileged access for privileged user accounts, and activating it only for the duration it is needed to perform an activity, is by far the most overlooked component in least privilege implementations.

This is what we call **just-in-time access management**.

For example, using the [HashiCorp Vault](https://www.vaultproject.io/) [AWS Engine](https://www.vaultproject.io/docs/secrets/aws) can generate AWS access credentials dynamically based on IAM policies.

This generally makes working with AWS IAM easier, since it does not involve clicking in the web UI at all. Additionally, the IAM credentials are time-based and are automatically revoked when the Vault lease expires.

For example, Vault will create an IAM user for each lease, and attach the managed and inline IAM policies as specified in the role to the user. And Vault will delete the IAM user upon reaching the TTL expiration.

In this way, we can achieve JIT access management with AWS IAM.

---

## 9 Monitoring and Auditing

Business and applications change over time. Creating users, groups, roles, and policies and automating them is only a starting point. From there, we also need to review and update security-related settings and policies regularly.

### 9.1 Schedule Access Audits

Even with strong policies around access control, **over-provisioning** remains a problem for many organizations. Auditing is one of the fundamental IAM best practices to build into your overall IAM strategy and maintain the principle of least privilege.

Organizations are constantly adding new tools and applications to their tech stack and employees may believe they need access to all these tools to perform their work. However, as teams streamline their workflows, IT usually finds orphaned accounts that employees aren’t using. By auditing usage logs and access permissions regularly, IT teams can de-provision access and reduce their attack surface. 

Limiting access is part of IAM security best practices, **but the only way to consistently track what access users really need is through regular audits.** Create an auditing schedule in your IAM strategy to make sure your team prioritizes this important security procedure.

### 9.2 Last Accessed Information

Policies and permissions should be reviewed regularly, especially when people leave or change.

Another IAM feature that can help review access and adhere to the least privilege is last accessed information. This information is available on the Access Advisor tab on the IAM console details page for an IAM user, group, role, or policy.

Last accessed information includes information about the actions that were last accessed for some services, such as Amazon EC2, IAM, Lambda, and Amazon S3. You can use this information to identify unnecessary permissions so that you can refine your IAM or Organizations policies and remove unused policies to better adhere to the principle of least privilege.

### 9.3 Monitor Activities

You can use logging features in AWS to determine the actions users have taken in your account and the resources that were used. The log files show the time and date of actions, the source IP for an action, which actions failed due to inadequate permissions, and more.

Many AWS services support logging; they can log user requests with details.

If you want to log API calls and related events made by AWS accounts, you can also use AWS [CloudTrail](https://aws.amazon.com/cloudtrail/), which monitors and records account activity across your AWS infrastructure, giving you control over storage, analysis, and remediation actions.

To further reduce permissions, you can view your account's events in AWS CloudTrail Event history. CloudTrail event logs include detailed event information that you can use to reduce the policy's permissions. The logs include only the actions and resources that your IAM entities need.

### 9.4 Other AWS Services That Can Help

**AWS Config**

AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources.

It provides detailed historical information about the configuration of your AWS resources, including your IAM users, user groups, roles, and policies. For example, you can use AWS Config to determine the permissions that belonged to a user or user group at a specific time.

**AWS GuardDuty**

AWS GuardDuty is a threat detection service that continuously monitors AWS accounts and workloads for malicious activity and delivers detailed security findings for visibility and remediation. 

For example, if you are located in the EU and one day your account is logged in in Africa (personal true story,) GuardDuty can find it out and alert you.

---

## Summary

With all due respect to AWS, IAM really is a pain. It's not easy to learn or understand all the concepts, and it's definitely not easy to use it perfectly in an automated manner. If you are also interested in managing your IAM users, roles and policies automatically to reduce your operational overhead, be sure to subscribe, because, in the next article, we will do a hands-on tutorial on managing AWS IAM with HashiCorp Terraform. See you in the next article!
