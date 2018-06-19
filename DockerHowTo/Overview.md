**DOCKER**
  * **What are containers**?

    Containerization uses the kernel on the host operating system to run multiple root file systems. Each root file system is called a container. A Container is a standard unit in which an application resides. A container packages an application and everything it needs to run into one portable unit. Each container has its own: processes, memory, devices and network stack. Containers are managed by the Docker engine. The Docker Engine is responsible for creating and managing containers and can run in any physical, virtual or cloud environment. You can read about internals of docker here - [http://docker-saigon.github.io/post/Docker-Internals](http://docker-saigon.github.io/post/Docker-Internals/). For a more usage focussed guide see here - 
    [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/).
  * **Why run your services as containers?**

    Containers provide an isolated environment and also package all the dependencies into a single image which is useful in recreating the same service wherever we want it to run. The image files (Dockerfile in docker containers) provide a declarative approach for service creation and running which means the running and maitainance of services are automated to the full extent.   
    Some of the other advantages are :  
    * Fast provisioning - Run many copies of the service with a single command
    * Lightweight etc..
  * **How to package your services as containers?**  
  Lets see how we can run CoreNLP service in a container and deploy it ro run through docker. 
    
    * Create your app / service.  
      Here we don't have do anything except download the corenlp jar and extract it on our file system.
      ```
      wget http://nlp.stanford.edu/software/stanford-corenlp-full-2017-06-09.zip
      unzip stanford-corenlp-full-2017-06-09.zip
      ```
    * Create a Dockerfile  
      ```
      FROM java:8
      ADD . stanford-corenlp-full-2017-06-09
      WORKDIR stanford-corenlp-full-2017-06-09

      RUN export CLASSPATH="`find . -name '*.jar'`"

      EXPOSE 9000

      CMD java -cp "*" -mx4g edu.stanford.nlp.pipeline.StanfordCoreNLPServer
      ```  
    * Build the image
      ```  
      $ ls
      Dockerfile		stanford-corenlp-full-2017-06-09
      ```
      ```
      $ docker build -t corenlp-server .
      $ docker images
      corenlp-server                                           latest              008e41b0ddc7               3.01 GB
      ```  
    * Run the image through docker
      ```
        docker run -p 9000:9000 corenlp-server
      ```  
      Now if you visit *http://<server_ip>:9000*, you should see CoreNLP running. 




      We saw how we can build an image for a service, push it to local repo and run on any machine using docker. In the document on [Kubernetes](K8S.md), we'll see how to run services on kubernetes, scale them to mutliple instances, load balance them across multiple instances and expose them to other applications.





