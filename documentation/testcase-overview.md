# Testcase Overview
This document describes the attributes and their relationships that make up a testcase.  Each testcase is made of the following main sections:

1. Basic Information
2. Environment
3. Scenarios/Actions
4. Monitoring/Metrics
5. Analytics (optional)

## Basic Information
These attributes are used to uniquely identify each testcase:

- Testcase Name
- Description (optional)
- ID
- Date Created/Updated
- Creator/Updator
- Tags (optional)

## Environment
These attributes are used to define where the testcase will be run, and what information will be collected as part of the testcase:
- Environment Name
- Auth Type
- etc

## Scenarios/Actions
Each testcase conists of one or more scenarios, and each scenarios contains one or more action. Scenarios (and their embeeded actions) are listed sequentionally. Aside from the first scenarios (and action), all the others will having timing aspects relative to the sequence.

Each scenario has the following attributes:
- Scenario Name
- Timing (all except first scenario)
- List of actions

Each action has the following attributes:
- Action Name
- Timing (all except first scenario)
- Settings

## Analytics