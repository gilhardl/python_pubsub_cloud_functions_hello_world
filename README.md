# Python Pub/Sub Cloud Functions Hello World

A hello world project, for Python Pub/Sub Cloud Functions

**Source :** https://cloud.google.com/functions/docs/calling/pubsub

## Google Cloud environment

Run this app in the cloud using Google Cloud Functions and Google Cloud Pub/Sub

### Set GCP project

```
$ gcloud projects list
$ gcloud config set project <your-project-id>
```

### Enable Cloud Functions and Pub/Sub

```
$ gcloud services enable cloudfunctions.googleapis.com cloudbuild.googleapis.com pubsub.googleapis.com
```

### Create Pub/Sub topic

```
$ gcloud pubsub topics create HELLO_WORLD
```
 
### Deploy functions

Run from `functions` directory

```
$ gcloud functions deploy publish --runtime python39 --trigger-http --allow-unauthenticated

$ gcloud functions deploy subscribe --runtime python39 --trigger-topic HELLO_WORLD
```

### Call function

```
$ gcloud functions call publish --data '{"topic":"HELLO_WORLD","message":"Hello World!"}'
```

or using cURL

```
$ curl -w "\n" $(gcloud functions describe publish --format "value(httpsTrigger.url)") -X POST  -d "{\"topic\": \"PUBSUB_TOPIC\", \"message\":\"YOUR_MESSAGE\"}" -H "Content-Type: application/json"
```

#### Check function execution

```
$ gcloud functions logs read subscribe
```

### Delete functions

```
$ gcloud functions delete publish --quiet
```

### Delete Pub/Sub topic

```
$ gcloud pubsub topics delete HELLO_WORLD
```
