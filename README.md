# Cloud Governance Gone Rogue – Azure Policy Lab

## Summary

This lab demonstrates the use of Azure Policy and Initiatives to enforce cloud governance across an Azure environment. As part of a simulated onboarding at MapleTech Solutions, a Canadian cloud-native company, the goal was to prevent developers from:
- Deploying resources outside of `Canada Central`
- Creating Public IP addresses
- Skipping mandatory tags

To achieve this, three custom Azure Policies were authored and grouped into an Initiative named **MapleTech Secure Foundation**, which was then assigned to a resource group to enforce compliance.

---

## Policies Explained

| Policy Name               | Description                                                                 | Effect |
|---------------------------|-----------------------------------------------------------------------------|--------|
| `Only-CanadaCentral`      | Denies resource deployments to any Azure region other than Canada Central. | Deny   |
| `Require-ProjectName-Tag` | Requires the `ProjectName` tag to be present on all deployed resources.     | Deny   |
| `Deny-Public-IP`          | Prevents the creation of public IP addresses.                              | Deny   |

All policies were authored as JSON definitions and saved in the [`policy-definitions/`](./policy-definitions/) folder.

---

## Test Cases

| Test Scenario                                            | Expected Result | Outcome |
|----------------------------------------------------------|-----------------|---------|
| Deploy VM in East US                                     | ❌ Denied       | ✅ Blocked by Region and Tag policies |
| Deploy Storage Account without `ProjectName` tag         | ❌ Denied       | ✅ Blocked by Tag policy             |
| Create a Public IP resource                              | ❌ Denied       | ✅ Blocked by Public IP policy       |
| Deploy VM in Canada Central with `ProjectName` tag       | ✅ Allowed      | ✅ Successfully deployed             |

 Screenshots of all test cases are available in the [`screenshots/`](./screenshots/) folder.

---

## Challenges & Lessons Learned

### Challenges:
- Policy creation failed at first due to incorrect JSON structure in the Azure Portal.
- Parameters required by tag-based policy needed clarification on where to define them during initiative creation.

### Lessons Learned:
- Azure Policy is highly effective at enforcing compliance and security across teams.
- Initiatives simplify applying multiple related policies at once.
- Testing is essential to ensure policies behave as expected under both compliant and non-compliant scenarios.

---

## Video Demo



