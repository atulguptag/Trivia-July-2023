### Lab Name - Managing SMB Workloads and Optimizing Storage Usage with NetApp BlueXP & Cloud Volumes ONTAP
### Solution Video - [CLICK HERE](https://youtu.be/UlxHJE0xn7o)

## Task 1. Set up service accounts

```cmd
export PROJECT_ID=$(gcloud config get-value project)
export serviceAccount="netapp-cloud-manager@"$PROJECT_ID".iam.gserviceaccount.com"
export serviceAccount2="netapp-cvo@"$PROJECT_ID".iam.gserviceaccount.com"

# assign roles to the netapp-cloud-manager service account
gcloud projects add-iam-policy-binding $PROJECT_ID \
      --member="serviceAccount:${serviceAccount}" \
      --role='roles/iam.serviceAccountAdmin'
gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member="serviceAccount:${serviceAccount}" \
        --role='roles/storage.objectAdmin'
gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member="serviceAccount:${serviceAccount}" \
        --role='roles/deploymentmanager.editor'
gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member="serviceAccount:${serviceAccount}" \
        --role='roles/logging.admin'
gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member="serviceAccount:${serviceAccount}" \
        --role='roles/compute.admin'
gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member="serviceAccount:${serviceAccount}" \
        --role='roles/cloudkms.admin'
gcloud projects add-iam-policy-binding $PROJECT_ID \
        --member="serviceAccount:${serviceAccount}" \
        --role='roles/storage.admin'

# create netapp-cvo service account
gcloud iam service-accounts create netapp-cvo --display-name=netapp-cvo
gcloud projects add-iam-policy-binding $PROJECT_ID \
      --member="serviceAccount:${serviceAccount2}" \
      --role='roles/storage.objectAdmin'
gcloud projects add-iam-policy-binding $PROJECT_ID \
      --member="serviceAccount:${serviceAccount2}" \
      --role='roles/storage.admin'
gcloud iam service-accounts add-iam-policy-binding ${serviceAccount2} --member="serviceAccount:${serviceAccount}" --role='roles/iam.serviceAccountUser'
```


## Task 2. Set up a new ONTAP storage environment
```cmd 
Follow the video instruction carefully to complete the Task 2.
```

## Task 3. Set up a Windows Virtual Machine
```cmd

export PROJECT_ID=$(gcloud config get-value project)
gcloud beta compute --project=$PROJECT_ID instances create windows-vm --zone=us-central1-c --machine-type=n1-standard-1 --image-project=windows-cloud --image-family=windows-2016
```