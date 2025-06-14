 # Azure Resource Manager Templates

```
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "Storage": {
            "type": "string",
            "metadata": {
                "description": "Storage account "
            },
            "defaultValue": "Premium",
            "allowedValues": [
                "Premium",
                "Standard"
            ]
        }
    },
    "functions": [],
    "variables": {              #### Defining reusable variables. 
        "resourceName": "storageaccount_testing"
    },
    "resources": [
        {
            "name": "[variables('resourceName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2023-05-01",
            "tags": {
                "displayName": "testing"
            },
            "location": "[resourceGroup().location]",
            "kind": "StorageV2",
            "sku": {
                "name": "Premium_LRS",
                "tier": "[parameters('Storage')]"
            }
        },  ## creating another resources
        {
            "name": "keyVault1",
            "type": "Microsoft.KeyVault/vaults",
            "apiVersion": "2023-07-01",
            "location": "[resourceGroup().location]",
            "tags": {
                "displayName": "keyVault1"
            },
            "properties": {
                "enabledForDeployment": true,
                "enabledForTemplateDeployment": true,
                "enabledForDiskEncryption": true,
                "tenantId": "tenantId",
                "accessPolicies": [
                    {
                        "tenantId": "tenantId",
                        "objectId": "objectId",
                        "permissions": {
                            "keys": [
                                "Get"
                            ],
                            "secrets": [
                                "List",
                                "Get",
                                "Set"
                            ]
                        }
                    }
                ],
                "sku": {
                    "name": "standard",
                    "family": "A"
                }
            },
            "resources": [
                {
                    "type": "secrets",
                    "name": "keyVaultSecret1",
                    "apiVersion": "2023-07-01",
                    "dependsOn": [
                        "[resourceId('Microsoft.KeyVault/vaults', 'keyVault1')]"
                    ],
                    "properties": {
                        "value": "secretValue"
                    }
                }
            ]
        } 
    

    

    ],
    "outputs": {}
}

```
* Schema  -->  validates the template (type, name, kind, loacation)
* contentVersion  --> it's like version control
* paramaters --> Instead of hardcoding the values (sku : Premium_LRS), we can set the default value and also, we can reuse the same template for other resource creation with some other values, by specifying in that template.

* Variables  ---> If is used for reuseability, for defining the values.
* outputs --> we can define that output like getting the public IP of the VM, as we do in the terraform.
* functions --->  we can create loops using functions. Eg: To create VMs with different names based on the loop condition.

## Why Bicep?
* Simplifies ARM templates with cleaner, readable syntax.
* Azure-native IaC tool by Microsoft.
* No state file needed – good for smaller or modular deployments.
* Built-in validation and IntelliSense support in VS Code.
* Ideal for pure Azure environments.
  
## Why Terraform for Azure ?
* Multi-cloud support – not limited to Azure.
* Tracks infrastructure state, enabling plan/apply workflows.
* Highly modular & reusable, great for large teams.
* Works well with CI/CD pipelines and version control.
* Ideal for complex or hybrid cloud setups.

## Why ARM templates for Azure?
* Official Azure IaC standard using JSON.
* Full resource support – always up-to-date with Azure features.
* No third-party dependencies, used in secure/governed environments.
* Supports policy compliance and RBAC.
* Ideal for enterprise or regulated environments.


| Tool          | Best For                                                                     |
| ------------- | ---------------------------------------------------------------------------- |
| **Bicep**     | Native Azure IaC with simplified syntax and strong tooling support.          |
| **Terraform** | Multi-cloud, complex deployments with state management and modularity.       |
| **ARM**       | Official JSON-based templates with full Azure feature parity and compliance. |
