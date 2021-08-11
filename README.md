My Django on GCP App Engine
======================
Let´s share.

Google Cloud Console
--------------------
New customers get $300 in free credits to spend on Google Cloud during the first 90 days. All Google Cloud customers get 28 instance hours per day free of charge. http://console.cloud.google.com

Google Cloud SDK
----------------
Tools and libraries for interacting with Google Cloud products and services. https://cloud.google.com/sdk

Google Cloud SQL
----------------
Fully managed relational database service for MySQL, PostgreSQL, and SQL Server. https://cloud.google.com/sql


gcloud services enable sqladmin
gcloud sql instances create portal-pro1 --database-version MYSQL_8_0 --tier=db-f1-micro --zone us-east1-b


https://dl.google.com/cloudsql/cloud_sql_proxy_x64.exe
curl -o cloud_sql_proxy https://dl.google.com/cloudsql/cloud_sql_proxy.darwin.amd64 && chmod +x cloud_sql_proxy
wget https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 -O cloud_sql_proxy && chmod +x cloud_sql_proxy
gcloud sql instances describe portal-pro1
cloud_sql_proxy.exe -instances="core-160214:us-east1:portal-pro1"=tcp:3306

Google Cloud App Engine
----------------------- 
Build highly scalable applications on a fully managed serverless platform. https://cloud.google.com/appengine
