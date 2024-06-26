# simple_jenkins

Run 

```bash
docker run `
  --name jenkins-blueocean `
  --restart=on-failure --detach `
  --network jenkins `
  --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client  `
  --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 `
  --publish 50000:50000 custom_jenkins
```

To run agent docker node
```bash
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins --volume /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
```
