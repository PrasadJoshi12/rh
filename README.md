# Solution
  - Use docker run command to create a container `-d` option is used to run container in background.
     ```console
    docker run -d infracloudio/csvserver:latest
    ```
  - Check the container is runnig or not using following command.
     ```console
    docker ps
    ```
  - Check container logs using `docker logs container_id`
    ```console
    docker logs ed1
    2021/03/12 06:33:02 error while reading the file "/csvserver/inputdata": open /csvserver/inputdata: no such file or directory
    ```
  - Create a `gencsv.sh` file.
    ```console
    vi gencsv.sh
	```
> **NOTE**: gencsv.sh file is provided in solution directory

  - Run the script `gencsv.sh`
    ```console
    chmod +x gencsv.sh
    ./gencsv.sh
	  ```
  - It will create a file name called as `inputFile` which we need to provide in container at path `/csvserver`
  - Run the docker in detach mode:
    ```console
    docker run -d -v /root/inputFile:/csvserver/inputdata infracloudio/csvserver:latest
    ```
  - Remove running container using command `docker rm -f container_id`
  - Use `docker inspect` to check the port exposed in container
    ```console
    docker inspect container_id
    ```
  - To set environment variable use `-e` and `-p` is use to forward port.
    ```console
    docker run -d -p 9393:9300 -v /root/inputFile:/csvserver/inputdata -e CSVSERVER_BORDER=Orange infracloudio/csvserver:latest
    ```
