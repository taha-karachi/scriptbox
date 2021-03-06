# Web Service Simulator

This project is a Python Flask web server instance that intends to simulate a service that functions
by receiving web requests, processes them, and sends the message to another downstream consumer. It is
a building block that can be used to simulate a distributed services architecture that utilizes HTTP
as its communication mechanism.

## Background

When creating an environment of distributed services, it is often times helpful to be able to simulate
various scenarios related to communication between services. This project is intended to support just
that - it is a building block that provides some VERY basic boiler-plate code to start a web server instance
on a specific port and having a specific path to POST items to.

Upon receiving a POST request, the web server logs the incoming request event. It then injects a
random/artificial delay to simulate processing, and will log the event corresponding to sending the message
to the next/downstream consumer.

Note that this project can also be configured as the first/last web service processor in a pipeline.
This allows both the ability to inject data as well as terminate the data flow for a particular
architectural setup to simulate real-world type of activity related to web requests.

The following diagram details how one may set up a web processing pipeline:

```
--------------        --------------        --------------        --------------
|            |        | Processor  |        | Processor  |        |            |
|  Injector  |  --->  | Stage #1   |  --->  | Stage #2   |  --->  | Terminator |
|            |        |            |        |            |        |            |
--------------        --------------        --------------        --------------
```

## Prerequisites

Install easy_install, pip and virtualenv. Then, clone this repository and navigate to this example:

```bash
$ git clone https://<git_location>/scriptbox.git
$ cd scriptbox/python--web-service-simulator
```

Install the required environment and libraries:

```bash
$ virtualenv --no-site-packages --distribute .env
$ source .env/bin/activate
$ export CC=/usr/bin/gcc     # set this to wherever your C-compiler is located
$ pip install -r requirements.txt
```

Create a configuration file from the sample and specify the values for your specific environment.

```bash
$ cp instance/config.py.sample instance/config.py
# edit the instance/config.py file for your environment
```

## Usage

Now that the configurations are in place, run the script to start the web service.
Note that you can use CTRL-C to terminate the instance.

```bash
$ python run.py
# you should see output corresponding to the request/response sequence
```
