# azure-entra-id-rbac-lab
Hands-on Azure lab using Microsoft Entra ID and Azure RBAC. Created users and security groups, assigned Reader access to a resource group, and tested least-privilege permissions by verifying the user could view resources but not create or modify them.
# Microsoft Entra ID RBAC & Access Control Lab

## Project Overview

In this hands-on Azure lab, I configured Microsoft Entra ID identities and Azure Role-Based Access Control (RBAC) to practice managing user access using the principle of least privilege.

The goal of this lab was to create a test user, place that user into a security group, assign the group the Reader role at the resource group level, and verify that the user could view resources but could not create or modify them.

---

## Technologies Used

- Microsoft Azure
- Microsoft Entra ID
- Azure Role-Based Access Control (RBAC)
- Azure Resource Groups
- Security Groups
- Azure Portal

---

## Lab Environment

### Test User
- Display Name: `Test User 1`

### Security Group
- Group Name: `Cloud Support Lab Users`
- Group Type: `Security`
- Membership Type: `Assigned`

### Resource Group
- Resource Group Name: `rg-entra-lab`

### Assigned Role
- Role: `Reader`
- Scope: Resource Group

---

## Step 1: Created a Microsoft Entra ID User

I navigated to:

`Microsoft Entra ID > Users > New User`

I created a new cloud user called:

`Test User 1`

This account was used to test Azure permissions separately from my administrator account.

### Screenshot

![Entra User](screenshots/entra-user.png)

---

## Step 2: Created a Security Group

I created a Microsoft Entra ID security group named:

`Cloud Support Lab Users`

I configured the group with:

- Group Type: Security
- Membership Type: Assigned

I then added `Test User 1` as a member of the group.

### Screenshot

![Security Group](screenshots/security-group.png)

---

## Step 3: Created a Resource Group

I created a dedicated Azure resource group for the lab:

`rg-entra-lab`

This resource group was used as the scope for testing Azure RBAC permissions.

### Screenshot

![Resource Group](screenshots/resource-group.png)

---

## Step 4: Assigned the Reader Role Using Azure RBAC

Inside the resource group, I navigated to:

`Access Control (IAM) > Add Role Assignment`

I selected the:

`Reader`

role and assigned it to:

`Cloud Support Lab Users`

This allowed members of the security group to view resources inside the resource group without giving them permission to create, modify, or delete resources.

### Screenshot

![RBAC Reader Assignment](screenshots/reader-role.png)

---

## Step 5: Tested Access With the Entra User

I opened a private/incognito browser window and signed into Azure using the `Test User 1` account.

The user successfully accessed:

`rg-entra-lab`

This confirmed that the Reader permission was being inherited through the security group.

### Screenshot

![User Resource Group Access](screenshots/user-access.png)

---

## Step 6: Verified Least-Privilege Access

To verify the permission level, I attempted to create an Azure Virtual Machine while signed in as `Test User 1`.

Azure blocked the action because the user only had the Reader role.

The portal returned an authorization error indicating that the account did not have permission to perform the requested action.

This confirmed that the RBAC configuration was working correctly.

### Screenshot

![Authorization Failure](screenshots/authorization-error.png)

---

## Troubleshooting and Validation

During testing, I verified the following:

✅ Test User 1 could authenticate to Microsoft Azure.

✅ Test User 1 could view the assigned resource group.

✅ Access was granted through membership in a Microsoft Entra ID security group.

✅ The Reader role allowed viewing Azure resources.

❌ Test User 1 could not create a Virtual Machine.

❌ Test User 1 could not make changes requiring write permissions.

This demonstrated the principle of **least privilege**, where users receive only the permissions necessary to perform their job responsibilities.

---

## Skills Demonstrated

This lab demonstrates experience with:

- Microsoft Entra ID user administration
- Security group management
- Azure RBAC
- IAM permissions
- Resource-level access control
- Role assignments
- Least-privilege security
- Identity and access troubleshooting
- Testing user permissions
- Azure Portal administration

---

## Real-World Scenario

An organization has a Cloud Support team that needs visibility into Azure resources for monitoring and troubleshooting but should not be able to modify production infrastructure.

Instead of assigning permissions individually, administrators can place support employees into a Microsoft Entra ID security group and assign the Reader role to that group.

This makes access easier to manage while reducing the risk of unauthorized infrastructure changes.

---

## Key Takeaway

This lab helped me understand the relationship between:

`User → Security Group → Azure RBAC Role → Resource Scope`

Rather than assigning permissions directly to every employee, Azure administrators can use groups and RBAC to manage access efficiently and securely.
