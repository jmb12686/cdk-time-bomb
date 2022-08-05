# cdk-implode

[![npm version](https://badge.fury.io/js/cdk-implode.svg)](https://badge.fury.io/js/cdk-implode)
[![PyPI Version](https://badge.fury.io/py/cdk-implode.svg)](https://badge.fury.io/py/cdk-implode)
![Nuget](https://img.shields.io/nuget/v/cdk-implode)

Implode your AWS CDK Stack after set amount of time, save money, be happy!

## Usage

### JavaScript / TypeScript

In your Typescipt / Javascript AWS CDK project, add the `cdk-implode` module:

```bash
npm install cdk-implode
```

Import the module and instantiate in your CDK Stack class.  Specify a TTL Duration after which time the entire CloudFormation stack will self destroy:


```javascript
import { SelfDestruct} from 'cdk-implode';
const selfDestruct = new SelfDestruct(this, "selfDestructor", {
  timeToLive: Duration.minutes(60)
});
```

Be sure to add an ordering dependency on a high level base Construct in your stack.  For example anchoring `SelfDestruct` to the `Vpc` ensures all resources in the stack will be destroyed prior to destroying itself.

```javascript
const vpc = new ec2.Vpc(this, "VPC", {
});

vpc.node.addDependency(selfDestruct);
```

### Python

Install using pip

```bash
pip install cdk-implode
```

### Java

Follow the [guide for configuring maven for use with Github Packages](https://docs.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-apache-maven-for-use-with-github-packages).  Then add the following to your project's `pom.xml`

```xml
<dependency>
  <groupId>olich538.cdk</groupId>
  <artifactId>timebomb</artifactId>
  <version>1.50.0</version>
</dependency>
```

## How to build this construct

Due to the large amount of dependencies required by jsii, use the docker image `udondan/jsii-publish` to reliably and consistenly build this CDK construct.  

```bash
docker run -it \
    --workdir /workdir \
    --volume $(pwd):/workdir \
    --env VERSION=0.3.0 \
    --env BUILD_SOURCE=true \
    --env BUILD_PACKAGES=true \
    --env NPM_TOKEN \
    --env PYPI_TOKEN \
    --env NUGET_TOKEN \
    --env GITHUB_TOKEN \
    --env GITHUB_REPOSITORY="${OWNER}/${REPOSITORY}" \
    udondan/jsii-publish:0.8.3
```
