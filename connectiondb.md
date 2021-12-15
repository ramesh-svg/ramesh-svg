{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "serverName": {
      "type": "string",
      "defaultValue": "[uniqueString('sql', resourceGroup().id)]",
      "metadata": {
        "description": "qmignewdmg"
      }
    },
    "sqlDBName": {
      "type": "string",
      "defaultValue": "SampleDB",
      "metadata": {
        "description": "Postgres" 
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "EastUS"  
      }
    },
    "administratorLogin": {
      "type": "string",
      "metadata": {
        "description": "qmigdmg" 
      }
    },
    "administratorLoginPassword": {
      "type": "securestring",
      "metadata": {
        "description": "qmignewdmg"  qmignewdmg
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Sql/servers",
      "apiVersion": "2020-02-02-preview",
      "name": "[parameters('serverName')]",
      "location": "[parameters('location')]",
      "properties": {
        "administratorLogin": "[parameters('administratorLogin')]",
        "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
      },
      "resources": [
        {
          "type": "databases",
          "apiVersion": "2020-08-01-preview",
          "name": "[parameters('sqlDBName')]",
          "location": "[parameters('location')]",
          "sku": {
            "name": "Standard",
            "tier": "Standard"
          },
          "dependsOn": [
            "[resourceId('Microsoft.Sql/servers', concat(parameters('serverName')))]"
          ]
        }
      ]
    }
  ]
}
