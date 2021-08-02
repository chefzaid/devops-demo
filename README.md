# devops-demo
Simple exercise for basic DevOps infrastructure (Docker, Kubernetes, Kafka)

* One frontend (HTML)
  * A text input and a submit button
  
* Three microservices (Java 11 + Spring Boot)
  *	A: receives the input from the frontend => Checks if it validates a defined regex (e.g. 3 letters followed by 4 numbers)
  *	B: saves data to the database
  *	C: displays data from the database

* The database will be PostgreSQL

B will need to be notified when A validates the input. C is standalone. Thus, we need an events pipeline (Kafka).

Once everything is done, a Docker file needs to be created. It takes a basic Ubuntu image with a JVM, puts in the fatjar and launch it

* On commit a Gitlab CI pipeline needs to compile the JAR, build the Docker image push it to the Registry
* Kubernetes will need to take this image and deploy the pods
  * 6 pods: 1 for the frontend, 3 for each microservice, 1 for the database, 1 for Kafka.
  * Create a volume for the database, it needs to be persistent, regardless of the image/pod destruction
  * You’ll need to manage the ports and the reverse proxy / API gateway through Ingress

Afterwards we will have other pods, for ElasticStack to manage the logs of all the microservices, and for Grafana for monitoring.
