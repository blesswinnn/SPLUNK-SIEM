# SPLUNK-SIEM

![image](https://github.com/user-attachments/assets/a4aa5438-e081-4eb8-8bd3-993df443a1b4)

# 📚 Splunk Components - Quick Notes
# 1. Forwarder
  Purpose: Collects and sends data to Splunk indexers.

  Types:

  Universal Forwarder (UF): Lightweight, only forwards raw data.

   Heavy Forwarder (HF): Parses, filters, and forwards data; can do some indexing too.

# 2. Indexer
  Purpose:

  Receives incoming data.

  Parses, processes, and indexes the data for faster search.
    Key functions:
    Data parsing
    Indexing
    Storing events
    Handling search requests

# 3. Search Head
Purpose: Provides a user interface for users to search, analyze, and visualize data.

Important: It does not store data; it only sends search queries to the indexers.

# 4. Deployment Server
Purpose: Manages and deploys configurations (like apps, settings) to multiple forwarders or Splunk instances.

Useful when: You have hundreds or thousands of forwarders.

# 5. Cluster Master (Now called Cluster Manager)
Purpose: Manages indexer clusters to ensure data replication and high availability.

Roles:

Controls peer nodes (indexers)

Manages data replication factors

# 6. License Master
Purpose:

Tracks Splunk license usage.

Ensures you stay within licensed data ingestion limits.

# 7. Monitoring Console (MC)
Purpose:

Health monitoring of Splunk environment.

Provides dashboards on system performance, indexing, searches, etc.

# 8. Heavy Forwarder (again, because sometimes it's separately discussed)
Purpose:

Parses data before sending it to the indexer.

Useful for filtering, routing, and enriching data at the source.

![image](https://github.com/user-attachments/assets/953ae5aa-d585-4c38-9b4b-01258f050394)

# 📚 Splunk Deployment Models

![image](https://github.com/user-attachments/assets/7c84d308-89b3-4497-8c45-3990af9172b3)

# 1. Standalone Deployment
Use case: Small environments, POC (Proof of Concept), testing.

Setup:

One single Splunk instance acts as indexer, search head, and forwarder together.

Pros: Easy to set up.

Cons: Not scalable, single point of failure.

# 2. Distributed Deployment
Use case: Medium to large environments.

Setup:

Forwarders → collect data.

Indexers → store and index data.

Search Heads → search and analyze data.

Key Points:

Components are separated for performance and scalability.

Allows horizontal scaling (add more indexers/search heads as needed).

# 3. Indexer Clustering
Use case: High availability and disaster recovery for data.

Setup:

Multiple indexers (peers) grouped together.

Managed by a Cluster Master (Manager).

Key Concepts:

Replication Factor: Number of copies of each piece of data.

Search Factor: Number of searchable copies.

Types:

Single-site cluster: All nodes in one location.

Multi-site cluster: Nodes spread across multiple sites for better disaster recovery.

# 4. Search Head Clustering
Use case: High availability and load balancing for searches.

Setup:

Multiple search heads form a cluster.

Managed by a Captain (one elected leader node).

Key Features:

Shared configuration (knowledge bundles).

User sessions and scheduled searches are balanced across search heads.

# 5. Deployment Server Model
Use case: Manage configurations for large numbers of forwarders.

Setup:

One Deployment Server centrally manages and pushes configuration files, apps, and updates to Universal Forwarders.

