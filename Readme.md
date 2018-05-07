## Overview

SpotCluster enables developers to run highly availability services on low cost "spot" instances. Key features include:

1. **80% savings**: SpotCluster makes efficient use of spot instances to drive costs down. On average, users enjoy savings of 81.3% compared with standard (on demand) VM groups.

2. **99.999% availability**: On average, stateless SpotCluster workloads running on at least 3 nodes enjoy 99.999+% uptime.

1. **Instance Diversification**: SpotCluster achieves high availability by carefully balancing workloads across a variety of instance types and availability zones. This reduces the probability that multiple instances in a cluster will be terminated at the same time.

2. **Proactive Replacements**: SpotCluster uses historical and real-time data to select instances with a high life expectancy, and to predict when instances are likely to be terminated. If SpotCluster anticipates a termination, it begins the replacement process early, providing ample time for terminating instances to drain, and replacement instances to become healthy. This helps to ensure high availability.

3. **On-Demand Fallback** SpotCluster falls back to reserved / on-demand instances if suitable spot instances are unavailable.

4. **Stateful Migrations**: When SpotCluster replaces a stateful instance, it migrates network identity (e.g. IP address) and network volumes from the terminating instance to its replacement. As a result, the instance appears to have simply rebooted, even though it has actually migrated to new hardware. This means that SpotCluster works seamlessly with most stateful workloads (e.g. MySQL, MongoDB, Redis, etc).

5. **Price Watch**: SpotCluster monitors spot pricing, and proactively replaces expensive instances with cheaper alternatives where possible.

6. **Workload Awareness**: Instances can help SpotCluster make sound decisions by providing information about themselves via the SpotCluster API. For example, if an instance indicates that it performs a critical or ‘master’ type role, it is less likely to be proactively replaced. Likewise, if an instance is subject to a proactive replacement, it can use the SpotCluster API request extra time.

7. **Plugins**: SpotCluster Plugins enable popular stacks to use the SpotCluster API well. For example, the SpotCluster plugin for Kubernetes helps Kubernetes allocate containers based on instance type (spot or persistent), and allows Kubernetes to fully drain an instance that will soon be replaced.

8. **Compatibility**: SpotCluster is compatible with existing structures like AWS AutoScaling Groups, and can be managed using Terraform or CloudFormation.

9. **Configurability**: SpotCluster can be configured to optimize for cost or availability (via the *economy ratio*), and can be configured to maintain a proportion of instances on persistent (i.e. On Demand or Reserved) hardware.

10. **Multi Cloud**: SpotCluster works with AWS, Azure, and Google Cloud, with support for Alibaba coming soon.

For more information and FAQs, see the project wiki.

## Status
SpotCluster is currently used internally at Oikos, and a few related startups. We are preparing it for open-source release, and anticipate the code will be available here in Q3 2018.

In the meantime, please join our mailing list to receive project updates.
