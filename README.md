# Azure-AI-Agents-with-Azure-Container-Apps-Deploy-at-Scale--Notes
This Repository contains my Notes of "Azure AI Agents with Azure Container Apps (Deploy at Scale)" Course from Udemy

**I) Azure Container Apps (ACA) Essentials: ACA-101**

**A) Evolution of Software Architecture**

**B) Introduction to ACA and Container Orchestration**

**C) ACA Essentials: Environments, Replicas, Revisions & More**

**D) Kubernetes v/s Azure Container Apps**




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

# **C) ACA Essentials: Environments, Replicas, Revisions & More**

# **D) Kubernetes v/s Azure Container Apps**


