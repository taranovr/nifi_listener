# nifi_listener
Pipeline в nifi, который слушает запросы и раскладывает их по необходимым (если содержит и не содержит текст "ERROR") папкам в бакете  yandex storage (s3)

Для тестов использовались следующие запросы:
curl --data "adbrsgbndt ERROR fevrtb" 127.0.0.1:8081/loglistener 
curl --data "uiebveovne" 127.0.0.1:8081/loglistener



Для реализации использовался docker со следующими параметрами: 
docker run --name nifi -p 9090:9090 -p 8081:8081 -d -e NIFI_WEB_HTTP_PORT='9090' apache/nifi:latest

Для реализации понадобился сервисный аккаунт с правами storage.admin, идентификатор ключа и секретный ключ.

Также для подключения к yandex storage с помощью процессора PutS3Object необходимо было присвоить контекст с параметром region "ru-central1" для flow, и использовать его в параметре "Region"
