1. Gradle
 ./gradlew clean build

2. Docker
 docker build -t snowflake-nextid:1.0 .
 docker run -p 8084:8080 snowflake-nextid:1.0

PS C:\> kubectl logs -f snowflake-nextid
   kubectl port-forward snowflake-nextid 8082:8080

 kubectl apply -f app-pod.yml
 kubectl apply -f app-deployment.yml

PS C:\> Remove-item alias:curl
PS C:\> curl -X GET http://localhost:8082/next-id   =>  7427738124698128384

Generate TLS certs:
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 365
openssl req -x509 -newkey rsa:4096 -keyout tls.crt -nodes -out tls.crt -sha256 -days 365

cat tls.crt | base64 -w 0
cat tls.key | base64 -w 0
