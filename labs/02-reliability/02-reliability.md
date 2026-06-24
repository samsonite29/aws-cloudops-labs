# Placement Groups

Goal of place groups - To achieve a more optimized communication, performance, or fault tolerance for EC2s.

## Placement Group Strategies

### 1. Cluster placement group

Cluster placement group is a strategy that ensures network performance - speed, responsiveness and low latency.

All instances are packed together inside an AZ

![IAM baseline](../../diagrams/pg-cluster.svg)

1. What I want — network performance: low latency, high throughput, fast node-to-node communication
2. What I get less of — low fault isolation: instances are packed into one AZ and close together, so when something fails it takes out more of them at once than a spread layout would. Fewer instances affected = more isolation. More instances affected = less isolation.
3. How I contain what I lose : multiple cluster groups across different AZs (low latency within each, fault isolation across them
<!-- 


performance tradeoff that sacrifices availability, Trades fault isolation for network performance, low latency
Partition Reliability & Fault Tolerance Primitive
Spread Reliability & Fault Tolerance Primitive -->
