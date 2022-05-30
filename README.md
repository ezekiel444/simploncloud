# Du IaaS au SaaS, par script !

# CREATE EXACT LOCATION:
	 az account list-locations -o table

# CREATE AZURE RESOURCE GROUP:

	az group create -l northcentralus -n EmainResource

# CREATE A STANDARD APP SERVICE PLAN WITH LINUX:
	
	az appservice plan create --name EmainPlan --resource-group EmainResource --sku FREE --is-linux

# CREATE A WEB APP:
	
	az webapp create --resource-group EmainResource --plan EmainPlan --name EmainAppService --runtime 'PHP|7.4' --deployment-local-git

# BROWSE YOUR WEBSITE:

	http://<app-name>.azurewebsites.net
  
# CREATE AN AZURE DATABASE FOR MARIADB SERVER

	az mariadb server create --resource-group EmainResource --name EmainDB  --location northcentralus --admin-user myadmin --admin-password <server_admin_password> --sku-name GP_Gen5_2 --version 10.2

# CONFIGURE FIREWALL RULE	

	az mariadb server firewall-rule create --resource-group EmainResource --server EmainDB --name AllowMyIP --start-ip-address 192.168.0.1 --end-ip-address 192.168.0.1

# SSL SETTINGS(disables SSL):
	
	az mariadb server update --resource-group EmainResource --name EmainDB --ssl-enforcement Disabled

# GET ACCESS CREDENTIALS

	az mariadb server show --resource-group EmainResource --name EmainDB

# CONNECT TO YOUR SERVER

	mysql -h mydemoserver.mariadb.database.azure.com -u myadmin@mydemoserver -p

