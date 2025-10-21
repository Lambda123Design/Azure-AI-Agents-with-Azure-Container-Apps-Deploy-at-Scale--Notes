# Azure-AI-Agents-with-Azure-Container-Apps-Deploy-at-Scale--Notes
This Repository contains my Notes of "Azure AI Agents with Azure Container Apps (Deploy at Scale)" Course from Udemy

**I) Azure Container Apps (ACA) Essentials: ACA-101**

**A) Evolution of Software Architecture**

**B) Introduction to ACA and Container Orchestration**

**C) ACA Essentials: Environments, Replicas, Revisions & More**

**D) Kubernetes v/s Azure Container Apps**

**II) Module 1: Getting Started with Azure Container Apps (ACA)**

**A) Lab: Deploying ACA Environment and Azure Container Registry (ACR) (Hands-On Lab)**

**B) What We Will Be Building: "Architectural Pit-Stop"**

**C) Lab: Deploying Azure AI Foundry and GPT LLM (Hands-On Lab)**

**D) Lab: Building and Pushing Container Image From Docker to ACR (Hands-On Lab)**

**E) Lab: Deploying ACR Image as an Azure Container App (Hands-On Lab)**




# **I) Azure Container Apps (ACA) Essentials: ACA-101**

# **A) Evolution of Software Architecture**

Alright, so with this video, let's take a look at the evolution of software architecture, because that's going to really help us in understanding the why behind Azure Container Apps. And yeah, the why behind everything. Why are we even learning this course and how it's going to help us moving forward into the future of technology and AI as we see it today?

So this is how, in a nutshell, the evolution of software development really looked like dating all the way back from the 1960s to the current era of AI that we are living in. Back in the days in the 1960s, it was the period of the mainframe era in which you had really, really large computers. The very first computers that were even started could not fit inside of your home. They had to be in some sort of a dedicated place. They even didn't have an operating system of their own. Well, in a sense that they didn't have an operating system technology-wise, but the operating system was just a human. So a human would carry out the tasks and perform some calculations using punched cards. So we didn't even have operating systems.

If you move forward to the 1980s to 1990s, that's when the rise of personal computers really came into the picture. That's the period when Steve Jobs announced the first personal computer, I think it was named after his daughter, which was Lisa. Then came the late 1990s to 2000, which was the internet revolution. Yep, you heard that right. It was the .com era in which everybody was rushing to get their businesses up on the internet. This was pretty similar to the AI era, the only difference being it was the era of .com, and it had the same hype and the same promises that AI is presenting to us today.

Then if you go forward to the 2010s, people started building software differently. They moved their focus towards software as a service, started selling subscriptions. There was a lot of heavy focus on product management and the user experience because if your consumers aren't happy, it’s not good for your business. Over and out.

Now we are living in the 2020 era. That's the era of AI. With AI, there have been a lot of advancements in Transformers, machine learning, deep learning, and whatnot. So it's not just that the hardware or technology has evolved, but the art of building software has also evolved. Back in those days, you used to work on a monolithic architecture, meaning you would write the code for the front end, the back end, and the database in a single code base, and launch your application as a whole.

This had severe bottlenecks. For instance, if users were only using your front end, only three requests to your front end, they weren’t really dealing with all those backend services. To scale the front end, with monolithic architecture, you’d have to scale the entire code base, which is inefficient and costly. Even today, legacy banks that haven’t modernized often still use this monolithic approach. For example, working with .NET, C# MVC architecture, SQL databases using Entity Framework Core for backend communication, and HTML/CSS scripts for the frontend is essentially monolithic.

Developers then realized these bottlenecks and moved towards service-oriented architecture (SOA). Here, the front end communicates with backend services via an enterprise service bus, which picks up the relevant backend service. For example, in an e-commerce website, checkout and payment gateway services would be separate, and the front end request is routed based on the user’s action. This decoupling was an improvement, but still limited in modularity.

The next step was microservices and serverless architecture. Microservices decouple components as far as possible. A microservice could be a single backend service or a combination of backend services and a database. The front end communicates through an API gateway. This setup allows scaling individual services independently and enables teams to focus on specific services, paving the way for better collaboration.

Containers play a crucial role in microservices. You build a container image—a zip file containing all the commands and requirements to run your application—and deploy it to a cloud server. Containers allow modular components to run independently. Container orchestration becomes essential for communication, security, and scaling. Azure offers two tools for this: Azure Kubernetes Service (AKS) and Azure Container Apps (ACA). AKS is widely adopted but requires skilled engineers. ACA offers serverless architecture where infrastructure management is abstracted, letting developers focus on business logic, scaling, and microservice communication.

Bear in mind, ACA and AKS solve the same problem of container orchestration, but ACA abstracts infrastructure control while being built on Kubernetes. This helps developers manage microservices without worrying about underlying servers.

Now let’s discuss containers in more detail. A meme captures it humorously: "You're not in a software project until someone says it works on my machine." Developers face the "dependency hell" problem—replicating an application from a local environment to another server, including all system-level components and libraries, is difficult. Virtual machines are heavy and challenging to replicate, leading to wasted development time.

Containers solve this by providing a lightweight, replicable environment. You package your application and its dependencies into a container image (a zip folder). Running this image as a container ensures it works consistently across different servers. Docker is the platform that provides the runtime to build these images and run them as containers. Docker works across operating systems, often leveraging Windows Subsystem for Linux (WSL) to run Linux environments on Windows or macOS.

Docker also serves as an image registry for versioning your application, tracking versions like v1, v2, v3, and so on. Docker uses a Dockerfile—a set of instructions for the Docker daemon—to build images. Images are immutable; changes require building a new image. Containers are instances of these images running your application.

Azure Container Registry (ACR) is Microsoft’s secure alternative to Docker Hub, supporting virtual networks and encrypted communication. In labs, we build images with Docker but deploy containers from ACR.

Virtualization vs. containerization: VMs are heavy, with each VM requiring its own OS, slow startup, and hard to manage. Containers share the host OS kernel, making them lightweight, fast to start, and portable. Containers align with DevOps and microservices, whereas VMs suit monolithic apps.

In summary: VMs are heavyweight, slow, and less portable. Containers are lightweight, fast, portable, and DevOps-friendly. The winner? Docker, Docker, Docker!

This long video provides a strong foundation for understanding microservices, containers, and Azure Container Apps. Kudos to you if you made it through—it’s pivotal for grasping deeper concepts in the next videos.

# **B) Introduction to ACA and Container Orchestration**

So with this video, we’re going to have a very brief introduction to Azure Container Apps. We’ll see how they came into existence, how this feature evolved, and get an overall overview of the cool features that it has to offer us.

To begin, let’s quickly recap everything we discussed between the traditional application approach and the microservices application approach that we are trying to understand today. The traditional application approach relied on a monolithic codebase that hosted the frontend, backend, database, and all the services together. It scaled by loading the app on multiple servers and VMs. However, it had a severe bottleneck: you couldn’t scale the frontend or backend individually because they were tightly coupled. To scale even one part, you had to scale the entire application, making it heavyweight, non-portable, and computationally expensive.

As software architecture evolved, it migrated from the traditional monolithic approach to the microservices-based approach. In this modern approach, developers build applications on the foundations of a decoupled architecture. For example, in an e-commerce app, there could be separate microservices for session storage, checkout, email notifications, delivery tracking, and payment gateways. Each of these microservices is independent yet communicative, allowing granular control over scaling and communication. You can scale just one microservice—say, the payment gateway—without affecting others.

However, with the microservices approach came a new problem: how do we orchestrate these microservices effectively? Orchestration includes managing communication between services, defining scaling rules (like setting minimum and maximum replicas), and ensuring smooth coordination between independent services. This need for orchestration gave rise to the challenge of container orchestration.

Developers wanted to build applications that could be distributed across multiple web servers and run the same way everywhere, just as they did on their local devices. Virtual Machines (VMs) were not the ideal solution for this, and that’s where containers came into the picture. Containers ensured consistency and helped avoid dependency hell. To orchestrate these containers efficiently, Kubernetes was introduced—and that’s where Azure Kubernetes Service (AKS) and Azure Container Apps are built upon.

Even though Azure Container Apps is a highly abstracted version of Kubernetes, it still relies on the Kubernetes foundation, which is an open-source, widely adopted platform designed to manage and scale containerized applications. Thus, the evolution moved from VMs → Containers → Kubernetes.

Container technology has come a long way. Around 2004–2007, Google began exploring container concepts. In March 2013, Docker was released—a containerized platform based on Linux with native integration into Windows and macOS. Docker introduced features like the Docker daemon, Docker runtime, and image registries for storing versions of applications. In October 2013, Container Linux by CoreOS was released, marking another major advancement. Then, in June 2014, Kubernetes was announced—an open-source container orchestration and scheduler created by Google, now maintained by the Cloud Native Computing Foundation.

Developers quickly realized the difficulty in maintaining containers at scale, which led to Kubernetes’ rapid adoption. Azure Container Apps emerged as a serverless container orchestration platform developed by Microsoft. It provides all the key orchestration features like scheduling, health monitoring, failover, resiliency, scaling, networking, and coordinated upgrades.

With Azure Container Apps, you can define event-driven scaling rules—for example, scaling based on the number of blobs in a storage account or pending messages in an Azure Service Bus queue. It’s serverless, meaning you don’t have to manage or patch the underlying infrastructure. Microsoft handles the compute and infrastructure, while you focus on the business workflow, scheduling, scaling, and inter-service communication.

Compared to Azure Kubernetes Service (AKS), Azure Container Apps offers faster time-to-market and a much smaller learning curve. While AKS provides deep infrastructure control, Container Apps strikes a sweet balance—offering both developer productivity and sufficient control over microservices orchestration.

If we look at Azure’s containerized workload options—from Red Hat OpenShift to Azure Kubernetes Service (AKS) and all the way to Azure Functions—we notice a shift from infrastructure-heavy solutions on the left to serverless-heavy ones on the right. Moving toward serverless means greater developer productivity but less granular control. AKS gives developers fine control over ingress, scaling, and inter-service communication, but it demands infrastructure expertise and time. Azure Functions, being entirely serverless, sacrifices that level of control.

Before Azure Container Apps, there wasn’t a sweet spot that offered both ease of use and flexible control. That’s exactly where Azure Container Apps fits in—it combines the best of both worlds. It brings together the infrastructure control of Kubernetes and the serverless simplicity of Azure Functions or Container Instances.

Working with Kubernetes requires strong engineering expertise and a longer setup time. Azure Container Apps, on the other hand, lets developers focus on business logic instead of infrastructure. It’s serverless, Kubernetes-based, and ideal for teams aiming for faster delivery without sacrificing too much flexibility.

Now that we’ve introduced Azure Container Apps, let’s move on to its definition and core use cases. Azure Container Apps is a serverless platform that reduces infrastructure overhead and costs while running containerized applications. You don’t have to manage servers, security patches, or configurations—Container Apps automatically provides the latest, secure infrastructure so you can focus on development.

Common use cases include deploying APIs, hosting background processing jobs, and handling event-driven workloads. The platform supports event-driven scaling, allowing applications to automatically scale based on queue messages, blobs, or HTTP traffic.

Let’s discuss a few example scenarios. For public API endpoints, you can easily implement blue-green or canary deployments. Suppose version 1 of your app is live in production, and you’re testing version 2 with new features. You can route 20% of the traffic to version 2 while keeping 80% on version 1. If everything runs smoothly, gradually shift more traffic until version 2 takes 100%. Doing this in Kubernetes would require complex setup (Cluster IPs, Ingress, routing policies), but in Azure Container Apps, it’s simple and built-in.

For background processing, you can run scheduled jobs—for example, performing database migrations or backups every 12 hours. For event-driven processing, scaling rules can depend on Service Bus queue length, blob count, or HTTP traffic.

Azure Container Apps also supports microservice communication with mutual TLS authentication, Dapr sidecars (Distributed Application Runtime), and automatic autoscaling. It enables internal/external ingress control, custom domain binding, and VNet integration, letting you use private subnets or Azure-managed virtual networks for microservice communication.

Because Azure Container Apps is based on containers, any language or runtime (Linux, Windows, etc.) is supported. It follows a pay-per-use model, so when your app scales down to zero replicas, you pay nothing for compute.

In summary, Azure Container Apps is built on serverless, event-driven scaling principles and runs microservices without requiring developers to manage Kubernetes or infrastructure. It supports blue-green deployments, A/B testing, traffic splitting, flexible networking, and custom scaling rules. It offers all the goodness of Kubernetes with the simplicity of serverless—a true middle ground for productivity and control.

That’s pretty much it for this introductory video—a brief but complete overview of Azure Container Apps. Next, we’ll dive deeper into how Container Apps work and go through a series of exciting hands-on labs and demos to explore their power in practice. So, without further ado, let’s move on to the next set of videos!

# **C) ACA Essentials: Environments, Replicas, Revisions & More**

In this video, we will try to understand the nitty-gritty details and internal workings of Azure Container Apps. It is an essential deep dive into the fundamental concepts of Azure Container Apps. Without further ado, let’s get started. The first concept we will explore is the boundary of a container app, which is called a Container Apps Environment. As shown in the diagram, the environment is a logical boundary that contains multiple container apps and provides the compute engine or runtime for them. Within an environment, you can have several container apps, depending on the resources allocated to the environment. Essentially, when you define an environment, you define the compute resources like CPU cores and RAM that will be available for all container apps within it.

A Container Apps Environment serves as a logical or isolation boundary around a collection of container apps. Inside this environment, container apps—like Container App One and Container App Two—run your applications. Within each container app, there can be multiple containers. One is the main application container, which carries out the primary business logic, while others could be sidecar containers, which enhance functionality but are not part of the main workflow. For example, a sidecar container could copy data from the main application container to an Azure Blob storage or AWS bucket. All container apps within an environment share the resources and virtual network of that environment, allowing them to communicate with each other securely.

Textbook definitions describe a Container Apps Environment as a secure boundary around one or more container apps and jobs. The Azure Container Apps runtime manages each environment, taking care of OS upgrades, scaling operations, failover procedures, and resource balancing. Because Azure Container Apps is a serverless offering, developers don’t need to worry about provisioning virtual machines or managing OS updates—Microsoft handles this automatically. Each environment is supported by a virtual network, which can either be a new network created by default or an existing network provided by the developer. Multiple container apps in the same environment share this virtual network and write logs to the same destination. You can also integrate Azure Functions and Azure Spring Apps into a Container Apps Environment, along with custom container images from Docker Hub or Azure Container Registry.

When deploying a Container Apps Environment, you can choose between two SKUs: Workload Profile and Consumption Plan. These SKUs differ in billing and internal resource allocation. With a Workload Profile, you reserve specific compute resources (like a particular virtual machine SKU) for your container apps. This is ideal for long-running workloads, as you know exactly the compute resources required. Billing is based on reserved compute capacity, even if container apps are scaled down to zero. On the other hand, the Consumption Plan uses shared compute, dynamically allocating resources based on demand. This is better suited for development or sporadic workloads because you are billed only when containers are running. In the Consumption Plan, replicas can scale down to zero, meaning no cost until traffic resumes.

Moving on to containers, each container app can have multiple containers, including main application containers and sidecars. Containers are the smallest deployable units in Azure Container Apps and are technology-agnostic, as long as they are packaged as container images. Each container app is grouped into pods and operates on Linux nodes in labs, managed entirely by Azure. Containers are bound to revisions, which are immutable snapshots of a container image and configuration at deployment time. Each time you update a container app with a new image, a new revision is created. Revisions allow for controlled deployments like blue-green or canary deployments, where traffic is gradually routed to the new version to test stability before full rollout. Safe rollbacks are possible by deactivating a problematic revision while the previous revision continues serving traffic.

Revisions scale independently using replicas, which are the number of running instances of a revision at any given time. Each replica can host one or more containers and handles traffic spikes. Replicas are stateless, meaning they don’t maintain local state, so persistent data should be stored in databases rather than in replicas. Incoming traffic is distributed evenly across replicas, typically using a round-robin approach. This ensures that workloads are handled efficiently while maintaining isolation.

In addition to container apps, Azure Container Apps supports jobs, which are containers that run to completion rather than continuously. Jobs can be triggered on demand, by events, or on a schedule (e.g., every 12 hours). They are useful for tasks like database migrations, data copying, or background batch processing. Jobs share the same environment-level networking, secrets, and scaling infrastructure as container apps but are designed to finish their execution instead of running indefinitely.

To summarize, Azure Container Apps can be visualized using a real-life analogy: the environment is like an apartment complex, a container app is like an apartment, a revision is like a snapshot or backup of that apartment, replicas are like multiple identical rooms, and containers are the furniture and appliances inside these rooms running workloads like APIs, background jobs, or processes. This video covered everything from environments to container apps, revisions, replicas, and jobs, providing a detailed view of how Azure Container Apps manages compute, isolation, deployment, scaling, and lifecycle management efficiently.

# **D) Kubernetes v/s Azure Container Apps**

In this video, we dive into the differences between Azure Container Apps (ACA) and Azure Kubernetes Service (AKS), which is a common question on discussion forums and Microsoft Tech Community. Understanding these differences is important from both a developer and architectural standpoint.

At a high level, both AKS and ACA aim to solve the same fundamental problem: container orchestration. While containers solve the problem of replicating applications across environments, the next challenge is orchestrating a large number of containers and managing the behavior of microservices. Both ACA and AKS focus on automation, enabling developers to define scaling rules, deploy containers from Azure Container Registry (ACR) or Docker Hub, and manage the CI/CD pipeline. They also aim to optimize resource allocation, efficiently utilizing compute resources across nodes, provide load balancing, and offer health monitoring to maintain resilient applications.

Despite these shared goals, the key difference between ACA and AKS lies in the level of abstraction. Moving from left to right in the spectrum of infrastructure control to developer productivity, Virtual Machines and AKS are more infrastructure-heavy, whereas ACA and Azure Functions are designed to enhance developer productivity. ACA abstracts much of the underlying infrastructure, allowing developers to focus on business logic rather than managing clusters, nodes, and networking. Although ACA runs on Kubernetes under the hood, it is serverless and opinionated, meaning Microsoft manages most of the infrastructure while offering less flexibility than AKS. In contrast, AKS provides full control over the Kubernetes system components, clusters, nodes, and networking.

A simple analogy helps clarify when to use each. For deploying a small application like a single-page blog, AKS would be overkill in terms of cost and complexity, while ACA provides a cost-effective, serverless solution. However, for large-scale enterprise workloads, such as Amazon.com or PayPal, AKS is better suited because it offers fine-grained control over complex microservices architectures. ACA is ideal for simpler, event-driven microservices where infrastructure management is offloaded, making it cost-effective, easy to start with, and suitable for startups prioritizing quick time-to-market.

Other notable differences include cluster management and scaling. In ACA, the underlying compute engine is fully managed by Azure, including OS patching, while in AKS, this management is partial, and scaling and cluster operations are partly the developer's responsibility. ACA provides event-driven automatic scaling out of the box, whereas AKS requires additional setup using Kubernetes Event-Driven Autoscaling (KEDA).

Regarding pricing, ACA charges per CPU core and memory per second in the consumption plan, making it cost-effective for both long-running and sporadic workloads. AKS, on the other hand, charges per node per hour, which requires maintaining at least two nodes, and can cost around $1,000 per month even with minimal configuration.

In summary, while ACA and AKS solve similar container orchestration problems, the choice between them depends on abstraction level, control requirements, workload complexity, and cost considerations. ACA is suitable for serverless, event-driven microservices with minimal infrastructure management, while AKS is appropriate for enterprise-scale applications requiring fine-grained control. This strategic knowledge equips developers and architects to make informed decisions about which service to use for their workloads.

# **II) Module 1: Getting Started with Azure Container Apps (ACA)**



# **A) Lab: Deploying ACA Environment and Azure Container Registry (ACR) (Hands-On Lab)**

# **B) What We Will Be Building: "Architectural Pit-Stop"**

# **C) Lab: Deploying Azure AI Foundry and GPT LLM (Hands-On Lab)**

# **D) Lab: Building and Pushing Container Image From Docker to ACR (Hands-On Lab)**

# **E) Lab: Deploying ACR Image as an Azure Container App (Hands-On Lab)**

