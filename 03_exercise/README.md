# Packages (Docker)

We will work today your Github repository. The repository with Python code, you have created last time:

```text
|- .github/workflows
|- hello_world/
|- test/
|- main.py
|- Makefile
|- README.md
|- requirements.txt
\- test_requirements.txt
```

## Preparation

1. Check whether the application works locally following the steps from the project `README.md`.

   ```bash
   make test
   make lint
   make run
   ```

   ```bash
   curl 127.0.0.1:5000/
   ```

2. Please verify your github flow works.

## Packaging

1. What is the dependency hell?

2. What are different approaches to address it?

   - How does Python or NodeJS solve it?
   - Linux distributions, e.g., deb or rpm? What is `snap` and what the difference is?
   - How did we address it on the cloud?
   - What did Docker bring to the table?

3. Add to your project `Dockerfile`:

   ```dockerfile
   FROM python:3

   ARG APP_DIR=/usr/src/hello_world_printer

   WORKDIR /tmp
   ADD requirements.txt /tmp/requirements.txt
   RUN pip install -r /tmp/requirements.txt

   RUN mkdir -p $APP_DIR
   ADD hello_world/ $APP_DIR/hello_world/
   ADD main.py $APP_DIR

   WORKDIR $APP_DIR
   CMD FLASK_APP=hello_world flask run --host=0.0.0.0
   ```  

4. Let's see whether we can build the docker image for our app:

   ```bash
   sudo docker build -t hello-world-printer .
   ```

   ```bash
   # please verify whether you can see your image
   sudo docker images 
   ```

   Notice: if your application is simple, you can verify whether it starts during the building phase. Just change `CMD` to `RUN` for testing

5. If it works, please add a dedicated target in your `Makefile`:

   ```makefile
   docker_build:
   	docker build -t hello-world-printer .
   ```

   and test it. 

6. Docker provides us commands to run the application with one command:

   ```bash
   sudo docker run \
       --name hello-world-printer-dev \
       -p 5000:5000 \
       -d hello-world-printer
   ````

7. To check whether it runs properly:

   ```bash
   # does it run?
   sudo docker ps

   # if you do not see your docker running:
   docker ps -a
   ```

   ```bash
   # does it respond?
   curl 127.0.0.1:5000/
   ```

   ```bash
   # what the logs say
   sudo docker logs hello-world-printer-dev
   ```

8. We might need to check the Docker from within: 

   ```bash
   sudo docker exec -it hello-world-printer-dev /bin/bash


     root@b7:/usr/src/hello_world_printer# 
   ```

9. Time to add another target to our `Makefile`:

   ```makefile
   docker_run: docker_build
   	docker run \
   		--name hello-world-printer-dev \
   		-p 5000:5000 \
   		-d hello-world-printer
   ```

10. How to restart a Docker:

    ```bash
    sudo docker stop hello-world-printer-dev 
    sudo docker rm hello-world-printer-dev
    sudo make docker_run
    ```

11. The next step is to build your package (in our scenario a Docker Image) as a part of your CI/CD process (see [docs](https://github.com/marketplace/actions/build-and-push-docker-images)). Please add at the end of your workflow file:

    ```yaml
      # ...
       - name: Set up QEMU
         uses: docker/setup-qemu-action@v1
       - name: Set up Docker Buildx
         uses: docker/setup-buildx-action@v1
       - name: Build and export to Docker
         uses: docker/build-push-action@v2
         with:
           context: .
           load: true
    ```

12. We should also publish our Docker Image to a repository. `hub.docker.com` is the most popular one:

    1. Create an account on hub.docker.com.
    2. Following the example from [docs](https://github.com/marketplace/actions/build-and-push-docker-images) publish your image.

<!--
13. Package and software versioning, read http://semver.org/ 

1. Zapoznaj się z opisem i napisz w swoich słowach co to jest Semantic Versioning:
Dlaczego MAY i MUST są z dużej litery?

Co to jest RFC 2119?

Opisz każde z pól następującej wersji:
1.0.1
1.3.2-1
1.4.5+1

2. Co to jest Calver (https://calver.org/)?
-->

## Advanced topics

- Run your Docker and mount the source code from your workstation to the Docker, so you can faster iterate. No need to rebuild your image, you can just restart the Docker:

  ```bash
  sudo docker run \
       --name hello-world-printer-dev \
       -v $(pwd):/usr/src/hello_world_printer/
       -p 5000:5000 \
       -d hello-world-printer
  ```

- Does my Dockerfile follow [best practices](https://github.com/wojciech12/workshop_kubernetes_and_cloudnative/tree/master/00_docker)? We have a linter for that:

  ```bash
  docker run --rm -i hadolint/hadolint < Dockerfile

  # search & lint!
  find . -iname Dockerfile | xargs -I {} bash -c "echo {}; docker run --rm -i hadolint/hadolint < {}"
  ```

- Security? Does the Docker image contain outdated packages? I recommend [trivy](https://hub.docker.com/r/aquasec/trivy).

  ```bash
  trivy image hello-world-printer
  ```

### Ideas for Python Practice

1. Add XML output for your hello printer app.

2. Let the client, provide her or his name as a GET argument:

   ```bash
   curl '127.0.0.1:5000?name=apolonia&output=json'
   ```

   add relevant tests.

3. Generate JSON output with the built-in json library (do not forget about the tests):

   ```python
   import json
   ```

4. Generate XML output with lxml (do not forget about the tests):

   ```bash
   pip3 install lxml
   ```

   Hint: see this post on [stackoverflow](https://stackoverflow.com/a/4470035).

5. Execute the flask app with [gunicorn](https://gunicorn.org/).
