## DEMO ECS - Deploying 'container of cats' using Fargate
Create a Fargate Cluster, create a task and container definition and deploy the world renowned 'container of cats' Application from Dockerhub into Fargate.

1. Create Cluster: ECS Console > Clusters > Create Cluster > Networking Only option > name "allthecats", (don't tick New VPC box, use Default VPC instead by not clicking) > Create. If you get ECS error, redo these steps
2. Create Task Definition (deploy container): Task Definitions > New > Compatibility: Fargate > Next Step > def name "containerofcats", no task role needed, operating system family: linux, task size: 1bg memory, 0.5vCPU > click "Add Container": name "containerofcatsweb", image "docker.io/acantril/containerofcats", Memory Limit Soft 1024, Port Mappings: 80 tcp > Add
3. Run it: Clusters > allthecats > Tasks tab > Launch type: fargate, OS family: linux, select VPC: Cluster VPC: default selection, subnet: select 2 at random > Create/Add
4. Cleanup > Stop Task Definition > Task: Actions: Deregister > Cluster: allthecats: Delete
