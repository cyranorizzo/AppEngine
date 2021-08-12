# My Django on GCP App Engine
Let´s share.

## [Google Cloud Console](http://console.cloud.google.com)
New customers get $300 in free credits to spend on Google Cloud during the first 90 days. All Google Cloud customers get 28 instance hours per day free of charge. 

## [Google Cloud SDK](https://cloud.google.com/sdk)
Tools and libraries for interacting with Google Cloud products and services. 

### 1. Add the Cloud SDK distribution URI as a package source:
```
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
```

Make sure you have apt-transport-https installed:
```
sudo apt-get install apt-transport-https ca-certificates gnupg
```
> Note: If your distribution does not support the signed-by option run this command instead:

```
echo "deb https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
```
> Note: Make sure you do not have duplicate entries for the cloud-sdk repo in /etc/apt/sources.list.d/google-cloud-sdk.list.


### 2. Import the Google Cloud public key:
```
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
```
> Note: If you are unable to get latest updates due to an expired key, obtain the latest apt-get.gpg key file.

> Note: If your distribution's apt-key command does not support the --keyring argument run this command instead:
```
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

### 3. Update and install the Cloud SDK:
```
sudo apt-get update && sudo apt-get install google-cloud-sdk
```
For additional apt-get options, such as disabling prompts or dry runs, refer to the apt-get man pages.

Docker Tip: If installing the Cloud SDK inside a Docker image, use a single RUN step instead:
```
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg  add - && apt-get update -y && apt-get install google-cloud-sdk -y
```

### 4. Optionally, install any of these additional components:
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

For the example, the google-cloud-sdk-app-engine-python component need be installed as follows:
```
sudo apt-get install google-cloud-sdk-app-engine-python
```

### 5. Run gcloud init to get started:
```
gcloud init
```

## [Google Cloud SQL](https://cloud.google.com/sql)
Fully managed relational database service for MySQL, PostgreSQL, and SQL Server. 

sudo apt install mysql-client python3-mysqldb
gcloud services enable sqladmin
gcloud sql instances create gcloud sql connect djangodb --user=root --database-version MYSQL_8_0 --tier=db-f1-micro --zone us-central1-a
gcloud sql users create djangouser --instance=djangodb --host=% --password=djangoPassword
gcloud sql databases create djangodb --instance=djangodb
gcloud sql instances describe djangodb
curl -o cloud_sql_proxy https://dl.google.com/cloudsql/cloud_sql_proxy.darwin.amd64 && chmod +x cloud_sql_proxy
./cloud_sql_proxy -instances="bedu-tech-lab:us-central1:djangodb"=tcp:3306
mysql -p -u djangouser -P 3306

## [Google Cloud App Engine](https://cloud.google.com/appengine)
----------------------- 
Build highly scalable applications on a fully managed serverless platform.

For the example, the google-cloud-sdk-app-engine-python component need be installed as follows:
```
sudo apt-get install google-cloud-sdk-app-engine-python
```

```
sudo apt-get install google-cloud-sdk-app-engine-python-extras
```