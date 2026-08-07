# Home Lab Config

## Overview
This repository contains the configuration files and scripts for my home lab setup.
The goal is to provide a comprehensive and organized structure for managing various aspects of my home lab,
including networking, server configurations, and automation.

## do-ddns container
The do-ddns container is a lightweight Alpine-based utility that keeps a DigitalOcean DNS record in sync with the current public IP address.
When it starts, it:
- looks up the current public IP using ipify
- reads the existing DNS record from DigitalOcean for the configured domain and record ID
- compares the current IP to the record value
- updates the DNS record when the IP has changed or no record exists yet

It expects the following environment variables:
- DOMAIN: the target domain name
- DO_TOKEN: a DigitalOcean API token with permission to update DNS records
- RECORD_ID: the ID of the DNS A record to update

This is useful for home lab setups where the public IP changes periodically and you want your domain to continue resolving to the correct address.
