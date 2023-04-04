## NYC Citibike-Data-Pipeline

### Overview:



### Problem description:



### Technologies:

Following technologies are used in implementing this pipeline

* Cloud: **GCP**
  * Data Lake: **GCS**
  * Data warehouse: **Big Query**
* **Terraform**: Infrastructure as code (IaC) - creates project configuration for GCP to bypass cloud GUI.
* Workflow orchestration: **Prefect**
* Data Transformation: **DBT**
* Data Visualisation: **looker data studio**


### Citibike Pipeline Architecture:

![image](https://user-images.githubusercontent.com/10378935/229666445-7873dc6e-9314-43a0-9aa2-c01a3202e01a.png)



## Setup to run the project


1. Clone the repo and install the neccesary packages

```bash
pip install -r requirements.txt
```

2. Next you need to setup your Google Cloud environment
- Create a Google Cloud Platform project, if you do not already have one(https://console.cloud.google.com/cloud-resource-manager)
- Configure Identity and Access Management (IAM) for the service account, provide the following privileges: 
  * BigQuery Admin
  * Storage Admin 
  * Storage Object Admin
- Download the JSON credentials and save it somehwere you'll remember, which will be JSON key.
- Install the [Google Cloud SDK](https://cloud.google.com/sdk/docs/install-sdk)
- Configure the environment variable point to your GCP key(https://cloud.google.com/docs/authentication/application-default-credentials#GAC) and authenticate it using following commands
```bash
export GOOGLE_APPLICATION_CREDENTIALS=<path_to_your_credentials>.json
gcloud auth application-default login
```

3. Set up the infrastructure of the project using Teeraform
- If you do not have Terraform installed you can install it [here](https://developer.hashicorp.com/terraform/downloads) and then add it to your PATH
- Once donwloaded run the following commands:
```bash
cd terraform/
terraform init
terraform plan -var="project=<your-gcp-project-id>"
terraform apply -var="project=<your-gcp-project-id>"
```

4. Run python code in Prefect folder
- After installing the required python packages, prefect should be installed
- You can setup the prefect server so that you can access the UI using the command below:
```bash
prefect orion start
```
- access the UI at: http://127.0.0.1:4200/
- You will then want to change out the blocks so that they are registered to your credentials for GCS and Big Query. This can be done in the Blocks options
- You can keep the blocks under the same names as in the code or change them. If you do change them make sure to change the code to reference the new block name
- Go back to the terminal and run:
  ```bash
  cd prefect/
  ```
- then run
```bash
  python citibike_data_pipeline.py
```
