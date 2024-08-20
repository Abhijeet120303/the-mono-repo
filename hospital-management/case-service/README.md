docker build -t hsp/case-service:AN -f dockerfile .

docker run -dit --rm -e DB_HOST=mysql --name case-service --network Hospital-management dnyanyog.org/case-service:latest

mvn docker:build 
