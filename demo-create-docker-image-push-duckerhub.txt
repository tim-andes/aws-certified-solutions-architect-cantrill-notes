## DEMO - Creating 'container of cats' Docker Image
Create a docker image containing the 'container of cats' application.
- Prereq: Create a DockerHub account

1. 1 Click Deploy (A.Cantrill lesson).
2. Nav to new EC2 instance > Connect > Session Manager
3. Commands https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0030-aws-associate-ec2docker/lesson_commands.txt
- `sudo amazon-linux-extras install docker` - Install Docker
- `sudo service docker start` - Start Docker
- `docker ps` - Test Docker. Expect a permissions error
- `sudo usermod -a -G docker ec2-user` - Add permissions
- `exit` and reopen a Session Manager
- `sudo su - ec2-user` - Log in as EC2 user
- `docker ps` now works
- `cd container`, `ls -la`
- `docker build -t containerofcats .` - Build container image
- `docker images --filter reference=containerofcats` - Show images in this container
- `docker run -t -i -p 80:80 containerofcats` - Map port 80 on container to port 80 on ec2 instance with cats image
- Log in to docker hub
docker login --username=YOUR_USER
docker images
docker tag IMAGEID YOUR_USER/containerofcats
docker push YOUR_USER/containerofcats:latest
