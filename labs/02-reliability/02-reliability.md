# Placement Groups

Goal of place groups - To achieve a more optimized communication, performance, or fault tolerance for EC2s.

Given that I have 12 EC2 instances

## Placement Group Strategies

### 1. Cluster Placement Group

Cluster placement group is a strategy that requires all instances to be packed together inside an AZ zone which ensures network performance - speed, responsiveness and low latency.

![Cluster Placement Group](../../diagrams/pg-cluster.svg)

1. What I gain — network performance: low latency, high throughput, fast node-to-node communication
2. What I would give away  — low fault isolation: instances are packed into one AZ and close together, so when something fails it takes out more of them at once than a spread layout would. Fewer instances affected = more isolation. More instances affected = less isolation.
3. How I contain what I give away : multiple cluster groups across different AZs (low latency within each, fault isolation across them.

When to use -  I want all my 12 ec2 instances close together, so communication is fast

### 2. Spread Placement Group

Spread placement group is another strategy that requires instances to be spread across multiple hardware and those hardware running in different AZs..

![Spread Placement Group](../../diagrams/pg-spread.svg)

1. What I gain - High availability, Reduced correlated and simultaneous failures, independent scalability
2. What I would give away - low latency, high throughput

When to use -  I want my 12 ec2 on a separate independent servers for more protections.

### 3. Partition Placement Group

Partition placement group is strategy that places ec2 instances in partitions. Partition here means logical group of EC2 instances. Each partition has its own set of physical servers and racks and do not share machines with other machines.

![Partition Placement Group](../../diagrams/pg-partition.svg)

When to use -  I want my 12 ec2 on a different partitions for more protections.

1. What I gain - High availability, Reduced correlated and simultaneous failures, independent scalability
2. What I would give away - low latency, high throughput


Note

1. Trade offs for spread and partition placement groups are quite similar but the difference is the level of protection. Spread placement group protect single instances while partition protects group of instances.