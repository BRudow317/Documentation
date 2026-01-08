# Project Plan: QuickBitLabs Host Origin
## Phase 1: Infrastructure & Storage
### Goal: Ensure the VHD is mounted and the directory structure is ready.
1.	Mount VHD:
    - Drive Letter: Q:
    - Ensure the drive is formatted and accessible in Windows Explorer.
2.	Directory Structure:
    - Root Path: Q:\quickbitlabs
    - Standard File Layout:

```properties
	Q:\quickbitlabs\
	├── run_server.py (The Python entry point)
	├── requirements.txt (Dependencies)
	├── config.yml (Cloudflare Tunnel configuration)
	├── /pg_data (PostgreSQL Database Storage - New)
	├── /static (Public assets: css, js, img)
	├── /templates (HTML files)
	└── /logs (Server logs)
```

## Phase 1.5: Database Setup (PostgreSQL on VHD)
### Goal: Install Postgres but store the actual data on the Q drive.
1.	Install PostgreSQL Binaries:
    - Download and install the latest PostgreSQL for Windows (e.g., v16 or v17).
    - Critical: During installation, you can uncheck "Launch Stack Builder".
    - Critical: You can let it install binaries to C:\Program Files\PostgreSQL\..., but we will configure the Data Directory manually below.
2.	Initialize Data Directory on Q:
    - Open a Command Prompt as Administrator.
    - Navigate to the bin folder (e.g., cd "C:\Program Files\PostgreSQL\17\bin").
    - Run the initialization command pointing to your VHD: initdb -D "Q:\quickbitlabs\pg_data" -U postgres -W (The -W flag prompts you to set a superuser password. Remember this!)
3.	Start Database Manually (Test):
    - Run: pg_ctl -D "Q:\quickbitlabs\pg_data" -l "Q:\quickbitlabs\logs\pg_logfile.log" start
4.	Create Application Database:
    - Run: createdb -U postgres quickbitlabs_db
## Phase 2: Python Environment (FastAPI + Uvicorn)
### Goal: Get the high-performance ASGI application running locally with DB support.
1.	Virtual Environment:
    - Open terminal in Q:\quickbitlabs.
    - Run: python -m venv venv
    - Activate: .\venv\Scripts\activate
2.	Dependencies:
    - Install packages: pip install fastapi uvicorn[standard] jinja2 requests sqlalchemy psycopg2-binary
    - Freeze requirements: pip freeze > requirements.txt
3.	Application Logic:
    - Create main.py: Updated to include SQLAlchemy connection logic.
    - Create run_server.py: Launcher script.
4.	Local Testing:
    - Run: python run_server.py
    - Check http://localhost:8000/health to verify DB connection.
Phase 3: Cloudflare Tunnel Configuration
Goal: Expose the local port (8000) to quickbitlabs.com.
1.	Install Cloudflared:
    - Download cloudflared for Windows.
2.	Authenticate:
    - Run: cloudflared tunnel login
3.	Create Tunnel:
    - Run: cloudflared tunnel create QuickBitLabsToAndromeda
    - Action: Save the Tunnel ID (UUID).
4.	Configure Routing (DNS):
    - Run: cloudflared tunnel route dns QuickBitLabsToAndromeda quickbitlabs.com
5.	Configuration File (config.yml):
    - Create Q:\quickbitlabs\config.yml:
    - tunnel: <Tunnel-UUID>
    - credentials-file: C:\Users\<USER>\.cloudflared\<Tunnel-UUID>.json
    - 
    - ingress:
    -   - hostname: quickbitlabs.com
    -     service: http://localhost:8000
    -   - service: http_status:404
6.	Run Tunnel:
    - Run: cloudflared tunnel run QuickBitLabsToAndromeda
## Phase 4: Automation (Persistence)
### Goal: Ensure everything survives a reboot.
1.	Auto-Mount VHD: Disk Management -> Q: persistent.
2.	PostgreSQL Service:
    - Register the Postgres service pointing to your Q drive: pg_ctl register -N "postgresql-quickbit" -D "Q:\quickbitlabs\pg_data"
    - Set it to Automatic in Windows Services (services.msc).
3.	Python & Tunnel Services:
    - Use NSSM to run run_server.py.
    - Use cloudflared service install.
## Phase 5: Security & Maintenance
### Goal: Ensure the system is secure and maintainable.
1.	Database Config: Edit Q:\quickbitlabs\pg_data\pg_hba.conf to ensure only 127.0.0.1/32 can connect.
2.	Firewall: Allow Python and Postgres on localhost.

### Project Plan: QuickBitLabs Host Origin
Phase 1: Infrastructure & Storage
Goal: Ensure the VHD is mounted and the directory structure is ready.
1.	Mount VHD:
- Drive Letter: Q:
- Ensure the drive is formatted and accessible in Windows Explorer.
2.	Directory Structure:
- Root Path: Q:\quickbitlabs
- Standard File Layout:
	Q:\quickbitlabs\
	├── main.py (The FastAPI application logic)
	├── run_server.py (The Python entry point to start the server)
	├── requirements.txt (List of Python dependencies)
	├── config.yml (Cloudflare Tunnel configuration)
	├── /static (Public assets)
	│ ├── /css
	│ ├── /js
	│ └── /img
	├── /templates (HTML files for Jinja2 rendering)
	└── /logs (Server access and error logs)
Phase 2: Python Environment (FastAPI + Uvicorn)
Goal: Get the high-performance ASGI application running locally. Note: We are using Uvicorn instead of Waitress because FastAPI requires an ASGI server.
1.	Virtual Environment:
- Open terminal in Q:\quickbitlabs.
- Run: python -m venv venv
- Activate: .\venv\Scripts\activate
2.	Dependencies:
- Install packages: pip install fastapi uvicorn[standard] jinja2 requests
- Note: requests was added per your request, jinja2 is needed if you want to serve HTML templates.
- Freeze requirements: pip freeze > requirements.txt
3.	Application Logic:
- Create main.py: This will contain your API endpoints and routes.
- Create run_server.py: A script to launch Uvicorn programmatically (easier for automation later).
4.	Local Testing:
- Run: python run_server.py
- Verify access at http://localhost:8000 (FastAPI default) in your browser.
- Check auto-generated docs at http://localhost:8000/docs.
Phase 3: Cloudflare Tunnel Configuration
Goal: Expose the local port (8000) to quickbitlabs.com.
1.	Install Cloudflared:
- Download cloudflared for Windows.
2.	Authenticate:
- Run: cloudflared tunnel login
3.	Create Tunnel:
- Run: cloudflared tunnel create QuickBitLabsToAndromeda
- Action: Save the Tunnel ID (UUID) and the credentials file path generated.
4.	Configure Routing (DNS):
- Run: cloudflared tunnel route dns QuickBitLabsToAndromeda quickbitlabs.com
- Note: Routing to the root domain is fully supported by Cloudflare.
5.	Configuration File (config.yml):
- Create Q:\quickbitlabs\config.yml:
- tunnel: <Tunnel-UUID>
- credentials-file: C:\Users\<USER>\.cloudflared\<Tunnel-UUID>.json
- 
- ingress:
-   - hostname: quickbitlabs.com
-     service: http://localhost:8000
-   - service: http_status:404
6.	Run Tunnel:
- Run: cloudflared tunnel run QuickBitLabsToAndromeda
Phase 4: Automation (Persistence)
Goal: Ensure quickbitlabs.com stays online after a reboot.
1.	Auto-Mount VHD: Use Disk Management to ensure Q: is assigned permanently.
2.	System Service:
- Use NSSM (Non-Sucking Service Manager) or Windows Task Scheduler to run Q:\quickbitlabs\venv\Scripts\python.exe Q:\quickbitlabs\run_server.py on startup.
- Install Cloudflare service: cloudflared service install
Phase 5: Security & Maintenance
1.	Docs Security: In main.py, consider disabling /docs and /redoc in production if the API is private.
2.	Firewall: Windows Firewall should allow python connections on localhost.
