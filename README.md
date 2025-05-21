# Scheduling HeatWave Instance with OCI CLI and Cron

This README provides instructions to schedule a HeatWave instance using a cronjob on a Linux machine with OCI CLI.

## 1. Spin Up a Linux Instance
Launch a Linux 8 instance (Oracle Linux preferred) where the cronjob will run.

## 2. Install OCI CLI
Run the following commands to install the OCI CLI on Oracle Linux 8:

sudo dnf -y install oraclelinux-developer-release-el8
sudo dnf install python36-oci-cli

To verify the installation:

oci --version

Ensure the `.oci` folder exists in the home directory (e.g., /home/opc/.oci/) and includes:

- A valid API key pair
- A properly configured `config` file with the following format:

[DEFAULT]
user=ocid1.user.oc1..aaaaaaaad**********
fingerprint=1f:48:e8:c8:ce:7c:80*******
key_file=/home/opc/.oci/oci_api_key.pem
tenancy=ocid1.tenancy.oc1..aaa*********
region=ap-melbourne-1

## 3. Create a Cronjob to Control HeatWave

To start editing the crontab:

crontab -e

Add the following line (modify timing and DB system ID as needed):

* * * * * oci mysql db-system heatwave-cluster stop --db-system-id $db_system_id

To check your current crontab entries:

crontab -l

To view cron logs and confirm execution:

sudo tail /var/log/cron

## Notes for Using `vim` in Crontab

- Jump to the bottom: Shift + g
- Enter insert mode: Press i
- Save and exit:
  - Press Esc
  - Type :wq
  - Press Enter

## Cron Timing Help

To experiment and understand cronjob timing patterns, use online tools such as:
https://crontab.guru
