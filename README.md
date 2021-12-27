
# Containerized WebSite

## Motivation

In this laboratory assignment, you are to create a web site on your cit384-${USER} VM.  But this web-site will be delivered via a containerized web server.


## Precursory Steps
Complete the following steps to validate that both your local computer and your VM is working correctly. These steps will also help you to re-familize yourself with common docker commands.

   
   1. Run the docker hello-world example.
      ```
      docker run --name inclass hello-world
      ```
   
   1. Copy the CIT160 dockerfile from the sandbox server.
      ```
      scp ssh.sandbox.csun.edu:~steve/cit160/etc/dockerfile .
      ```
   
   1. Modify the CIT160 docker file to include the line:
      ```
      COPY dockerfile /tmp
      ```
   
   1. Run (Build, Create, Start, and Exec) the command to display the contents of the /tmp/dockerfile.
      ```
      docker build -t bash_image .
      docker create --name bash_container --interactive --tty bash_image
      docker start bash_container
      docker exec -it bash_container cat /tmp/dockerfile
      ```

## Assignment Steps:
   1. Copy your resume and other artifacts into your new repository.

   2. Create a dockerfile to be used to create you new website within a container. See the Starter Dockerfile below. This container needs to include:
      - the Apache httpd server
      - your index.html file and other artifacts associated with your resume

   3. Add, Commit, and Push your updates to the server

   4. Run the appropriate docker commands on your desktop to validate everything is working correctly
      ```
      docker build -t my_resume git@github.com:smf-steve/<blah>.git
      docker run -dit --name resume.site -p 8080:80 my_resume
      ```

   5. Use the curl command to test your website:
      * curl http://localhost:8080/

   6. Using your browser, enter the following URL:
      * http://localhost:8080/

   7. Log into your cit384-${USER}, VM and redo Steps #5 & #6

   8. Ponder how you can use your local browser to access your website on your VM.
      1. Use the VPN
      2. For inquiring minds, checkout the process to create a tunnel using SSH.

## Enhancements:
  1. Add SSL/HTTPS support


## Starter Dockerfile
```

# Obtain a starting image for the Apache Web Server
FROM httpd

# Set the working directory to match DocumentRoot                                   
WORKDIR /usr/local/apache2/htdocs

# Copy your index.html file to DocumentRoot directory               
COPY index.html .                               

# Add in other directives as needed
# LABEL maintainer:"Steven.Fitzgerald@csun.edu"
# RUN
# EXEC
```


# Resources:
1. https://docs.docker.com/reference/
2. https://docs.docker.com/engine/reference/builder/
3. https://hub.docker.com/_/httpd
