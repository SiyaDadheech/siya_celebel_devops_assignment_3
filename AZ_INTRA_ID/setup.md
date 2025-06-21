# to create test user in cli
> az ad user create --display-name "Test User" --user-principal-name testuser1@your-tenant-id.onmicrosoft.com --password "testpass"
# to create groups in Azure cli
> az ad group create --display-name "Test Group" --mail-nickname "testgroup"
# to assign role to user or group
> az role assignment create --assignee testuser1@<your-tenant-id>.onmicrosoft.com --role "Reader" --scope /subscriptions/subscription-id
# to create json file
> vim Customrole.json
add the following content there:
>  {
  "Name": "Custom Reader",
  "IsCustom": true,
  "Description": "Can read resource groups and VMs",
  "Actions": [
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Compute/virtualMachines/read"
  ],
  "NotActions": [],
  "AssignableScopes": [
    "/subscriptions/<subscription-id>"
  ]
}

# to create the role
> az role definition create --role-definition Customrole.json



