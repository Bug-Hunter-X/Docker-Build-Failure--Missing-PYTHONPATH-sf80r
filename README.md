# Docker Build Failure: Missing PYTHONPATH
This repository demonstrates a common Dockerfile error related to missing environment variables, specifically PYTHONPATH, and its solution.

## Bug
The initial Dockerfile (Dockerfile) attempts to run a Python application that depends on modules located in a subdirectory. Because PYTHONPATH is not set, the application fails to find and import those modules, causing the build to succeed but the container to fail when trying to execute the application. 

## Solution
The fixed Dockerfile (Dockerfile_fixed) addresses this by setting the PYTHONPATH environment variable to include the directory containing the application's modules. This allows Python to successfully locate and import the needed dependencies. 

## Setup and Running
1. Clone this repository.
2. Build the bugged image using: `docker build -t bugged-app -f Dockerfile .`
3. Try to run it using `docker run bugged-app` (it will fail)
4. Build the fixed image using: `docker build -t fixed-app -f Dockerfile_fixed .`
5. Try to run it using `docker run fixed-app` (it will work)

## Lessons Learned
- Always ensure necessary environment variables are set within your Dockerfile, especially when dealing with paths for your app. 
- Carefully review import statements in your code to make sure they're correctly accessing your modules within the docker environment. 
- Use a multi-stage build to reduce image size if the application dependencies are significant.