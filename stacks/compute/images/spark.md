# Spark
[![datamechanics](https://img.shields.io/badge/datamechanics-spark-lightblue)](https://www.datamechanics.co/)

To get `spark` up and running, we don't need to reinvint the wheel, `datamechanics.io` is an operator of `spark` on `kubernetes` and have lots of [images available](https://hub.docker.com/r/datamechanics/spark) for use.


We can use that as the starting point to get our cluster running


## Packing the base image
this is the image with dependencies that our spark nodes need
we will reference this within the notebook when we create the `spark context`
```bash
docker build -t datamechanics-spark3.2.1-java11:0.0.7 ./images/spark/node

#push it to our private repo (which kubernetes has access to)
docker image tag datamechanics-3.2.1 registry.derp.work/datamechanics-spark3.2.1-java11:0.0.7
docker image push registry.derp.work/datamechanics-spark3.2.1-java11:0.0.7
```


## Packing the notebook image
the notebook image is essentially the driver, we can just build on top of the node image
this image is then referenced in the [notebook manifest](stacks/compute/spark/1_notebook_mode.yaml)

```bash
docker build -t datamechanics-spark3.2.1-java11-jupiter:0.0.7 ./images/spark/driver

docker image tag datamechanics-spark3.2.1-java11-jupiter:0.0.7 registry.derp.work/datamechanics-spark3.2.1-java11-jupiter:0.0.7

docker image push registry.derp.work/datamechanics-spark3.2.1-java11-jupiter:0.0.7
```