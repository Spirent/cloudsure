# Testcase Overview
A testcase is set of actions performed on a target enviroment while the resulting impact is being measured. A testcase can also post-processing of the results to determine an outcome.

 Each testcase consists of following sections. Each section will have a set of attributes. 

1. Basic Information
2. Environment
3. Scenarios
4. Monitoring
5. Analytics

> Note: All sections are required, except analytics which is optionally.  If not used, the result of the testcase will be stored for post-analytics outside the testcase.

### Basic Information
Each testcase includes the following information elements:

- Testcase Name
- Description (optional)
- Unique ID
- Date Created/Updated
- Creator/Updator
- Tags (optional)

### Environment
These attributes are used to define where the testcase will be run:
- Environment Name
- Auth Type
- API Endpoint
- etc
- etc

### Scenarios
Each testcase conists one or more scenarios. If more than one scenario are required, they are in a sequentional list. Each scenario (other than the first) will include a timing aspects relative to the sequence. Each scenario includes one or more actions.

Each scenario has the following attributes:
- Scenario Name
- Scenario Timing (all except first)
- Action(s)

Each scenario action has the following attributes:
- Action Name
- Action Target(s):
- Action Settings
- Action Timing (all except first scenario)

### Monitoring

### Analytics
  
