# Portfolio Monitoring – Grafana Cloud Synthetic Monitoring

## Overview

Grafana Cloud Synthetic Monitoring is used to monitor the availability and response of my portfolio website.
## Dashboard Screenshot

![Grafana Synthetic Monitoring Dashboard](screenshots/grafana-monitoring.png)

It performs automated HTTP checks on the website and displays monitoring results through graphical dashboards.

## Monitoring Configuration

- **Monitoring Platform:** Grafana Cloud
- **Feature:** Synthetic Monitoring
- **Check Type:** API / HTTP
- **HTTP Method:** GET
- **Target URL:** https://maneeshaveeramreddy.github.io/portfolio-simple/
- **Application:** Portfolio Website

## Monitoring Workflow

1. Create an API/HTTP check in Grafana Cloud Synthetic Monitoring.
2. Configure the HTTP method as GET.
3. Provide the portfolio website URL as the target.
4. Grafana periodically sends requests to the website.
5. The monitoring dashboard displays the check results over time.

## Monitoring Results

The dashboard provides a graphical representation of monitoring results, helping identify:

- Website availability.
- Successful and failed HTTP checks.
- Response-time variations.
- Website accessibility over time.

## Benefits

- Automatically checks website availability.
- Helps identify website downtime.
- Tracks response-time changes.
- Provides visual monitoring through Grafana dashboards.

## Architecture

Grafana Cloud Synthetic Monitoring → HTTP GET Request → Portfolio Website → Monitoring Results and Dashboard

## Conclusion

Synthetic Monitoring provides an automated way to verify whether the deployed portfolio website is accessible and responding to HTTP requests.
