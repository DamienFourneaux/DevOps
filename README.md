# DevOps
Repository for the DevOps project

Question 1.1 : For which reason is it better to run the container with a flag -e to give the environment variables rather than put them directly in the Dockerfile?

Running the container with a flag -e to pass environment variables is preferable to hardcoding them in the Dockerfile because it keeps sensitive information (such as passwords or API keys) out of the image layers and allows the same image to be reused with different configurations at runtime,improving both security and flexibility.


Question 1.2 : Why do we need a volume to be attached to our postgres container?

Attaching a volume to the Postgres container is necessary because containers are ephemeral by default—any data written inside the container’s filesystem is lost when the container stops or is removed. By mounting a host directory or named volume (for example, -v dbdata:/var/lib/postgresql/data), the database files persist between restarts or recreation of the container so that stored data is not lost.


Question 1.3 : Document your database container essentials: commands and Dockerfile.
See directly the dockerfile


Question 1.4 : Why do we need a multistage build? And explain each step of this dockerfile.

A multistage build reduces the final image size and keeps only what’s needed at runtime: first it uses a full JDK image to compile the code and produce the JAR, then it switches to a minimal JRE image and copies just that JAR, leaving out the compiler, source files, and other build tools.

Question 1.5 : Why do we need a reverse proxy?

A reverse proxy is required to receive client HTTP requests on common ports (such as 80 or 443) and forward them to the appropriate backend service (e.g., different microservices on various internal ports or hosts); it also handles TLS termination, load balancing, and centralizes authentication or rate limiting in front of multiple application containers.


Question 1.6 : Why is docker-compose so important?

Docker Compose is so important because it allows defining and managing multiple interdependent containers in a single YAML file (for example, web, database, cache), making it easy to start, stop, and scale the entire application stack with simple commands rather than manually running each container and configuring their networking and volumes by hand.


Question 1.7 : Document docker-compose most important commands.

docker-compose build: Builds all services defined in the docker-compose.yml file.
docker-compose up -d: Starts all services in detached mode, creating networks, volumes, and containers as needed.
docker-compose down: Stops and removes containers, networks, and optionally volumes created by up.
docker-compose ps: Lists the status of running containers for the current Compose project.


Question 1.8 : Document your docker-compose file.
See on the Docker-compose file directly


Question 1.9 : Document your publication commands and published images in dockerhub.

Login to Docker Hub: docker login
Tag the image: docker tag my-app-image myusername/my-app:latest
Push to Docker Hub: docker push myusername/my-app:latest

I have 4 images on the dockerhub :  Two database image, An http image (simple-api) and A Backend image.

Link to access the images on dockerhub : https://hub.docker.com/u/dfourneaux


Question 1.10 : Why do we put our images into an online repo?

Putting images in an online repository is necessary so that servers or CI/CD pipelines can pull the exact same image over the internet  without rebuilding locally. It enables versioning, collaboration, and automated deployments to any environment with just an internet connection.

-----------------------------------------------------------------------------------------------------------------------------------------------------------

Question 2.1 : What are Testcontainers?

Testcontainers is a Java library that makes it easy to use Docker containers in automated tests. Instead of having to install and configure a real database or message broker on the machine running tests, Testcontainers will start up a fresh Docker container just for the duration of the test. This way, each test can run against a clean, isolated instance of the service, ensuring that tests behave the same way on any developer’s computer or in a CI environment.


Question 2.2 : For what purpose do we need to use secured variables?

Secured variables (sometimes called “secrets” or “protected variables”) let you store sensitive information—like API keys, passwords, or tokens—without putting them directly into your code or workflow files. When a CI/CD pipeline runs, it can access these variables without exposing their values in logs or commit history. This protects credentials from being leaked while still allowing workflows to authenticate or connect to external services.


Question 2.3 : Why did we put needs: build-and-test-backend on this job? Maybe try without this and you will see!

The needs: build-and-test-backend setting creates a dependency: it tells the workflow to wait until the “build-and-test-backend” job finishes successfully before starting this job. If you remove that line, this job might run too early—before the backend code is compiled and tested—and could fail because it depends on the results of the earlier job. In other words, adding needs ensures that the backend is fully built and tested first, so only if those steps pass will the workflow move on to pushing images or any further steps.


Question 2.4 : For what purpose do we need to push Docker images?

Pushing a Docker image to a registry (like Docker Hub or a private registry) makes it easy to share and deploy the application in other environments. Once the image is built and stored in a registry, any server or container platform can pull that exact image without rebuilding it from source. This supports versioning (each image tag corresponds to a specific code version), ensures consistency across different servers, and streamlines continuous delivery and deployment because the same built image is reused rather than rebuilt each time.

-----------------------------------------------------------------------------------------------------------------------------------------------------------

Question 3.1 : Document your inventory and base commands
See in inventories folder in ansible folder


Question 3.2 : Document your playbook
See the playbook in ansible folder

Question 3.3.A : 
See on the roles folder, in each role, there is a README file


Question 3.3.B : Is it really safe to deploy automatically every new image on the hub ? explain. What can I do to make it more secure?

Automatically deploying every new image pushed to Docker Hub can be risky, as one might download and run untested or malicious code. Images could contain vulnerabilities or backdoors that are immediately promoted to production. To secure this process, it would be better to use a trusted or private registry (or require image signing and verification), enable automated vulnerability scanning on each image before deployment, and add a manual approval or testing stage in the CI/CD pipeline so that only vetted tags (for example, after passing security checks and integration tests) are actually deployed to production.