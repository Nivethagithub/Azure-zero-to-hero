# Azure Resource Manager Templates

{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "functions": [],
    "variables": {},
    "resources": [
        {
            "name": "storageaccount_testing",
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2023-05-01",
            "tags": {
                "displayName": "testing"
            },
            "location": "[resourceGroup().location]",
            "kind": "StorageV2",
            "sku": {
                "name": "Premium_LRS",
                "tier": "Premium"
            }
        }
    ],
    "outputs": {}
}


* Schema  -->  validates the template (type, name, kind, loacation)
* contentVersion  --> it's like version control
* paramaters --> Instead of hardcoding the values (sku : Premium_LRS), we can set the default value and also, we can reuse the same template for other resource creation with some other values, by specifying in that template. 
