# cfn-modules: ElastiCache Serverless

ElastiCache Serverless with secure firewall configuration, [encryption](https://www.npmjs.com/package/@cfn-modules/kms-key), backup enabled, and [alerting](https://www.npmjs.com/package/@cfn-modules/alerting).

## Install

> Install [Node.js and npm](https://nodejs.org/) first!

```
npm i @cfn-modules/elasticache-serverless
```

## Usage

```
---
AWSTemplateFormatVersion: '2010-09-09'
Description: 'cfn-modules example'
Resources:
  Cache:
    Type: 'AWS::CloudFormation::Stack'
    Properties:
      Parameters:
        VpcModule: !GetAtt 'Vpc.Outputs.StackName' # required
        ClientSgModule: !GetAtt 'ClientSg.Outputs.StackName' # required
        AlertingModule: '' # optional
        BastionModule: '' # optional
        KmsKeyModule: '' # optional
        CacheName: 'demo' # required
        SnapshotRetentionLimit: '35' # optional
        MaxDataStorageLimit: 10 # optional
        MaxECPUPerSecondLimit: 1000 # optional
      TemplateURL: './node_modules/@cfn-modules/elasticache-serverless/module.yml'
```

## Examples

none

## Related modules

none

## Parameters

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Default</th>
      <th>Required?</th>
      <th>Allowed values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>VpcModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/vpc">vpc module</a></td>
      <td></td>
      <td>yes</td>
      <td></td>
    </tr>
    <tr>
      <td>ClientSgModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/client-sg">client-sg module</a> where traffic is allowed from on port 6379 to the cache</td>
      <td></td>
      <td>yes</td>
      <td></td>
    </tr>
    <tr>
      <td>AlertingModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/alerting">alerting module</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>BastionModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/search?q=keywords:cfn-modules:Bastion">module implementing Bastion</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>KmsKeyModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/kms-key">kms-key module</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>SnapshotRetentionLimit</td>
      <td>The number of days for which ElastiCache retains automatic snapshots before deleting them (set to 0 to disable backups)</td>
      <td>35</td>
      <td>no</td>
      <td>[0...35]</td>
    </tr>
    <tr>
      <td>MaxDataStorageLimit</td>
      <td>The maximum amount of data stored in the cache.</td>
      <td>10</td>
      <td>no</td>
      <td>[1...]</td>
    </tr>
    <tr>
      <td>MaxECPUPerSecondLimit</td>
      <td>Maximum number of ECPU per second. Must be between 1000 and 15000000. You can set the value to zero to remove the limit.</td>
      <td>1000</td>
      <td>no</td>
      <td>[1000...15000000]</td>
    </tr>
    <tr>
      <td>CacheName</td>
      <td>The unique name for the cache.</td>
      <td>no</td>
      <td>yes</td>
      <td>Max 40 characters.</td>
    </tr>
    
  </tbody>
</table>

## Limitations

* All connections to database require TLS.
* Valkey/Redis runs in cluster mode, clients/apps need to support that.