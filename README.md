# My Django on GCP App Engine
Let´s share.

## [Google Cloud Console](http://console.cloud.google.com)
New customers get $300 in free credits to spend on Google Cloud during the first 90 days. All Google Cloud customers get 28 instance hours per day free of charge. 

To create a new project, do the following:

### 1. Go to the Manage resources page in the Cloud Console.
### [Go to the Manage Resources page](https://console.cloud.google.com/cloud-resource-manager?_ga=2.65163304.789727678.1628784528-114546109.1601312323&_gac=1.216221540.1628784616.CjwKCAjwjdOIBhA_EiwAHz8xmyaQuvGfBGN9u88yl5g4NICzITiWGIQIeJM1qJDhl1I7Sli1pq87_BoCwzkQAvD_BwE)
### 2. On the Select organization drop-down list at the top of the page, select the organization in which you want to create a project. If you are a free trial user, skip this step, as this list does not appear.
### 3. Click Create Project.
### 4. In the New Project window that appears, enter a project name and select a billing account as applicable. A project name can contain only letters, numbers, single quotes, hyphens, spaces, or exclamation points, and must be between 4 and 30 characters.
### 5. Enter the parent organization or folder in the Location box. That resource will be the hierarchical parent of the new project.
### 6. When you're finished entering new project details, click Create.

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

> Welcome! This command will take you through the configuration of gcloud.
> Your current configuration has been set to: [default]
> You can skip diagnostics next time by using the following flag:
>  gcloud init --skip-diagnostics
> Network diagnostic detects and fixes local network connection issues.
> Checking network connection...done.                                                                                                                                                              
> Reachability Check passed.
> Network diagnostic passed (1/1 checks passed).
> You must log in to continue. Would you like to log in (Y/n)? y

> Google Cloud SDK wants to access your Google Account
> xxxx@gmail.com
> This will allow Google Cloud SDK to:
> See, edit, configure, and delete your Google Cloud data and see the email address for your Google Account.
> View and manage your Google Compute Engine resources
> View and manage your applications deployed on Google App Engine
> Make sure you trust Google Cloud SDK
> You may be sharing sensitive info with this site or app. You can always see or remove access in your Google Account.
> Learn how Google helps you share data safely.
> See Google Cloud SDK’s Privacy Policy and Terms of Service.

### Allow

> Please enter numeric choice or text value (must exactly match list item):
> Do you want to configure a default Compute Region and Zone? (Y/n)? 
> Please enter numeric choice or text value (must exactly match list item):  8


## [Google Cloud SQL](https://cloud.google.com/sql)
Fully managed relational database service for MySQL, PostgreSQL, and SQL Server. 

Requirements for testing at local laboratories:

```
sudo apt install mysql-client default-mysql-client python3-mysqldb libssl-dev libsqlclient-dev
```

Cloud SQL Service Activation:

```
gcloud services enable sqladmin
```

Create an instance that will serve as a database for django:

```
gcloud sql instances create --database-version MYSQL_8_0 --tier=db-f1-micro --zone us-central1-a
```

Create a user to access the django database:

```
gcloud sql users create djangouser --instance=djangodb --host=% --password=djangoPassword
```

> Note that there is a password that must be changed in productive environments

Create a database within instance that will serve as a database for django:

```
gcloud sql databases create djangodb --instance=djangodb
```

List instance details:

```
gcloud sql instances describe djangodb
```

## [Google Cloud App Engine](https://cloud.google.com/appengine)
Build highly scalable applications on a fully managed serverless platform.

For the example, the google-cloud-sdk-app-engine-python component need be installed as follows:
```
sudo apt-get install google-cloud-sdk-app-engine-python google-cloud-sdk-app-engine-python-extras python3-pip python3-dev 
```

Clone a custom django repository
```
git clone https://github.com/cyranorizzo/AppEngine.git
```

Change directory to the django project
```
cd AppEngine
```

Write the credentials file with the previsly database, user and password created
```
cat > .env << EOF
# Database credentials
DB_HOST = '/cloudsql/[project]:[region]:[instance]'
DB_NAME = 'djangodb'
DB_USER = 'djangouser'
DB_PASSWORD = 'djangoPassword'
EOF
```
> Note the instance is buited from [project]:[region]:[instance]

Install django dependences
```
pip install -r requirements.txt
```

Start a localhost proxy to the database on Google Cloud SQL
```
./cloud_sql_proxy -instances="[project]:[region]:[instance]"=tcp:3306
```
> Note the instance is buited from [project]:[region]:[instance]
> I recommend running on another terminal (tty)

Inicialize the database with django requiremetns
```
python3 manage.py migrate
```

Create a super user to the admin
```
python3 manage.py createsuperuser
```

Start localy to test
```
python3 manage.py runserver 80
```

Collect all static files
```
python3 manage.py collectstatic
```

Finally deploy
```
gcloud app deploy
```
> You can run the same command many times 

After this you can reach the application from the target url.
The debug are automaticaly set to false, so the root site my not work, try to access xxxx.xx.x.appspot.com</admin>