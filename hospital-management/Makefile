.PHONY: all

DIRS = api-gateway appointment-service patient-service directory-service case-service 
LIB_PROJECT = hospital-management-console
REPO_URL = https://github.com/Abhijeet120303/the-mono-repo.git

# Default target
all:  git_status git_pull git_stash build_services build_lib build_images push_images

git_clone:
	@echo "Cloning all services and JavaFX project with lib..."
	git clone $(REPO_URL)

git_status:
	@echo "git status of all services.........."
	git status
	
git_pull:
	@echo "git pull............"
	git pull

git_stash:
	@echo "git stash.........."
	git stash

build_services:
	@for dir in $(DIRS); do \
		echo "Building $$dir..."; \
		cd $$dir && mvn clean install -Dmaven.test.skip=true && cd ..; \
	done

build_lib:
	cd $(LIB_PROJECT) && mvn clean install -Dmaven.test.skip=true

build_images:
	@for dir in $(DIRS); do \
		echo "Building Docker image for $$dir..."; \
		cd $$dir && mvn docker:build -Dmaven.test.skip=true -Dimage.registry=abhijeetnirphal && cd ..; \
	done

run_all:
	@for dir in $(DIRS); do \
		echo "Running $$dir..."; \
		docker run -dit --rm -e DB_HOST=mysql --network Hospital-management --name $$dir abhijeetnirphal/$$dir:latest; \
	done

push_images:
	@for dir in $(DIRS); do \
		echo "Pushing Docker image for $$dir..."; \
		cd $$dir && docker push abhijeetnirphal/$$dir:latest && cd ..; \
	done

sonar_scan:
	@for dir in $(DIRS); do \
		echo "************************************* Scanning $$dir..."; \
		cd $$dir && mvn clean verify sonar:sonar -Dsonar.projectKey=$$dir -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqa_1f0d85486497d35e2938cd00a16dcf598f8c25fb -Dmaven.test.skip=true && cd ..; \
	done

license_scan:
	@for dir in $(DIRS); do \
		echo "************************************* Scanning $$dir..."; \
		cd $$dir && docker run -it --rm -v "$${PWD}":/scan dnyanyog.org/license_finder:latest && cd ..; \
	done
