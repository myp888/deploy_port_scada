# gsfpc_buildscada
Dockerfile to create Ignition Docker Image with Auto-Restore

This project builds a preconfigured Docker image for [Inductive Automation Ignition](https://inductiveautomation.com/), with: 
- ✅ Automatic gateway restore on first run
- ✅ Pre-installed `.modl` modules
- ✅ Persistent gateway data using Docker volumes
- ✅ Healthcheck support for orchestrators (Docker Compose, Kubernetes, etc.)

--- ## 🔧 Quick Start ### 
1. Build the Docker image
   
     _docker buildx build -t my-ignition-image ._ 
   
2. Run it with data persistence
   
   _docker volume create ignition_data docker run -p 8088:8088 \ -v ignition_data:/usr/local/bin/ignition/data \ my-ignition-image_
   
or 

docker volume create ignition_data && \
docker run -d \
  --name ignition_gateway \
  -p 8088:8088 -p 8043:8043 -p 8060:8060 -p 8061:8061 \
  -v ignition_data:/usr/local/share/ignition/data \
  -e ACCEPT_IGNITION_EULA=Y \
  -e GATEWAY_ADMIN_PASSWORD=password \
  my-ignition-image

volume doesn't overwrite or delete if run more than 1

3. Then open: http://localhost:8088

# 
📁 Folder Structure  

    .
    ├── Dockerfile
    ├── entrypoint.sh
    ├── restore.gwbk       # Gateway backup (optional)
    └── modules/
        └── my-module.modl   # Optional modules  
    
# 
🔒 Default Credentials

These are set in the Dockerfile:
-	Username: admin
-	Password: password
  
You can change them by editing the environment variables in the Dockerfile.

# 
💡 Notes

-	The gateway restore only happens if the data volume is empty
-	The healthcheck ensures the web UI is accessible at /main/system/console
-	Add more .modl files to the modules/ folder to preload them

# 
📄 License
MIT — customize freely for internal or commercial use.


