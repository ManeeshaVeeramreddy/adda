# Portfolio Monitoring – Grafana Cloud

## Overview

Grafana Cloud is used to monitor the portfolio application and its AWS EC2 server.

The purpose of monitoring is to observe server performance, identify resource usage, and understand the health of the deployed application.

## Infrastructure

- **Application:** Portfolio website
- **Hosting:** AWS EC2
- **Operating System:** Ubuntu
- **Monitoring Platform:** Grafana Cloud
- **Metrics Collection:** Grafana Alloy

## Monitoring Objectives

- Monitor CPU utilization.
- Monitor memory usage.
- Observe server performance.
- Identify resource usage patterns.
- View monitoring information through Grafana Cloud dashboards.

## Architecture

AWS EC2 (Ubuntu Server) → Grafana Alloy → Grafana Cloud → Monitoring Dashboards

## Benefits

- Provides visibility into server performance.
- Helps identify resource-related issues.
- Supports continuous monitoring of the deployed infrastructure.
- Provides a centralized dashboard for monitoring information.

## Note

This monitoring setup uses the existing AWS EC2 instance. No additional EC2 instance is required.
