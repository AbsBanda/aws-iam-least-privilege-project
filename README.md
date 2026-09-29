# AWS IAM Least Privilege Project

## Project Overview

This hands-on AWS project demonstrates how to implement the Principle of Least Privilege using AWS Identity and Access Management (IAM) and Amazon S3.

The objective was to create a development user who could perform only the S3 actions required for their role, while preventing unauthorized actions.

## Technologies Used

- Amazon Web Services (AWS)
- AWS Identity and Access Management (IAM)
- Amazon S3
- IAM Users
- IAM User Groups
- Custom IAM Policies
- JSON

## Project Objectives

The project involved:

- Creating a dedicated Amazon S3 development bucket.
- Creating a custom least-privilege IAM policy.
- Creating an IAM group for frontend developers.
- Creating an IAM user called `alice-dev`.
- Assigning permissions through group membership.
- Testing authorized and unauthorized actions.
- Verifying that AWS denied actions that were not explicitly permitted.

## Security Concepts Demonstrated

### Principle of Least Privilege

The IAM user was granted only the permissions required to work with objects in the designated development bucket.

### Group-Based Access Control

Permissions were assigned to the `FrontendDevelopers` IAM group rather than directly to the user. The `alice-dev` user inherited the required permissions through group membership.

### Authentication vs Authorization

The project demonstrated that successfully signing in to AWS does not automatically provide access to AWS resources. Authentication verifies the identity, while IAM policies determine what that identity is authorized to do.

### Implicit Deny

Actions that were not explicitly allowed by the custom IAM policy remained denied by AWS. This was demonstrated by attempting to create another S3 bucket.

## Implementation

The implementation and testing process is documented below with screenshots.

### Step 1 - Create the Development S3 Bucket

A dedicated S3 bucket was created for development activities.

### Step 2 - Create a Custom IAM Policy

A custom IAM policy was created to provide only the S3 permissions required by the developer.

### Step 3 - Create the FrontendDevelopers Group

An IAM user group named `FrontendDevelopers` was created and the custom policy was attached to the group.

### Step 4 - Create the Developer User

An IAM user named `alice-dev` was created with AWS Management Console access and added to the `FrontendDevelopers` group.

### Step 5 - Test Authorized Access

The `alice-dev` user signed in separately and successfully uploaded a test file to the authorized development bucket.

This confirmed that the required `s3:PutObject` permission was working.

### Step 6 - Test Unauthorized Access

The `alice-dev` user attempted to create another S3 bucket.

AWS denied the operation because `s3:CreateBucket` was not included in the custom IAM policy.

This confirmed that the Principle of Least Privilege was being enforced.

## Result

The project successfully demonstrated least-privilege access in AWS.

The developer could perform the actions required for their role while unauthorized S3 operations remained blocked.

## Key Lessons Learned

- Authentication and authorization are separate security processes.
- IAM policies should grant only the permissions required for a role.
- IAM groups make permissions easier to manage consistently.
- Actions not explicitly allowed are implicitly denied.
- Testing both successful and denied actions is important when validating IAM configurations.
