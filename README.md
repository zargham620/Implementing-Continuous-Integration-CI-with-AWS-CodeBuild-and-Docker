# **Implementing Continuous Integration (CI) with AWS CodeBuild, CodePipeline, and Docker**  

This project demonstrates a complete CI/CD pipeline implementation using AWS CodeBuild, CodePipeline, and Docker for a Node.js application. The pipeline automatically builds and deploys a containerized Node.js application to Amazon ECR.  

## **Project Overview**  
The project sets up an automated CI/CD pipeline that:  

- Builds a Docker container for a Node.js application  
- Pushes the container to Amazon ECR  
- Implements continuous integration using AWS CodeBuild  
- Manages the pipeline with AWS CodePipeline  

## **Prerequisites**  
- AWS Account with appropriate permissions  
- Docker installed locally for testing  
- Node.js 14 or later  
- AWS CLI configured with appropriate credentials  
- Access to AWS ECR, CodeBuild, and CodePipeline services  

## **Project Structure**  
```
.
├── app.js                 # Main Node.js application file
├── Dockerfile             # Docker configuration for containerization
├── buildspec.yml          # AWS CodeBuild specification file
├── package.json           # Node.js project configuration
└── README.md              # This file
```

## **Component Details**  

### **Node.js Application**  
A simple Node.js application that logs `"docker zargham"` to demonstrate the pipeline functionality.  

### **Docker Configuration**  
The `Dockerfile` sets up a Node.js 14 environment and exposes port 8080:  

- Uses `node:14` as the base image  
- Sets up the working directory in `/var/src/app`  
- Installs dependencies  
- Copies application code  
- Exposes port 8080  
- Runs the application  

### **AWS CodeBuild Configuration**  
The `buildspec.yml` file defines the build process:  

- **Pre-build phase**: Logs into Amazon ECR  
- **Build phase**: Builds and tags the Docker image  
- **Post-build phase**: Pushes the image to ECR and creates deployment artifacts  

## **Setup Instructions**  

1. **Clone this repository** to your local machine  

2. **Configure AWS Services:**  
   ```sh
   aws configure
   ```

3. **Create an ECR repository:**  
   ```sh
   aws ecr create-repository --repository-name zar_repo --region us-east-1
   ```

4. **Update the `buildspec.yml`** with your ECR repository URI  

5. **Set up AWS CodeBuild:**  
   - Create a new build project  
   - Use the provided `buildspec.yml`  
   - Configure appropriate IAM roles and permissions  

6. **Configure AWS CodePipeline:**  
   - Create a new pipeline  
   - Connect to your source repository  
   - Add CodeBuild as a build stage  
   - Configure deployment stages as needed  

## **Local Testing**  

1. **Install dependencies:**  
   ```sh
   npm install
   ```

2. **Build the Docker image locally:**  
   ```sh
   docker build -t my-node-app .
   ```

3. **Run the container:**  
   ```sh
   docker run -p 8080:8080 my-node-app
   ```

## **Pipeline Workflow**  
1. Code changes are pushed to the repository  
2. AWS CodePipeline detects changes and triggers the pipeline  
3. CodeBuild builds the Docker image using `buildspec.yml`  
4. The image is pushed to ECR  
5. The application is ready for deployment  

## **Security Considerations**  
- Ensure proper IAM roles and permissions are configured  
- Keep AWS credentials secure  
- Regularly update dependencies  
- Follow AWS security best practices  

## **License**  
This project is licensed under the **MIT License**.  

## **Contributing**  
Feel free to submit issues and pull requests.
