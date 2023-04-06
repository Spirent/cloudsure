# Testcase Overview
A testcase a is set of actions performed on a target enviroment while measuring the resulting impact. A testcase can also include post-processing of the results to determine an outcome (e.g. pass/fail, score, etc.).

 Each testcase consists of following sections, each containing a set of attributes. 

1. Information
2. Environment
3. Scenarios
4. Observability
5. Analytics (Optional)

> Note: All sections are required, except analytics.  If an analytics section is not included, the result of the testcase will be stored for post-analytics outside the testcase.

### Information
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

#### Actions
Each scenario action has the following attributes:
- Action Name
- Action Type: here are 
- Action Target(s):
- Action Settings
- Action Timing (all except first scenario)

### Observability

- 

### Analytics
  
