# Description
When you want to run microservices inside of an ECS cluster , the easiest/standard/recommended way is to register Services with ELBs.
You can register the ELBs in DNS and each service is instanly available. No need for a service discovery.

As the number of microservices grow , so increases the cost of the ELBs. Especially in Test/Staging environment this can get quite costly where multiple environment are running on the same cluster.

The alternative is to use a discovery service and a reverse proxy like (Nginx, HaProxy, Traefik, Kong, Fabio).
Most tools/examples I found used Consul. But then I thought, why duplicate the ECS state in consul? That way you can avoid running a consul cluster.

## Generate file using Template
The first use of *elb-watch* is to have a command similar to docker-gen/nginx-proxy where a template is populated and a signal is send to a container.
instead of reading the state from Consul, it reads the state from ECS.

## Route53 sidekick
The second use of *elb-watch* is to find the connection details of container (ip/port) and update a record in route53.
This is useful as a side-kick for services that are not http based (for example your redis server)

# Related projects
- <https://github.com/CpuID/ecs-discoverer>
- <https://github.com/majest/docker-consul-ecs>
- <https://github.com/adamdecaf/aws-ecs-nginx-proxy>
- <https://github.com/awslabs/service-discovery-ecs-consul>
- <https://github.com/awslabs/ecs-refarch-service-discovery/>
- <https://github.com/kyani-inc/ecs-discovery>
- <https://github.com/gliderlabs/registrator>
- <https://github.com/jwilder/docker-gen>

# Reading
- <https://aws.amazon.com/blogs/compute/service-discovery-via-consul-with-amazon-ecs/>
- <http://www.slideshare.net/AmazonWebServices/microservices-and-amazon-ecs>
- <https://segment.com/blog/rebuilding-our-infrastructure/>
- <https://github.com/rhockenbury/trace>
- <https://github.com/jhspaybar/ecs_state>
- <http://engineering.skybettingandgaming.com/2016/05/05/aws-and-consul/>
- <https://sitano.github.io/2015/10/06/abt-consul-outage/>
- <https://www.nginx.com/blog/service-discovery-in-a-microservices-architecture/>
