## Travis CI

hid-sp18-503

status: 70

### Repository Build status 

[![Build Status](images/hid-sp18-503.png)](https://travis-ci.org/seashiva94/hid-sp18-503)

Travis Continuous Integration (Travis CI) is a continuous integration
service that synchronizes with github.  It allows developers to
automate the process of testing an deploying code.  Travis CI allows
users to test code for various different environments and allows the
use of various languages, which can be easily specified by adding a
travis.yml file in the repository.

We demonstrate how to use it in Python. To use Travis CI on github you
need to have a github account and a a travis account. Please go to the
Web sites and creat your account.

* <travis.com>
* <github.com>

To access it within github, you need to allow travis to synchronize
the repositories. To do so please go to the <a href
="https://travis-ci.org/auth?redirectUri=https%3A%2F%2Ftravis-ci.org%2Fauth%3FredirectUri%3Dhttps%253A%252F%252Ftravis-ci.org%252F">
configuration </a>.

Next select the repository that you want to use with Travis CI on the
travis website.  Now go to github and locally clone the repository.

### The .travis.yml file

In the github repository you need to place a `.travis.yml` file.  The
`.travis.yml` file describes to travis, which language is used, what
environments to test the code on, and to install any dependencies that
may be required.

The first line of the `yml` file specifies the language used

```
language: python
```

Next we need to specify the versions of python we need to test the
code for.  Here we need to specify the versions in the same manner as
we use to install the language, as travis creates a virtual
environment for each of these versions.
  
```
python:
  - 3.6.4
```

Dependencies can be specified in the `yml` file under using he
`install:` tag. From our Python section \ref{??} we mentioned that the
use of pip is recommended for python. Thus let us assume we have the
requirements in a requirements.txt file within the git repository.
Hence we can use it in the install tag as follows:

```
install:
  - pip install -r requirements.txt
  ```
  
If tests should be performed for different versions of libraries, this
can also be specified. Let us give an example for different versions
of django. Here we define the versions in the `env:` tag. Hence the
the install is run multiple times but for each environment we set.
  
```
env:
  - django_version=1.10
  - django_version=1.11
install:
  - pip install Django==$django_version
```

To specify what commands to execute to run the tests,
we use the `script:` tag. If a make file is used for this purpose,
this can be done a follows however travis allows the use of pytest for
this purpose as well.

```
script: make test
```

Travis allows various services to be run as required at the time of
testing.  This can be enabled using the ```services``` tag in the
`travis.yml` file. To start a mongodb service for testing your code on
travis add the following to the `travis.yml` file

```
services:
  - mongodb
```
  
To show, and keep track of the build status of the repository, travis
allows users to add build status badges in the markdown file. Once a
test is complete, click on the badge on the travis page, and select
markdown. Then copy the markdown code and add it to the required
markdown file.  On subsequent pushes to the repository, this status
keeps updating.

### An Example
  
\TODO{Arnav: the example is not linked. So we need to make sure that
the example is also copied. I am not sure what the best way of doing
this is, maybe we need a new example directory under the user
cloudmesh such as cloudmesh/travis-example. In any case link to Repo
is missing}

To showcase the use of travis, the `.travis.yml` file in this repository
uses a make file (test_build) to test the swagger code. Swagger auto generates basic
tests that check for correct response codes as specified in the swagger 
specification yml file.
The `.travis.yml` file specifies that mongodb is needed for testing.
The  script tag in `.travis.yml` file invokes the make command which in turn
performs the following steps.

* It dowmloads swagger cli
* It uses the swagger/Makefile to generate the swagger code and install requirements
* It install test requirements provided by swagger
* It uses pytest to perform tests that were generated by swagger
* Finally it cleans the repository.

### Travis and docker

\TODO{Help needed: we need an extension to showcase how to use docker}

### Class examples

A significant example is located at

* <https://github.com/cloudmesh/book/blob/master/.travis.yml>

Here we have published an image to docker hub and use it to verify if
this LaTeX is compiling whenever we check in a change to git. Due to
the big image, this check will take significant amount of time.

The Dockerfile to create the image is located at

* <https://github.com/cloudmesh/book/tree/master/examples/docker/tex>




