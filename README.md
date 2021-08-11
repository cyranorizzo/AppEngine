#My Django on GCP App Engine
Let´s share.

Google Cloud Console
--------------------
New customers get $300 in free credits to spend on Google Cloud during the first 90 days. All Google Cloud customers get 28 instance hours per day free of charge. http://console.cloud.google.com

Google Cloud SDK
----------------
Tools and libraries for interacting with Google Cloud products and services. https://cloud.google.com/sdk

Installation
1. Add the Cloud SDK distribution URI as a package source:
```
$ echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
```

Make sure you have apt-transport-https installed:

$ sudo apt-get install apt-transport-https ca-certificates gnupg
> Note: If your distribution does not support the signed-by option run this command instead:

$ echo "deb https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
Note: Make sure you do not have duplicate entries for the cloud-sdk repo in /etc/apt/sources.list.d/google-cloud-sdk.list.


2. Import the Google Cloud public key:

$ curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
> Note: If you are unable to get latest updates due to an expired key, obtain the latest apt-get.gpg key file.

> Note: If your distribution's apt-key command does not support the --keyring argument run this command instead:

$ curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -


3. Update and install the Cloud SDK:

$ sudo apt-get update && sudo apt-get install google-cloud-sdk
For additional apt-get options, such as disabling prompts or dry runs, refer to the apt-get man pages.
Docker Tip: If installing the Cloud SDK inside a Docker image, use a single RUN step instead:


RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg  add - && apt-get update -y && apt-get install google-cloud-sdk -y


4. Optionally, install any of these additional components:
- google-cloud-sdk-app-engine-python
- google-cloud-sdk-app-engine-python-extras
- google-cloud-sdk-app-engine-java
- google-cloud-sdk-app-engine-go
- google-cloud-sdk-bigtable-emulator
- google-cloud-sdk-cbt
- google-cloud-sdk-cloud-build-local
- google-cloud-sdk-datalab
- google-cloud-sdk-datastore-emulator
- google-cloud-sdk-firestore-emulator
- google-cloud-sdk-pubsub-emulator
- kubectl

For example, the google-cloud-sdk-app-engine-java component can be installed as follows:

sudo apt-get install google-cloud-sdk-app-engine-java


5. Run gcloud init to get started:

gcloud init

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
