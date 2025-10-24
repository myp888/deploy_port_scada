# Deploy GSFPC Gateway

create Ignition container - gsfpc_scada_gateway

modify the yml to change name 'gsfpc_scada_gateway'



## 🔧 Quick Start ##

1. Compose gateway


	 docker volume create ignition_datadocker volume create ignition_data docker compose up -d 

 
	 docker run -d --name ignition_gateway -p 8088:8088 -p 8043:8043 -p 8060:8060 -p 8061:8061 -v ignition_data:/usr/local/share/ignition/data -e ACCEPT_IGNITION_EULA=Y -e GATEWAY_ADMIN_PASSWORD=password gsfpc/pfda_scada_image


	 

   
or 

	 docker volume create ignition_data 

 
	 docker run -d --name ignition_gateway -p 8088:8088 -p 8043:8043 -p 8060:8060 -p 8061:8061 -v ignition_data:/usr/local/share/ignition/data -e ACCEPT_IGNITION_EULA=Y -e GATEWAY_ADMIN_PASSWORD=password gsfpc/pfda_scada_image


volume doesn't overwrite or delete if run more than 1

2. Then open: http://localhost:8088

# 
📁 Folder Structure  

    .
    ├── Dockerfile
    ├── entrypoint.sh
    └── modules/
        └── my-module.modl   # Optional modules  
    
# 
🔒 Default Credentials

These are set in the yml file:
-	Username: pfdagsfpc
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


