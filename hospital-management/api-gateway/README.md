docker build -t hsp/api-service:AN -f dockerfile .

docker run -dit --rm -p 8080:8080 -e DB_HOST=mysql --name api-service --network Hospital-management dnyanyog.org/api-gateway:latest 

mvn docker:build