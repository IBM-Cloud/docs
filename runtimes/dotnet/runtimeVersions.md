---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Runtime Versions
{: #runtime_vertsions}


{: shortdesc}

## Supported versions
{: #supported_versions}
This buildpack supports the following versions, those marked as deprecated will be removed in a future buildpack release.  See [Microsoft's support statement for LTS and Current releases](https://www.microsoft.com/net/core/support).

### project.json tooling (deprecated)

| .NET SDK version        | Default |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   No    |
| 1.0.0-preview2-1-003177 |   No    |

### MSBuild SDK tooling

| .NET SDK version        | Default |
|-------------------------|---------|
| 1.0.3                   |   No    |
| 1.0.4                   |   Yes   |

### .NET Core runtime versions

| .NET Core runtime version | Release type | Default |
|---------------------------|--------------|---------|
| 1.0.0 (deprecated)        | LTS          |   No    |
| 1.0.1 (deprecated)        | LTS          |   No    |
| 1.0.3 (deprecated)        | LTS          |   No    |
| 1.0.4                     | LTS          |   No    |
| 1.0.5                     | LTS          |   Yes   |
| 1.1.0 (deprecated)        | Current      |   No    |
| 1.1.1                     | Current      |   No    |
| 1.1.2                     | Current      |   No    |

## Specifying the .NET SDK version

Control the .NET SDK version with an optional global.json in the application's root directory. For example:
```
   {
      "projects": [ "src" ],
      "sdk": {
        "version": "1.0.1"
      }
   }
```
{: codeblock}

If not specified, the MSBuild tooling for the latest Long-term-support (LTS) runtime is used.  To use project.json tooling, you can specify one of the project.json versions listed above but should also keep in mind that these versions will be removed in the future.
