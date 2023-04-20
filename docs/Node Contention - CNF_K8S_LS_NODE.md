## Testcase Overview

This Testcase can selectively deplete the CPU, Memory, and IO resources of the Kubernetes node. The Testcase validates the resilience of applications whose replicas may be evicted due to nodes becoming unschedulable (Not Ready) because of a lack of resources.

This testcase can optionally be run with Landslide load generation.

### Testcase Components

For this Testcase, here we define the mandatory and optional components for the test at a high level.

***Mandatory***

These components of the test are mandatory in order to run the test.

- *CloudSure Agent* \- A synthetic load generation engine required to be deployed on nodes being affected for the test. Here we always and only deploy 1 CloudSure Agent for each node under test. Make sure the appropriate resources are given to fill resources.

> Note: In this test case, CloudSure does not deploy the Platform pod for communication with the agents and back to the CloudSure UI Controller. Instead, each CloudSure agent deployed during test execution will need a LoadBalancer IP to communicate to the CloudSure UI Controller.

***Optional***

These components of the test are optional and depending on the purpose of the test you may or not be needed.

- *Landslide* \- A scalable platform for testing and simulating 5G and O-RAN mobile networks based on legacy or cloud-native infrastructure is called Landslide. Millions of mobile customers generate real-world control and data plane traffic as they travel throughout the network.
- *Metrics Collection* \- CloudSure can collect cAdvisor metrics which gives users knowledge of the resource usage and performance attributes of their active containers.

## Testcase Configuration Sections Covered

1.  Environment
2.  Landslide
3.  Resiliency

## 1\. Environment

This section defines where a testcase will be executed. This is typically a Kubernetes namespace, cluster, etc, and includes all the attributes needed to provide access to the Kubernetes API.

This testcase requires additional deployment information to enable CloudSure Agent to perform the impairments. This information is also defined in this section.

#### Cloud Configuration Profile

- **Environment Name:**
    Name of Environment
    
- **Description:**
    Optional description of Cloud Configuration Profile
    
- **Auth Type:** CERT\_AUTH\_DATA/USERNAME\_AUTH\_DATA/TOKEN\_AUTH\_DATA/KUBECONF\_AUTH\_DATA
    Users need to select of the options and configure the parameters to access the Kubernetes API
    
- **Deployment Specification(s)**
    For the Node Contention Testcase users need to define a deployment specification for the test to deploy the CloudSure Agents at runtime. Here is where we define the details for the CloudSure Agent. Users need to 'Add Deployment Specification' and select 'Basic' Template. Mandatory fields are indicated by a * icon next to the filed. Those are describe below and everything else are for more advanced deployments.
    
    > Note: The 'Advanced' template can not be used for this test.
    
    - **Name:**
        Name prefix to use when deploying Pods. Location will be appended to name as well as an integer index.
        
    - **Container Type** Single option, CLOUDSURE_AGENTC
        Container type of Pod being deployed.
        
    - **Container Image Name**
        Name of the container image that will be deployed in Pod. Container must already exist on host or be available via repo.
        `registry.spirentaion.com/cloudsure-agent:23.01.4034`
        
    - **Compute (vCPUs)**
        Number of vCPUs to deploy the container Pod with. Cannot exceed or equal Node CPU count, must be less.
        
    - **Memory (MB)**
        Amount of memory in MB to deploy the container Pod with. Cannot exceed or equal Node Memory, must be less.
        
    - **Storage (GB)**
        Amount of storage in GB to deploy the container Pod with. Cannot exceed or equal Node Storage, must be less.
        
    - **Create Volume** Toggle: ON/OFF
        Enable to create persistent volumes for disks otherwise will use container storage.
        
        - **Storage (GB)**
            Size of persistent volume in GB to create when create_volume is true.
            
        - **Storage Class**
            Storage class to use when create_volume is true. To use the default storage class, this can be left blank.
            
        - **Ports**
            Ports used and needed by the CloudSure Agent to communicate back to the CloudSure UI Controller.
            
            > Note: Defaults are fine and pre-configured. Change as necessary.
            
    - **Arguments**
        List of arguments to pass to the container.
        
    - **Commands**
        List of commands to pass to the container.
        
    - **Readiness Probe Commands**
        List of commands to run to verify the readiness of the container.
        
- **Timeouts (seconds):**
    
    - **Compute Allocate**
        The maximum time in seconds to wait for allocation of virtualized compute resources to complete.
    - **Compute Operate**
        The maximum time in seconds to wait for an operation command on instantiated virtualized compute resources to complete.
    - **Compute Terminate**
        The maximum time in seconds to wait for de-allocation and termination of one or more instantiated virtualized compute resources to complete.

#### Agent Instance Configuration

The Node Contention testcase does not utilize the Spirent framework mentioned in other resiliency testcases. This testcase instead deploys the CloudSure Agent to perform the impairments. CloudSure only deploys one agent per node at test execution time and agent resource usage can't exceed the pod specs defined in the environment variables.

> Note: In this test case, CloudSure does not deploy the Platform pod for communication with the agents and back to the CloudSure UI Controller. Instead, each CloudSure agent deployed during test execution will need a LoadBalancer IP to communicate to the CloudSure UI Controller.

- **Instance Pod File**
    This provides details on how the CloudSure Agent pod will be deployed into the cluster. There are two options: DEFAULT/Data File. For Data File users need to upload a yaml file defining how the CloudSure Agent should be deployed. *Selecting DEFAULT will use the default Pod file and works in most cases.*
- **Instance Service File**
    This provides details on how the CloudSure Agent service will be defined into the cluster. There are two options: DEFAULT/Data File. For Data File users need to upload a yaml file defining how the CloudSure Agent service should be configured. *Selecting DEFAULT will use the default service file and works in most cases.*
- **Instance PVC File**
    This provides details on how the CloudSure Agent PVC will be defined into the cluster. There are two options: DEFAULT/Data File. For Data File users need to upload a yaml file defining how the CloudSure Agent PVC should be configured. *Selecting DEFAULT will use the default PVC file and works in most cases.*

#### Deployment Behavior

- **Enable Asynchronous Operations** Toggle: ON/OFF
    When enabled, instances will be deployed/destroyed asynchronously.
- **Enable Cleanup of Deployed Resources** Toggle: ON/OFF
    When enabled, infrastructure resources created by test are deleted upon test completion.

## 2\. Landslide

- **Landslide Test Session** Toggle: ON/OFF
    Configuration used to enables or disables the use of Landslide load generation. If ON, users need to configure the * fields to complete communication to Landslide API and to configure the Test Session.
    
- **Landslide Configuration**
    
    - **Landslide Manager Server IP**
        IP address/hostname of the Landslide Manager.
        
    - **Landslide Manager Port Number**
        Port number to use to connect to the Landslide manager.
        
    - **Landslide Manager User Name**
        Username to login to the Landslide Manager. This needs to be a user who can execute Landslide Test Sessions and also has access to the test session needing to run.
        
    - **Landslide Manager Password**
        Password to login to the Landslide Manager
        
    - **Fetch Only Favorite Measurements** Toggle: ON/OFF
        Landslide Live Results collects only favorite measurements, if enabled.
        
        > Note: Landslide TAS will still hold all of the results even if this is enabled.
        
    - **Landslide Test Report Type** Options OVERRIDE\_TO\_SUMMARY\_ONLY/OVERRIDE\_TO\_ALL/NO\_OVERRIDE
        Specifies how to configure report options to enable writing of CSV reports of a particular type to the database. When set to OVERRIDE\_TO\_SUMMARY\_ONLY or OVERRIDE\_TO\_ALL, the test session config will be modified. If the NO\_OVERRIDE option is selected, whatever is configured in the test session will be used.
        
- **Test Session Override Configuration File**
    Users can upload a Test Session configuration file to override Landslide test parameters. Users must use caution when overriding parameters as many Landslide parameters are read-only and the test might error at test runtime.
    

> Note: The Landslide REST API documentation lists the parameters that can be updated or, alternatively, are read-only.

### Test Session Override Configuration

- **Test Session Override Configuration Variables**
    For advanced test configuration, users can create variables in the 'Test Session Override Configuration File' and change those variables in this section.

> Note: For the dynamic variable's "name" to take effect, it must be listed as "name" in the test session override configuration file. Dynamic variables are ignored if they are defined but don't have a matching variable in the overriding configuration file. If they don't apply, Landslide may also disregard some of the parameters in the override configuration file (for example, if duration is set in a test session that has automation controls).

The dynamic variable has a couple of parameters as follows and can input as many as necessary:

- - **Dynamic Variable Type** Toggle: Integer/String
        \- **Name**
        Dynamic Variable name used in 'Test Session Override Configuration File'
        \- **Value**
        Value for the dynamic variable being changed.

## 3\. Resiliency

In this section we'll describe the available impairment parameters to fill out for the Node Contention testcase.

### Target Parameters

Node Contention can be applied to specific nodes through a variety of different node selection methods, next the user can specify the radius of the impairment.

#### Node Selection Method

- **Node Name List**
    Users can add a list of nodes they want to impair on the cluster. Specify the name of the node on the cluster. Click 'Add Item' to insert more objects.

> For the below Target sections, users can specify a target input object for the node they would like to apply resource contentions to. For example, if users want to only affect a pod from a specific deployment type they'd use deployment name target. CloudSure will only look at that deployment where the pods are placed and only add resource contention to the nodes the pods are residing on. The same applies for the other target methods.

- **Pod Name List**
    Users can add a list of pods they want to impair on the cluster. Specify the name of the pod on the cluster. Click 'Add Item' to insert more objects.
- **Pod Labels**
    Users can add a list of pods they want to impair on the cluster by specifying the label of the pod. This is a comma separated field to insert multiple labels.
- **Deployment Name**
    Users can add a deployment name they want to impair on the cluster. Specify the name of the deployment on the cluster.
- **Stateful Set Name**
    Users can add a stateful set name they want to impair on the cluster. Specify the name of the stateful set on the cluster. Single object only.
- **Pod Name Regex**
    Users can add a regex for the pod name to identify pod input objects they want to impair on the cluster.
- **Pod Label Regex**
    Users can add a regex for the pod labels to identify pod input objects they want to impair on the cluster.

#### Selection Method

- **Selection Count**
    Users can select the integer count they would like the radius of impact. For example, if users have 2 nodes on your Node Selection Method, users can put 1 or 2 on the Selection Count. If only a subset of the nodes are targeted then the node targets are selected randomly.

> Note: If Selection Count is used, it must not exceed the total number of objects returned by the Node Selection Method. For example, if the Selection Count is 3 and there are only 2 nodes as a result of Node Selection, you will receive an error. If you want to impair all nodes that result from Node Selection, set Selection Percent to 100%.

- **Selection Count**
    Users can specify a percentage of object nodes to target. The number of selected objects are rounded up. If only a subset of the nodes are targeted then the node targets are selected randomly.

#### Impairment Parameters

- **Impairment Delay**
    A one-time delay in seconds between starting the Landslide test and starting the impairment.
    
- **Impairment Duration**
    The duration in seconds that the impairment runs for.
    
- **CPU Impairment Parameters**
    The CPU resources on the Kubernetes node are depleted as a result of this Test. The test tries to validate the robustness of applications whose replicas may be evicted due to nodes becoming unschedulable (Not Ready) due to a lack of CPU resources.
    
    - **Node CPU HOG Impairment**: ON/OFF
    - **Node CPU Core**: Number of CPU Cores to consume per node
    - **PU Load %**: Fixed CPU load to generate as a percent for a single core
- **Memory Impairment Parameters**
    The Memory resources on the Kubernetes node are depleted as a result of this test. The test tries to validate the robustness of applications whose replicas may be evicted due to nodes becoming unschedulable (Not Ready) due to a lack of Memory resources.
    
    - **Node Memory Hog Impairment**: ON/OFF
    - **Read Threads**: Number of the read threads to perform read operations. Zero value disables read operations.
    - **Write Threads**: Number of the write threads to perform write operations. Zero value disables write operations.
    - **Read/Write Threads**: Read/write mode that the impairment will use. Choices are READ/WRITE/READWRITE
    - **Buffer Size**: Size of the memory buffer in bytes. Buffer is used to perform read/write operations. The size must be a multiple of the block size.
    - **Access Pattern**: Access pattern that will be used during memory hog impairment. Choices are RANDOM/SEQUENTIAL/REVERSE
    - **Block Size**: Size of the block in bytes. Block is a small unit to perform one read/write operation
- **Block IO Impairment Parameters**
    This test puts the Kubernetes node under io stress. The test's goal is to test the resiliency of programs that share this disk resource for ephemeral     or persistent storage. It evaluates application robustness in the face of replica evictions induced by IO load on available disk space.
    
    - **Node Block IO Hog Impairment Enabled**: ON/OFF
        Node Block IO Hog Impairment
    - **Read/write mode**: READ/WRITE/READWRITE
        Read/write mode that the impairment will use
    - **Access Pattern**: RANDOM/SEQUENTIAL/REVERSE
        Access pattern that will be used during Block IO hog impairment.
    - **Queue Depth**
        Queue depth that the impairment will use. In storage, queue depth refers to the number of pending input/output (I/O) requests that a storage resource can handle at any given time. Performance-demanding applications can generate enough storage I/Os to fill hundreds of queues. If the number of I/O requests exceeds the storage device's supported queue depth, a failure message is sent to the connecting host. The I/O must then be resent by the host operating system (OS).
    - **File Size (bytes)**
        File size in bytes that the impairment will use.
    - **Block Size**
        Size of the block in bytes. Block is a small unit to perform one read/write operation.
    - **Path**
        Storage fill target path

#### Node Metrics Collection

> To be completed
