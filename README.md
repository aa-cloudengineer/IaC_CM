# Infrastructure as Code (IaC)
Infrastructure as Code (IaC) refers to the process of defining and managing infrastructure, such as servers, networks, and storage, through machine-readable files. This means that instead of manually configuring infrastructure, IaC tools enable teams to automate the provisioning and management of infrastructure using code. This approach allows teams to treat infrastructure as code, which can be version-controlled, tested, and integrated into a continuous delivery pipeline.

IaC manages infrastructure using a descriptive model. Infrastructure includes networks, virtual machines, load balancers, to name a few. An IaC model produces the same environment every time it is applied.

Most common IaC Tools:

- [Terraform](https://github.com/aa-cloudengineer/IaC/tree/main/Terraform)
  A popular IaC tool that enables teams to manage infrastructure resources such as servers, networks, and storage in a declarative way 
  using a simple language called HashiCorp Configuration Language (HCL).
  
- [Cloudformation](https://github.com/aa-cloudengineer/IaC/tree/main/Cloudformation)
 A service provided by Amazon Web Services (AWS) that enables teams to define and manage infrastructure resources as code using templates. 
 CloudFormation supports several AWS services and enables teams to create and manage complex architectures.

- Google CDM
  A service provided by Google Cloud Platform (GCP) that enables teams to define and manage GCP resources as code using YAML or JSON     
  templates.
  
- Azure ARM
  A service provided by Microsoft Azure that enables teams to manage infrastructure resources using JSON templates.

# CM
Configuration Management (CM) Tools, on the other hand, are used to automate the configuration and management of software applications running on the infrastructure. They help teams to maintain consistency across different environments by automating the configuration of software components and ensuring that configurations are applied consistently across all instances of an application.

Configuration Management (CM) maintains the consistency of an application’s performance, as well as its functional and physical inputs along with requirements, overall design, and operations throughout the lifespan of the product.

Most common Configuration Management tools:

- [Ansible](https://github.com/aa-cloudengineer/IaC/tree/main/Ansible)
A popular CM tool that enables teams to automate the configuration and management of software applications. Ansible uses a simple language called YAML to define configurations and supports several operating systems and cloud providers.

-  Chef
  A configuration management tool that automates the deployment, configuration, and management of software.

-  Puppet
  A configuration management tool that helps automate the management of infrastructure, applications, and compliance.

- SaltStack
  A tool that automates the configuration and management of software applications, operating systems, and servers.

  The main difference between Infrastructure as Code (IaC) and Configuration Management (CM) is that IaC focuses on managing and provisioning infrastructure through code, while CM focuses on automating the configuration and management of software applications, operating systems, and servers. IaC tools focus on infrastructure management, while CM tools focus on software configuration management.

IaC and CM are complementary concepts that help teams automate and manage their IT infrastructure more efficiently. While IaC focuses on the infrastructure layer, CM focuses on the application layer. Some common IaC tools include Terraform, CloudFormation, Ansible, and Pulumi, while common CM tools include Chef, Puppet, SaltStack, and Ansible.
