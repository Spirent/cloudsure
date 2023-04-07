# Testcase Overview
A testcase is set of actions that a user wants to perform on one or more targets while measuring the resulting impact. 

 Each testcase consists of following sections, and each section contains one or more mandatory attributes (and possibly some optional attributes). 

1. [Information](#information)
2. [Environment](#environment)
3. [Scenarios](#scenarios)
4. [Observability](#observability)
5. [Analytics](#analytics)

> Note: Every testcase requires all of the these sections, except analytics which is optional. 

### Information
This section provides basic information about each testcase, and includes the following attributes:

- **Name:** A short meaningful name to make a test case easy to find.
- **Description (optional):** A more verbose statement about the testcase.
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
  
