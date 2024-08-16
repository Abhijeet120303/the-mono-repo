docker build -t hsp/directory-service:AN -f dockerfile .

docker run -dit --rm -e DB_HOST=mysql --name directory-service --network Hospital-management dnyanyog.org/directory-service:latest

docker run -dit --rm --network Hospital-management -v mysql-data:/var/lib/mysql --name mysql hsp-mysql:latest

mvn docker:build

docker run -it --rm --name sonarqube -p 9000:9000 sonarqube:latest

mvn clean verify sonar:sonar -Dmaven.test.skip=true -Dsonar.projectKey=directory-service -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqa_59b8a2448e6908c94798713b951682876b23296b

# trivy-scan
docker run -it --rm  -v /var/run/docker.sock:/var/run/docker.sock -v trivy-cache:/root/.cache/  aquasec/trivy image dnyanyog.org/api-gateway:latest


# grype-scan
docker run --rm  --volume /var/run/docker.sock:/var/run/docker.sock --name Grype anchore/grype:latest $(ImageName):$(ImageTag)

docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock --name Grype anchore/grype:latest dnyanyog.org/appointment-service:latest

docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock -v grype-cache:/.cache/ --name Grype anchore/grype:latest dnyanyog.org/directory-service