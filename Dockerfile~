# Set base image (host OS)
FROM python:3.9-slim-buster

# Set the working directory in the container
#WORKDIR /new-demo

# Copy the dependencies file to the working directory
COPY requirements.txt ./

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy all the contents to the working directory
COPY . .

# Command to run when container start
#CMD ["python", "-u" , "test.py"]


