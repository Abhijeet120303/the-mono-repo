 docker build -t hsp/patient-service:AN -f dockerfile .

 docker run -dit --rm -e DB_HOST=mysql --name patient-service --network Hospital-management dnyanyog.org/patient-service:latest  

 mvn docker:build