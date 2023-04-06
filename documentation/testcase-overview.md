# Testcase Overview
A testcase is set of actions performed on a target enviroment while the resulting impact is being measured. Optionally a testcase can also post-processing of the results to determine an outcome.

 Each testcase consists of following sections. Each section will have a set of attributes. 

1. Basic Information
2. Environment
3. Scenarios/Actions
4. Monitoring/Metrics
5. Analytics (optional)

### Basic Information
These attributes are used to uniquely identify each testcase:

- Testcase Name
- Description (optional)
- ID
- Date Created/Updated
- Creator/Updator
- Tags (optional)

## Environment
These attributes are used to define where the testcase will be run:
- Environment Name
- Auth Type
- etc
- etc
- etc

## Scenarios/Actions
Each testcase conists of one or more scenarios, and each scenarios contains one or more action. Scenarios (and their embeeded actions) are listed sequentionally. Aside from the first scenarios (and action), all the others will having timing aspects relative to the sequence.

Each scenario has the following attributes:
- Scenario Name
- Scenario Timing (all except first scenario)
- List of actionst

Each action has the following attributes:
- Action Name
- Action Target(s): this the Kubernetes object that the action will affect.
- Action Settings
- Action Timing (all except first scenario)

## Analytics
  
