echo "Welcome To Complete Guide To Create Your Saas App From The Command Line Yahhhh!!!!!"
	 az account list-locations --output table
echo "please lookup the table above and provide a location"
$location = read-host "Enter your location"
	
$resourceName = read-host "Enter a resource name"	
$appServicePlan = read-host "Enter your app service plan"
$appServiceName = read-host "Enter your web app name"
$dbName = read-host "Enter your mariaDb name"
$username = read-host "Enter your username for mariadb"
$password = read-host "Enter your password for mariadb"		
az group create -l $location -n $resourceName
az appservice plan create --name $appServicePlan --resource-group $resourceName --sku FREE --is-linux
az webapp create --resource-group $resourceName --plan $appServiceName --name $appServiceName --runtime 'PHP|7.4' --deployment-local-git
echo "BROWSE YOUR WEBSITE: on http://$appServiceName.azurewebsites.net"
	az mariadb server create --resource-group $resourceName --name $dbName  --location $location --admin-user $username --admin-password $password --sku-name GP_Gen5_2 --version 10.2
	az mariadb server firewall-rule create --resource-group $resourceName --server $dbName --name AllowMyIP --start-ip-address 192.168.0.1 --end-ip-address 192.168.0.1
echo "SSL SETTINGS(disables SSL):"
	az mariadb server update --resource-group $resourceName --name $dbName --ssl-enforcement Disabled
echo "GET ACCESS CREDENTIALS"
	az mariadb server show --resource-group $resourceName --name $dbName
echo "CONNECT TO YOUR SERVER with 'mysql -h $dbName.mariadb.database.azure.com -u myadmin@mydemoserver -p' "