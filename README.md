# cdk-time-bomb
Implode your AWS CDK Stack after set amount of time, save money, be happy!

## Usage

In your Typescipt / Javascript AWS CDK project, add the `cdk-time-bomb` module:

```bash
npm install cdk-time-bomb
```

Import the module and instantiate in your CDK Stack class.  Specify a TTL Duration after which time the entire CloudFormation stack will self destroy:


```javascript
import { SelfDestruct} from 'cdk-time-bomb';
const selfDestruct = new SelfDestruct(this, "selfDestructor", {
timeToLive: Duration.minutes(60)
});
```