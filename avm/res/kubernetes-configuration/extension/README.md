# Kubernetes Configuration Extensions `[Microsoft.KubernetesConfiguration/extensions]`

> ⚠️THIS MODULE IS CURRENTLY ORPHANED.⚠️
> 
> - Only security and bug fixes are being handled by the AVM core team at present.
> - If interested in becoming the module owner of this orphaned module (must be Microsoft FTE), please look for the related "orphaned module" GitHub issue [here](https://aka.ms/AVM/OrphanedModules)!

This module deploys a Kubernetes Configuration Extension.

## Navigation

- [Resource Types](#Resource-Types)
- [Usage examples](#Usage-examples)
- [Parameters](#Parameters)
- [Outputs](#Outputs)
- [Cross-referenced modules](#Cross-referenced-modules)
- [Notes](#Notes)

## Resource Types

| Resource Type | API Version |
| :-- | :-- |
| `Microsoft.KubernetesConfiguration/extensions` | [2022-03-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.KubernetesConfiguration/2022-03-01/extensions) |
| `Microsoft.KubernetesConfiguration/fluxConfigurations` | [2022-03-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.KubernetesConfiguration/2022-03-01/fluxConfigurations) |

## Usage examples

The following section provides usage examples for the module, which were used to validate and deploy the module successfully. For a full reference, please review the module's test folder in its repository.

>**Note**: Each example lists all the required parameters first, followed by the rest - each in alphabetical order.

>**Note**: To reference the module, please use the following syntax `br/public:avm-res-kubernetesconfiguration-extension:1.0.0`.

- [Using only defaults](#example-1-using-only-defaults)
- [Using large parameter set](#example-2-using-large-parameter-set)
- [WAF-aligned](#example-3-waf-aligned)

### Example 1: _Using only defaults_

This instance deploys the module with the minimum set of required parameters.
> **Note:** The test currently implements additional non-required parameters to cater for a test-specific limitation.



<details>

<summary>via Bicep module</summary>

```bicep
module extension 'br/public:avm-res-kubernetesconfiguration-extension:1.0.0' = {
  name: '${uniqueString(deployment().name, location)}-test-kcemin'
  params: {
    // Required parameters
    clusterName: '<clusterName>'
    extensionType: 'microsoft.flux'
    name: 'kcemin001'
    // Non-required parameters
    configurationProtectedSettings: '<configurationProtectedSettings>'
    configurationSettings: '<configurationSettings>'
    fluxConfigurations: '<fluxConfigurations>'
    location: '<location>'
    releaseNamespace: 'flux-system'
    releaseTrain: 'Stable'
    targetNamespace: '<targetNamespace>'
    version: '<version>'
  }
}
```

</details>
<p>

<details>

<summary>via JSON Parameter file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "clusterName": {
      "value": "<clusterName>"
    },
    "extensionType": {
      "value": "microsoft.flux"
    },
    "name": {
      "value": "kcemin001"
    },
    // Non-required parameters
    "configurationProtectedSettings": {
      "value": "<configurationProtectedSettings>"
    },
    "configurationSettings": {
      "value": "<configurationSettings>"
    },
    "fluxConfigurations": {
      "value": "<fluxConfigurations>"
    },
    "location": {
      "value": "<location>"
    },
    "releaseNamespace": {
      "value": "flux-system"
    },
    "releaseTrain": {
      "value": "Stable"
    },
    "targetNamespace": {
      "value": "<targetNamespace>"
    },
    "version": {
      "value": "<version>"
    }
  }
}
```

</details>
<p>

### Example 2: _Using large parameter set_

This instance deploys the module with most of its features enabled.


<details>

<summary>via Bicep module</summary>

```bicep
module extension 'br/public:avm-res-kubernetesconfiguration-extension:1.0.0' = {
  name: '${uniqueString(deployment().name, location)}-test-kcemax'
  params: {
    // Required parameters
    clusterName: '<clusterName>'
    extensionType: 'microsoft.flux'
    name: 'kcemax001'
    // Non-required parameters
    configurationProtectedSettings: '<configurationProtectedSettings>'
    configurationSettings: {
      'image-automation-controller.enabled': 'false'
      'image-reflector-controller.enabled': 'false'
      'kustomize-controller.enabled': 'true'
      'notification-controller.enabled': 'false'
      'source-controller.enabled': 'true'
    }
    fluxConfigurations: [
      {
        gitRepository: {
          repositoryRef: {
            branch: 'main'
          }
          sshKnownHosts: ''
          syncIntervalInSeconds: 300
          timeoutInSeconds: 180
          url: 'https://github.com/mspnp/aks-baseline'
        }
        namespace: 'flux-system'
        suspend: false
      }
    ]
    location: '<location>'
    releaseNamespace: 'flux-system'
    releaseTrain: 'Stable'
    targetNamespace: '<targetNamespace>'
    version: '0.5.2'
  }
}
```

</details>
<p>

<details>

<summary>via JSON Parameter file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "clusterName": {
      "value": "<clusterName>"
    },
    "extensionType": {
      "value": "microsoft.flux"
    },
    "name": {
      "value": "kcemax001"
    },
    // Non-required parameters
    "configurationProtectedSettings": {
      "value": "<configurationProtectedSettings>"
    },
    "configurationSettings": {
      "value": {
        "image-automation-controller.enabled": "false",
        "image-reflector-controller.enabled": "false",
        "kustomize-controller.enabled": "true",
        "notification-controller.enabled": "false",
        "source-controller.enabled": "true"
      }
    },
    "fluxConfigurations": {
      "value": [
        {
          "gitRepository": {
            "repositoryRef": {
              "branch": "main"
            },
            "sshKnownHosts": "",
            "syncIntervalInSeconds": 300,
            "timeoutInSeconds": 180,
            "url": "https://github.com/mspnp/aks-baseline"
          },
          "namespace": "flux-system",
          "suspend": false
        }
      ]
    },
    "location": {
      "value": "<location>"
    },
    "releaseNamespace": {
      "value": "flux-system"
    },
    "releaseTrain": {
      "value": "Stable"
    },
    "targetNamespace": {
      "value": "<targetNamespace>"
    },
    "version": {
      "value": "0.5.2"
    }
  }
}
```

</details>
<p>

### Example 3: _WAF-aligned_

This instance deploys the module in alignment with the best-practices of the Azure Well-Architected Framework.


<details>

<summary>via Bicep module</summary>

```bicep
module extension 'br/public:avm-res-kubernetesconfiguration-extension:1.0.0' = {
  name: '${uniqueString(deployment().name, location)}-test-kcewaf'
  params: {
    // Required parameters
    clusterName: '<clusterName>'
    extensionType: 'microsoft.flux'
    name: 'kcewaf001'
    // Non-required parameters
    configurationProtectedSettings: '<configurationProtectedSettings>'
    configurationSettings: {
      'image-automation-controller.enabled': 'false'
      'image-reflector-controller.enabled': 'false'
      'kustomize-controller.enabled': 'true'
      'notification-controller.enabled': 'false'
      'source-controller.enabled': 'true'
    }
    fluxConfigurations: [
      {
        gitRepository: {
          repositoryRef: {
            branch: 'main'
          }
          sshKnownHosts: ''
          syncIntervalInSeconds: 300
          timeoutInSeconds: 180
          url: 'https://github.com/mspnp/aks-baseline'
        }
        namespace: 'flux-system'
        suspend: false
      }
    ]
    location: '<location>'
    releaseNamespace: 'flux-system'
    releaseTrain: 'Stable'
    targetNamespace: '<targetNamespace>'
    version: '0.5.2'
  }
}
```

</details>
<p>

<details>

<summary>via JSON Parameter file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "clusterName": {
      "value": "<clusterName>"
    },
    "extensionType": {
      "value": "microsoft.flux"
    },
    "name": {
      "value": "kcewaf001"
    },
    // Non-required parameters
    "configurationProtectedSettings": {
      "value": "<configurationProtectedSettings>"
    },
    "configurationSettings": {
      "value": {
        "image-automation-controller.enabled": "false",
        "image-reflector-controller.enabled": "false",
        "kustomize-controller.enabled": "true",
        "notification-controller.enabled": "false",
        "source-controller.enabled": "true"
      }
    },
    "fluxConfigurations": {
      "value": [
        {
          "gitRepository": {
            "repositoryRef": {
              "branch": "main"
            },
            "sshKnownHosts": "",
            "syncIntervalInSeconds": 300,
            "timeoutInSeconds": 180,
            "url": "https://github.com/mspnp/aks-baseline"
          },
          "namespace": "flux-system",
          "suspend": false
        }
      ]
    },
    "location": {
      "value": "<location>"
    },
    "releaseNamespace": {
      "value": "flux-system"
    },
    "releaseTrain": {
      "value": "Stable"
    },
    "targetNamespace": {
      "value": "<targetNamespace>"
    },
    "version": {
      "value": "0.5.2"
    }
  }
}
```

</details>
<p>


## Parameters

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`clusterName`](#parameter-clustername) | string | The name of the AKS cluster that should be configured. |
| [`extensionType`](#parameter-extensiontype) | string | Type of the extension, of which this resource is an instance of. It must be one of the Extension Types registered with Microsoft.KubernetesConfiguration by the extension publisher. |
| [`name`](#parameter-name) | string | The name of the Flux Configuration. |

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`configurationProtectedSettings`](#parameter-configurationprotectedsettings) | secureObject | Configuration settings that are sensitive, as name-value pairs for configuring this extension. |
| [`configurationSettings`](#parameter-configurationsettings) | object | Configuration settings, as name-value pairs for configuring this extension. |
| [`enableTelemetry`](#parameter-enabletelemetry) | bool | Enable/Disable usage telemetry for module. |
| [`fluxConfigurations`](#parameter-fluxconfigurations) | array | A list of flux configuraitons. |
| [`location`](#parameter-location) | string | Location for all resources. |
| [`releaseNamespace`](#parameter-releasenamespace) | string | Namespace where the extension Release must be placed, for a Cluster scoped extension. If this namespace does not exist, it will be created. |
| [`releaseTrain`](#parameter-releasetrain) | string | ReleaseTrain this extension participates in for auto-upgrade (e.g. Stable, Preview, etc.) - only if autoUpgradeMinorVersion is "true". |
| [`targetNamespace`](#parameter-targetnamespace) | string | Namespace where the extension will be created for an Namespace scoped extension. If this namespace does not exist, it will be created. |
| [`version`](#parameter-version) | string | Version of the extension for this extension, if it is "pinned" to a specific version. |

### Parameter: `clusterName`

The name of the AKS cluster that should be configured.
- Required: Yes
- Type: string

### Parameter: `configurationProtectedSettings`

Configuration settings that are sensitive, as name-value pairs for configuring this extension.
- Required: No
- Type: secureObject

### Parameter: `configurationSettings`

Configuration settings, as name-value pairs for configuring this extension.
- Required: No
- Type: object

### Parameter: `enableTelemetry`

Enable/Disable usage telemetry for module.
- Required: No
- Type: bool
- Default: `True`

### Parameter: `extensionType`

Type of the extension, of which this resource is an instance of. It must be one of the Extension Types registered with Microsoft.KubernetesConfiguration by the extension publisher.
- Required: Yes
- Type: string

### Parameter: `fluxConfigurations`

A list of flux configuraitons.
- Required: No
- Type: array

### Parameter: `location`

Location for all resources.
- Required: No
- Type: string
- Default: `[resourceGroup().location]`

### Parameter: `name`

The name of the Flux Configuration.
- Required: Yes
- Type: string

### Parameter: `releaseNamespace`

Namespace where the extension Release must be placed, for a Cluster scoped extension. If this namespace does not exist, it will be created.
- Required: No
- Type: string

### Parameter: `releaseTrain`

ReleaseTrain this extension participates in for auto-upgrade (e.g. Stable, Preview, etc.) - only if autoUpgradeMinorVersion is "true".
- Required: No
- Type: string

### Parameter: `targetNamespace`

Namespace where the extension will be created for an Namespace scoped extension. If this namespace does not exist, it will be created.
- Required: No
- Type: string

### Parameter: `version`

Version of the extension for this extension, if it is "pinned" to a specific version.
- Required: No
- Type: string


## Outputs

| Output | Type | Description |
| :-- | :-- | :-- |
| `name` | string | The name of the extension. |
| `resourceGroupName` | string | The name of the resource group the extension was deployed into. |
| `resourceId` | string | The resource ID of the extension. |

## Cross-referenced modules

This section gives you an overview of all local-referenced module files (i.e., other CARML modules that are referenced in this module) and all remote-referenced files (i.e., Bicep modules that are referenced from a Bicep Registry or Template Specs).

| Reference | Type |
| :-- | :-- |
| `br/public:avm-res-kubernetesconfiguration-fluxconfiguration:0.1.1` | Remote reference |

## Notes

To use this module, it is required to register the AKS-ExtensionManager feature in your subscription. To do so, you can use the following command:

```powershell
az feature register --namespace Microsoft.ContainerService --name AKS-ExtensionManager
```

Further it is required to register the following Azure service providers. (It's OK to re-register an existing provider.)

```powershell
az provider register --namespace Microsoft.Kubernetes
az provider register --namespace Microsoft.ContainerService
az provider register --namespace Microsoft.KubernetesConfiguration
```

For more details see [Prerequisites](https://learn.microsoft.com/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2)
