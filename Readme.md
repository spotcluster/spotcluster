SpotCluster is a new project that helps developers reduce their cloud compute costs through efficient use of spot instances.

## Concepts

### Spot Instances
Spot instances are low cost virtual machines that are up to 90% cheaper than regular on-demand instances. Spot instances are available on AWS, Azure, Google Cloud, and Alibaba, and are identical to on-demand instances, except for one important catch: they can be interrupted (i.e. force terminated) at any time by the cloud provider. This makes it difficult to deliver highly available services, especially stateful services, using spot instances.


### SpotCluster
SpotCluster makes it easy to deploy critical services (including stateful services) on spot instances. It uses several strategies to ensure high availability:

1. It deploys workloads across a variety of instance types and availability zones. This reduces the probability that multiple instances in a cluster will be terminated at the same time.

2. It uses historical and real-time data to select instances with a high life expectancy, and to predict when instances are likely to be terminated. If it anticipates a termination, it begins the replacement process early, providing ample time for a smooth transition.

3. It falls back to reserved / on-demand instances if suitable spot instances are unavailable.

4. It migrates instance state (e.g. IP address and network volumes) across replacements if required.

5. It monitors instance pricing, and proactively replaces instances with cheaper alternatives where possible.

## Features

### Proactive Replacements
SpotCluster uses real-time and historical data to predict when spot instances are likely to be force terminated, then proactively migrates work to alternate instances up to 90 minutes in advance. This gives instances extra time to drain properly, improving reliability.

### Price Watch
SpotCluster continually monitors and ranks spot instance types based on price and life expectancy. If SpotCluster detects an opportunity to save you money without unduly increasing risk, it gradually rebalances your workload to cheaper instances.

### Stateful Support
If SpotCluster needs to replace a stateful instance (e.g. a database shard), it ensures that the replacement instance retains the network identity (IP address) and network volumes (e.g. EBS) of the original instance. As a result, the instance appears to have simply rebooted, even though it has actually migrated to new hardware. This means that SpotCluster works out-of-the-box with most stateful workloads.

### Workload Awareness and Plugins
Instances can help SpotCluster make sound decisions by providing information about themselves via the Awareness API. For example, if an instance indicates that it performs a critical or ‘master’ type role, it is less likely to be proactively replaced. Likewise, if an instance is subject to a proactive replacement, it can use the Awareness API request extra time.

Plugins enables popular software to use the Awareness API well. For example, the SpotCluster plugin for Kubernetes helps Kubernetes allocate containers based on instance type (spot or persistent), and allows Kubernetes to fully drain an instance that will soon be replaced.

## Cluster Management
Clusters can be managed in several ways, including:
* SpotCluster API
* SpotCluster Admin Console
* Terraform
* SpotCluster

For more information, see the Documentation (coming soon).

## Strategy Options
SpotCluster supports a number of strategy options that can be used to optimize your cluster. This includes:

* An **economy ratio**, which determines how frequently SpotCluster triggers lazy replacements in order to save money. A high economy ratio will result in greater cost savings, but more replacements. A low ratio will result in fewer replacements, but fewer cost savings.

* An **availability ratio**, which determines the maximum number of stateful instances that can be unavailable at any given time.

* A **minimum persistent ratio**, which determines the proportion of instances that should run on persistent (i.e. On-Demand / Reserved) instances.

## Integrations
### AWS Autoscaling Groups
SpotCluster can be  configured to work with existing Autoscaling Groups. This allows SpotCluster to quickly deliver cost savings for systems built on AutoScaling Groups (e.g. Elastic Beanstalk, AWS Container Service).

SpotCluster for ASG works by replacing built-in Lifecycle Hooks with custom ones, overriding ASG logic for launching new instances and replacing failing ones.

## Alternate Solutions
We are aware of a number of projects that seek to address the same problem, including SpotInst, Autospotting, Hollow Trees, and Pusher.
