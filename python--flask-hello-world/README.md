# Flask Hello World

This project is intended to be a starting point for a basic Hello World Python Flask application
that I repeatedly revisit for many proof of concept projects.

## Prerequisites

Install easy_install, pip and virtualenv. Then, clone this repository and navigate to this example:

```bash
$ git clone https://<git_location>/scriptbox.git
$ cd scriptbox/python--flask-hello-world
```

Install the required environment and libraries:

```bash
$ virtualenv --no-site-packages --distribute .env
$ source .env/bin/activate
$ pip install -r requirements.txt
```

## Testing

You can test the application by running the PyTest Unit test suite (which is what a CI pipeline
in Jenkins or some other CI tool would use):

```bash
$ python -m pytest tests/test_app.py
```

## Usage

To start the Flask application, simply run the `run.py` script:

```bash
$ python run.py
```

You can now open a browser and navigate to http://<SERVER_IP>:8000/ to see the Hello World Flask
basic website.

## Kubernetes

There are Kubernetes YAML configuration files and a Docker file in this directory due to
this repo being used as part of a larger tutorial on Kubernetes. Those files can be found in the
`k8s/` directory.

## Jenkins

This mini-project can also be used as a starter project for a Jenkins pipeline. There is a file
in the `jenkins/` directory named `Jenkinsfile` that can serve as the pipeline definition. To
configure this repository to be set up as a Pipeline within Jenkins (as of Jenkins 2), simply
create a Pipeline project in Jenkins and under the "Pipeline" configuration, specify the
following parameters:

- **Definition**: Pipeline script from SCM
- **SCM**: Git
- **Repositories -> Repository URL**: https://github.com/jekhokie/scriptbox.git
- **Repositories -> Credentials**: none
- **Branches to build -> Branch Specifier (blank for 'any')**: \*/master
- **Repository Browser**: (Auto)
- **Additional Behaviors**: (None/Leave Default)
- **Script Path**: python--flask-hello-world/jenkins/Jenkinsfile
- **Lightweight checkout**: (checked)

In addition, if you wish to have any new checkins into the project automatically trigger a build,
you can specify the following:

- **GitHub project**: (checked)
- **GitHub project -> Project url**: https://github.com/jekhokie/scriptbox.git/
- **Poll SCM**: (checked)
- **Poll SCM -> Schedule**:  \* \* \* \* \*

**Note**: The "Poll SCM -> Schedule" setting above will trigger Jenkins to inspect for any new commits
every minute.

Once you configure the above settings, press "Save" and kick off a build. Jenkins should use the
Jenkinsfile within the project to kick off the build steps. You can also optionally create a commit
and push to master for this repository, and the next minute Jenkins checks for changes it will also
automatically trigger a build.
