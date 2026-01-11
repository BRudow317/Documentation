# PostgreSQL Local Setup

## Optional: VHD Setup for Data Storage
Goal: Create and mount a Virtual Hard Disk (VHD) for storing PostgreSQL data.

## Database Setup (PostgreSQL on VHD)
Goal: Install PostgreSQL but store the actual data on the Q drive.
1.	Install PostgreSQL Binaries:
  - Download and install the latest PostgreSQL for Windows (e.g., v16 or v17).
  - **Critical**: During installation, you can uncheck "Launch Stack Builder".
  - **Critical**: You can let it install binaries to C:\Program Files\PostgreSQL\..., but we will configure the Data Directory manually below.
2.	Initialize Data Directory on Q:
  - open a Command Prompt as Administrator.
  - Navigate to the bin folder (e.g., cd "C:\Program Files\PostgreSQL\17\bin").
  - Run the initialization command pointing to your VHD: initdb -D "Q:\quickbitlabs\pg_data" -U postgres -W (The -W flag prompts you to set a superuser password. Remember this!)
3.	Start Database Manually (Test):
  - Run: pg_ctl -D "Q:\quickbitlabs\pg_data" -l "Q:\quickbitlabs\logs\pg_logfile.log" start
4.	Create Application Database:
  - Run: createdb -U postgres quickbitlabs_db

## Automation (Persistence)
Goal: Ensure everything survives a reboot.
1.	Auto-Mount VHD: Disk Management -> Q: persistent.
2.	PostgreSQL Service:
  - Register the Postgres service pointing to your Q drive: pg_ctl register -N "postgresql-quickbit" -D "Q:\quickbitlabs\pg_data"
  - Set it to Automatic in Windows Services (services.msc).
3.	Python & Tunnel Services:
  - Use NSSM to run run_server.py.
  - Use cloudflared service install.