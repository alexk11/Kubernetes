1. Gradle
 ./gradlew clean build

2. Docker
 docker build -t snowflake-nextid:1.0 .
 docker run -p 8084:8080 snowflake-nextid:1.0

PS C:\> kubectl logs -f snowflake-nextid
   kubectl port-forward snowflake-nextid 8082:8080

PS C:\> Remove-item alias:curl
PS C:\> curl -X GET http://localhost:8082/next-id   =>  7427738124698128384
