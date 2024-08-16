docker build -t hsp/appointment-service:AN -f dockerfile .

docker run -it --rm -e DB_HOST=mysql --name appointment-service --network Hospital-management dnyanyog.org/appointment-service:latest

mvn docker:build