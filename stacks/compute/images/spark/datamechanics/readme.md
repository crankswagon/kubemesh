just use this https://hub.docker.com/r/datamechanics/spark

```
docker build -t datamechanics-3.2.1 ./images/datamechanics

#push it to our private repo (which kubernetes has access to)
docker image tag datamechanics-3.2.1 registry.derp.work/datamechanics-spark:3.2.1
docker image push registry.derp.work/datamechanics-spark:3.2.1

```