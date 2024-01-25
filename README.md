# nifi_listener
A pipeline for Nifi, which listens for requests and distributes them to the necessary folders in the Yandex storage (S3) bucket based on their content (if it contains or does not contain the text "ERROR").

The following requests were used for testing:
curl --data "adbrsgbndt ERROR fevrtb" 127.0.0.1:8081/loglistener
curl --data "uiebveovne" 127.0.0.1:8081/loglistener

Docker was used for implementation with the following parameters:
docker run --name nifi -p 9090:9090 -p 8081:8081 -d -e NIFI_WEB_HTTP_PORT='9090' apache/nifi:latest

To implement this, a service account with storage.admin permissions, key ID, and secret key were required.

Also, to connect to Yandex storage using the PutS3Object processor, it was necessary to assign a context with the parameter "region" set to "ru-central1" for the flow and use it in the "Region" parameter.
