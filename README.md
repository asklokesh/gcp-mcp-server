# GCP MCP Server

<!-- mcp-name: io.github.asklokesh/gcp-mcp-server -->

<div align="center">

# Gcp Mcp Server

[![GitHub stars](https://img.shields.io/github/stars/LokiMCPUniverse/gcp-mcp-server?style=social)](https://github.com/LokiMCPUniverse/gcp-mcp-server/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/LokiMCPUniverse/gcp-mcp-server?style=social)](https://github.com/LokiMCPUniverse/gcp-mcp-server/network)
[![GitHub watchers](https://img.shields.io/github/watchers/LokiMCPUniverse/gcp-mcp-server?style=social)](https://github.com/LokiMCPUniverse/gcp-mcp-server/watchers)

[![License](https://img.shields.io/github/license/LokiMCPUniverse/gcp-mcp-server?style=for-the-badge)](https://github.com/LokiMCPUniverse/gcp-mcp-server/blob/main/LICENSE)
[![Issues](https://img.shields.io/github/issues/LokiMCPUniverse/gcp-mcp-server?style=for-the-badge)](https://github.com/LokiMCPUniverse/gcp-mcp-server/issues)
[![Pull Requests](https://img.shields.io/github/issues-pr/LokiMCPUniverse/gcp-mcp-server?style=for-the-badge)](https://github.com/LokiMCPUniverse/gcp-mcp-server/pulls)
[![Last Commit](https://img.shields.io/github/last-commit/LokiMCPUniverse/gcp-mcp-server?style=for-the-badge)](https://github.com/LokiMCPUniverse/gcp-mcp-server/commits)

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![MCP](https://img.shields.io/badge/Model_Context_Protocol-DC143C?style=for-the-badge)](https://modelcontextprotocol.io)

[![Commit Activity](https://img.shields.io/github/commit-activity/m/LokiMCPUniverse/gcp-mcp-server?style=flat-square)](https://github.com/LokiMCPUniverse/gcp-mcp-server/pulse)
[![Code Size](https://img.shields.io/github/languages/code-size/LokiMCPUniverse/gcp-mcp-server?style=flat-square)](https://github.com/LokiMCPUniverse/gcp-mcp-server)
[![Contributors](https://img.shields.io/github/contributors/LokiMCPUniverse/gcp-mcp-server?style=flat-square)](https://github.com/LokiMCPUniverse/gcp-mcp-server/graphs/contributors)

</div>

A comprehensive Model Context Protocol (MCP) server for integrating Google Cloud Platform (GCP) APIs with GenAI applications.

## Features

- **Comprehensive GCP Service Coverage**:
  - Compute Engine: VM instances, instance groups, autoscaling
  - Cloud Storage: Buckets, objects, signed URLs, lifecycle policies
  - Cloud Functions: Deploy, invoke, manage serverless functions
  - BigQuery: Datasets, tables, queries, data warehouse operations
  - Cloud SQL: Database instances, backups, replicas
  - Kubernetes Engine (GKE): Cluster management, workload deployment
  - Cloud Run: Serverless container deployment
  - Pub/Sub: Topics, subscriptions, message publishing
  - Cloud IAM: Service accounts, roles, policies
  - Cloud Build: CI/CD pipelines, build triggers
  - Vertex AI: ML model deployment and management
  - Cloud Logging & Monitoring: Metrics, alerts, log analysis
  
- **Authentication Methods**:
  - Service Account JSON keys
  - Application Default Credentials (ADC)
  - OAuth 2.0 for user authentication
  - Workload Identity Federation
  - Impersonation support

- **Enterprise Features**:
  - Multi-project support
  - Cross-region operations
  - VPC-SC (Service Controls) support
  - Cost management and billing alerts
  - Compliance and security scanning
  - Resource labeling and organization

## Installation

```bash
pip install gcp-mcp-server
```

Or install from source:

```bash
git clone https://github.com/asklokesh/gcp-mcp-server.git
cd gcp-mcp-server
pip install -e .
```

## Configuration

Create a `.env` file or set environment variables:

```env
# GCP Credentials
GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account-key.json
GCP_PROJECT_ID=your-project-id
GCP_REGION=us-central1
GCP_ZONE=us-central1-a

# OR use Application Default Credentials
GOOGLE_CLOUD_PROJECT=your-project-id

# Optional Settings
GCP_QUOTA_PROJECT_ID=quota-project-id
GCP_IMPERSONATE_SERVICE_ACCOUNT=service-account@project.iam.gserviceaccount.com
GCP_TIMEOUT=30
GCP_MAX_RETRIES=3

# Multi-Project Support
GCP_PROD_PROJECT_ID=prod-project-id
GCP_PROD_CREDENTIALS=/path/to/prod-key.json

GCP_DEV_PROJECT_ID=dev-project-id
GCP_DEV_CREDENTIALS=/path/to/dev-key.json
```

## Quick Start

### Basic Usage

```python
from gcp_mcp import GCPMCPServer

# Initialize the server
server = GCPMCPServer()

# Start the server
server.start()
```

### Claude Desktop Configuration

Add to your Claude Desktop config:

```json
{
  "mcpServers": {
    "gcp": {
      "command": "python",
      "args": ["-m", "gcp_mcp.server"],
      "env": {
        "GOOGLE_APPLICATION_CREDENTIALS": "/path/to/service-account-key.json",
        "GCP_PROJECT_ID": "your-project-id",
        "GCP_REGION": "us-central1"
      }
    }
  }
}
```

## Available Tools

### Compute Engine Operations

#### List Instances
```python
{
  "tool": "gcp_compute_list_instances",
  "arguments": {
    "project": "my-project",
    "zone": "us-central1-a",
    "filter": "status=RUNNING"
  }
}
```

#### Create Instance
```python
{
  "tool": "gcp_compute_create_instance",
  "arguments": {
    "project": "my-project",
    "zone": "us-central1-a",
    "name": "my-instance",
    "machine_type": "e2-medium",
    "source_image": "projects/debian-cloud/global/images/family/debian-11",
    "disk_size_gb": 20,
    "network_tags": ["web-server"],
    "metadata": {
      "startup-script": "#!/bin/bash\napt-get update\napt-get install -y nginx"
    }
  }
}
```

### Cloud Storage Operations

#### Create Bucket
```python
{
  "tool": "gcp_storage_create_bucket",
  "arguments": {
    "project": "my-project",
    "bucket_name": "my-unique-bucket",
    "location": "US",
    "storage_class": "STANDARD",
    "lifecycle_rules": [
      {
        "action": {"type": "Delete"},
        "condition": {"age": 365}
      }
    ]
  }
}
```

#### Upload Object
```python
{
  "tool": "gcp_storage_upload_object",
  "arguments": {
    "bucket": "my-bucket",
    "object_name": "data/file.txt",
    "content": "File content here",
    "content_type": "text/plain",
    "metadata": {"key": "value"}
  }
}
```

### BigQuery Operations

#### Create Dataset
```python
{
  "tool": "gcp_bigquery_create_dataset",
  "arguments": {
    "project": "my-project",
    "dataset_id": "my_dataset",
    "location": "US",
    "description": "My dataset description"
  }
}
```

#### Execute Query
```python
{
  "tool": "gcp_bigquery_query",
  "arguments": {
    "project": "my-project",
    "query": "SELECT * FROM `project.dataset.table` WHERE date = CURRENT_DATE()",
    "use_legacy_sql": false,
    "maximum_bytes_billed": 1000000000
  }
}
```

### Cloud Functions Operations

#### Deploy Function
```python
{
  "tool": "gcp_functions_deploy",
  "arguments": {
    "project": "my-project",
    "region": "us-central1",
    "name": "my-function",
    "runtime": "python39",
    "entry_point": "main",
    "source_code": "def main(request):\n    return 'Hello World!'",
    "trigger_type": "http",
    "memory_mb": 256
  }
}
```

### GKE Operations

#### Create Cluster
```python
{
  "tool": "gcp_gke_create_cluster",
  "arguments": {
    "project": "my-project",
    "zone": "us-central1-a",
    "cluster_name": "my-cluster",
    "initial_node_count": 3,
    "machine_type": "e2-standard-4",
    "enable_autopilot": false,
    "enable_autoscaling": true,
    "min_nodes": 1,
    "max_nodes": 10
  }
}
```

### Cloud Run Operations

#### Deploy Service
```python
{
  "tool": "gcp_cloudrun_deploy",
  "arguments": {
    "project": "my-project",
    "region": "us-central1",
    "service_name": "my-service",
    "image": "gcr.io/my-project/my-image:latest",
    "memory": "512Mi",
    "cpu": "1",
    "max_instances": 100,
    "allow_unauthenticated": true
  }
}
```

### Vertex AI Operations

#### Deploy Model
```python
{
  "tool": "gcp_vertexai_deploy_model",
  "arguments": {
    "project": "my-project",
    "region": "us-central1",
    "model_name": "my-model",
    "endpoint_name": "my-endpoint",
    "machine_type": "n1-standard-4",
    "min_replica_count": 1,
    "max_replica_count": 3
  }
}
```

## Advanced Configuration

### Multi-Project Support

```python
from gcp_mcp import GCPMCPServer, ProjectConfig

# Configure multiple projects
projects = {
    "production": ProjectConfig(
        project_id="prod-project-id",
        credentials_path="/path/to/prod-key.json",
        default_region="us-central1"
    ),
    "development": ProjectConfig(
        project_id="dev-project-id",
        credentials_path="/path/to/dev-key.json",
        default_region="us-east1"
    ),
    "data-warehouse": ProjectConfig(
        project_id="dw-project-id",
        credentials_path="/path/to/dw-key.json",
        default_region="us-central1"
    )
}

server = GCPMCPServer(projects=projects, default_project="production")
```

### Service Account Impersonation

```python
from gcp_mcp import GCPMCPServer, ImpersonationConfig

impersonation_config = ImpersonationConfig(
    target_service_account="elevated-sa@project.iam.gserviceaccount.com",
    lifetime_seconds=3600,
    delegates=[],
    target_scopes=["https://www.googleapis.com/auth/cloud-platform"]
)

server = GCPMCPServer(impersonation_config=impersonation_config)
```

### Cost Management

```python
from gcp_mcp import GCPMCPServer, CostConfig

cost_config = CostConfig(
    enable_cost_tracking=True,
    budget_alert_threshold=1000.0,  # USD
    cost_allocation_labels=["team", "environment", "project"],
    bigquery_billing_export_dataset="billing_export"
)

server = GCPMCPServer(cost_config=cost_config)
```

## Integration Examples

See the `examples/` directory for complete integration examples:

- `basic_operations.py` - Common GCP operations
- `multi_project.py` - Managing multiple GCP projects
- `data_pipeline.py` - Building data pipelines with BigQuery and Dataflow
- `ml_deployment.py` - Deploying ML models with Vertex AI
- `infrastructure_as_code.py` - Managing infrastructure programmatically
- `cost_optimization.py` - Cost analysis and optimization

## Security Best Practices

1. **Use service accounts** with minimal permissions
2. **Enable audit logging** for all API calls
3. **Implement VPC Service Controls** for data exfiltration prevention
4. **Use Workload Identity** for GKE workloads
5. **Rotate service account keys** regularly
6. **Enable organization policies** for security constraints
7. **Use Cloud KMS** for encryption key management

## Error Handling

The server provides detailed error information:

```python
try:
    result = server.execute_tool("gcp_compute_create_instance", {
        "name": "my-instance",
        "zone": "invalid-zone"
    })
except GCPError as e:
    print(f"GCP error: {e.error_code} - {e.message}")
    if e.error_code == "ZONE_NOT_FOUND":
        print(f"Valid zones: {e.valid_zones}")
```

## Performance Optimization

1. **Use batch operations** where available
2. **Enable request caching** for read operations
3. **Implement regional failover** for high availability
4. **Use Cloud CDN** for static content
5. **Optimize BigQuery queries** with partitioning and clustering

## Contributing

Contributions are welcome! Please read our contributing guidelines and submit pull requests.

## License

MIT License - see LICENSE file for details