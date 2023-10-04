# Changes for MWAA to Run Locally with Podman

This document outlines the steps taken to modify the AWS Managed Workflows for Apache Airflow (MWAA) local runner to operate using Podman, instead of Docker.

## Directory Structure Setup

### 1. Podman Directory Creation
- A new directory named `podman` has been created under `aws-mwaa-local-runner`.

## File Copy Operations

### 2. Config Folder
- **Source**: `aws-mwaa-local-runner/docker/config`
- **Destination**: `aws-mwaa-local-runner/podman/config`

### 3. Script Folder
- **Source**: `aws-mwaa-local-runner/docker/script`
- **Destination**: `aws-mwaa-local-runner/podman/script`

### 4. Dockerfile
- **Source**: `aws-mwaa-local-runner/docker/Dockerfile`
- **Destination**: `aws-mwaa-local-runner/podman/Dockerfile`

### 5. docker-compose-local.yml File
- **Source**: `aws-mwaa-local-runner/docker/docker-compose-local.yml`
- **Destination**: `aws-mwaa-local-runner/podman/podman-compose-local.yml`

## File Modifications

### 6. Line Separator Changes
- All files within the `podman` directory had their line separators changed from `CRLF` to `LF`.

### 7. Volume Config in `podman-compose-local.yml`
- **Original**:
  ```yml
  pg_data:/var/lib/postgresql/data
  ```
- **Updated** to include the following at the end of the `.yml` file, at the same level as services:
  ```yml
  volumes:
    pg_data:
  ```

### 8. `aws-mwaa-local-runner-2_6_default.conflist` File Change
- The `cniVersion` in `/etc/cni/net.d/aws-mwaa-local-runner-2_6_default.conflist` file was changed from `1.0.0` to `0.4.0`.
