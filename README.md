# kubemesh
 kubemesh is a library of kubernetes manifests for building out a self contained `datamesh` on any environment

 # why?
[![datamesh](https://img.shields.io/badge/datamesh-data%20decentralisation-darkgreen)](https://www.thoughtworks.com/what-we-do/data-and-ai/data-mesh)

The tl;dr on `data mesh` is that data analysis should be decentralised and managed+operated by functional teams that intimately know and consume the source data.

Most of the modern data analysis platforms force you to pick an underlying processing engine; and if you want to operate a `datamesh` you can "decentralise" on that engine. So what if you come across a workload that does not perform well on the chosen platform?

That's where `kubernetes` comes in by letting you pick whatever engine you want for the analytic workload. 

## Tested On
![k3s](https://img.shields.io/badge/kubernetes-v1.22.3%2Bk3s1-blue)

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

If you think this is a terrible idea, please also open an issue and tell me why I'm an idiot.

## Usage
<a href="./LICENSE"><img
       src="https://img.shields.io/badge/LICENSE-WTFPL-black"
       alt="WTFPL" /></a>
