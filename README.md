# create repo (generate key)

# login to dockerhub
# github secrets

# create .github/workflows/build.yaml

name: CI/CD Pipeline 
 
on: 
  push: 
    branches: 
      - master 
 
jobs: 
  build: 
    runs-on: ubuntu-latest 
 
    steps: 
    - name: Checkout code 
      uses: actions/checkout@v2 
 
    - name: Set up Docker Buildx 
      uses: docker/setup-buildx-action@v2 
 
    - name: Log in to Docker Hub 
      uses: docker/login-action@v2 
      with: 
        username: ${{ secrets.DOCKER_USERNAME }} 
        password: ${{ secrets.DOCKER_PASSWORD }} 
 
    - name: Build and push Docker image 
      uses: docker/build-push-action@v5 
      with: 
        context: . 
        push: true 
        tags: ufonalim/webapp:latest


# create branch and push

===================================

# sudo apt-get update
# sudo apt-get install -y docker.io
# sudo systemctl start docker
# sudo systemctl enable docker
# docker login
# docker pull
# docker run -d -p 111:111 image:tag

=================================

# https://cloud.google.com/run/docs/quickstarts/build-and-deploy/deploy-dotnet-service

=================================
  # Deploy Docker image to remote VM

# ssh-keygen -t rsa -b 4096
# 
      - name: Deploy to Remote VM via SSH
        uses: appleboy/ssh-action@v0.1.7
        with:
          host: ${{ secrets.VM_IP }}
          username: ${{ secrets.VM_USER }}
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          port: 22
          script: |
            # Pull the latest image from Docker Hub
            docker pull yourdockerhubusername/yourimage:latest

            # Stop and remove the old container if it exists
            docker stop yourcontainer || true
            docker rm yourcontainer || true

            # Run the new container
            docker run -d --name yourcontainer -p 80:80 yourdockerhubusername/yourimage:latest