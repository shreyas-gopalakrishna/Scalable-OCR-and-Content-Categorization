## Scalable Service for Character Recognition and Content Categorization

CSCI 5253 - Data Center Scale Computing - Project

#### Project URL
https://github.com/shreyas-gopalakrishna/Scalable-OCR-and-Content-Categorization
https://www.youtube.com/watch?v=cWYq_U782eU&t

#### Project Goals
Character recognition - A web service takes images of documents or notes, performs OCR (Optical character recognition) on them and stores the input image and the converted text.

Content classification - The contents of documents are analyzed with keywords to classify them into specific topics. Users can view documents based on the categories.

Search based on Keywords - A search feature to search a word across all uploaded documents
Scalable service - The service is designed to scale to accommodate increased workloads as multiple users try to access the service.


#### Components
Kubernetes

Google Vision API

Google Natural Language API

Google Cloud Storage (Bucket)

Redis

REST Server

CloudSQL

RabbitMQ

### Architecture diagram
![](https://github.com/shreyas-gopalakrishna/Scalable-OCR-and-Content-Categorization/blob/master/images/Architecture.png)

### Steps to Run code
1. `gcloud container clusters create mykube` creates a kubernetes cluster.
2. `sh redis-launch.sh` creates docker image of redis, pushes it to kubernetes, and exposes port.
3. `sh rabbitmq-launch.sh` creates docker image of rabbitmq, pushes it to kubernetes, and exposes port.
4. `sh cloudsql-create.sh` creates cloud sql instance and sets the permissions and password.
5. `sh rest-launch.sh` creates docker image with flask and other modules installed, pushes it to kubernetes, and exposes 5000 port for REST API.
6. `sh worker-launch.sh` creates docker image for worker with required modules installed, pushes it to kubernetes and waits for messages from rabbitmq.
7. `sh logs-launch.sh` creates docker image for logswith required modules installed, pushes it to kubernetes and waits for debug messages from rest and worker.
8. `sh frontend-launch.sh` creates docker image of httpd,adds the frontend code base, pushes it to kubernetes, and exposes port 80 for website access.

##### Note
DCSC.json is the GOOGLE_APPLICATION_CREDENTIALS file. It is not included in the repository.

A custom service credentials json from must be generated and used to run the project.

### Snapshots from Project

![](https://github.com/shreyas-gopalakrishna/Scalable-OCR-and-Content-Categorization/blob/master/images/1.png)<br/>
*Scalable pods in Google cloud* <br/>
<br/>
![](https://github.com/shreyas-gopalakrishna/Scalable-OCR-and-Content-Categorization/blob/master/images/2.png)<br/>
*Text recognition in uploaded image* <br/>
<br/>
![](https://github.com/shreyas-gopalakrishna/Scalable-OCR-and-Content-Categorization/blob/master/images/3.png)<br/>
*Content categorization of text found in the image* <br/>
<br/>
![](https://github.com/shreyas-gopalakrishna/Scalable-OCR-and-Content-Categorization/blob/master/images/4.png)<br/>
*All uploaded documents* <br/>
<br/>
![](https://github.com/shreyas-gopalakrishna/Scalable-OCR-and-Content-Categorization/blob/master/images/5.png)<br/>
*Search query across all uploaded images* <br/>
<br/>

##### UI Template Credits
https://github.com/ColorlibHQ/AdminLTE/releases/tag/v2.4.18



#### Sources
https://cloud.google.com/vision/docs/ocr

https://cloud.google.com/vision/docs/auth

https://medium.com/@jdegange85/document-image-datasets-b7f8df01010d

https://cloud.google.com/natural-language/docs/classify-text-tutorial
