# Building Microservices Apps from Git Repo

The Workbench supports building applications using four methods:
Git repo, Jar packages, container images, and Helm charts. This article
explains how to build a traditional microservices application from a Git repo
source code, enabling features such as traffic governance, log viewing, monitoring, and tracing.

## Prerequisites

- You need to create a workspace and a user who is added to the workspace with the
  __workspace edit__ role. Refer to [Creating a Workspace](../../../ghippo/user-guide/workspace/workspace.md)
  and [Users and Roles](../../../ghippo/user-guide/access-control/user.md).
- Create two credentials that can access the code repo and image repo.
  See [Credential Management](../pipeline/credential.md).
- Prepare a GitLab repo and a Harbor repo.

## Create Credentials

Following [Credential Management](../pipeline/credential.md), create two credentials:

1. On the __Credentials__ page, create two credentials:

    - git-credential: Username and password for accessing the code repo.
    - registry-credential: Username and password for accessing the image repo.

2. Once created, you can view the credentials on the __Credential List__ page.

## Create Microservices App from Git

1. In the __Workbench__ -> __Wizard__ page, click __Build With Git Repo__ .

    ![Wizard](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/amamba/images/ms01.png)

2. Fill in the basic information as per the instructions and click __Next__ :

    - Name: Specify the name of the resource workload.
    - Resource Type: Currently, only deployments are supported.
    - Deployment Location: Choose the cluster and namespace where the application will be deployed.
      If you want to integrate with microservices, make sure you have
      [created a registry](../../../skoala/trad-ms/hosted/index.md) in the current workspace.
    - Application: Specify the name of the native application. You can select from an existing list
      or create a new one, which by default will have the same name as specified.
    - Replicas: Set the number of Pods for the application.

    ![Basic Information](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/amamba/images/git01.png)

3. Fill in the pipeline configuration details based on the instructions and click __Next__ .

    - Repo: Select a repo or enter the Git repo address. In this example, the Git repo address
      is `https://gitlab.daocloud.cn/ndx/skoala.git`, which should be replaced with the actual
      address. The choice of repo is from the GitLab instance integrated by the user.
    - Branch: The default branch is __main__ and can be left unchanged.
    - Credentials: Select the credential ( __git-credential__ ) for accessing the code repo.
      If it is a public repo, no need to fill this field.
    - Dockerfile Path: Enter the absolute path of the Dockerfile in the code repo.
      For example, __demo/integration/springcloud-nacos-sentinel/code/Dockerfile__ .
    - Target Image Name: Select or enter the target image name. In this example, the address is
      [__release-ci.daocloud.io/test-lfj/fromgit__](http://release-ci.daocloud.io/test-lfj/fromgit),
      which should be replaced with the actual address. The choice of image repo is from the
      image repo instance integrated and bound to the current workspace.
    - Tag: Enter the version of the image repo, for example, __v2.0.0__ .
    - Credentials: Select the credentials for accessing the image repo, for example, __registry-credential__ .
    - ContextPath: Set the context path for the docker build command execution. Specify the relative path
      to the root of the code directory, such as __target__ . If left blank, it defaults to the directory
      where the Dockerfile is located.
    - Build Arguments: The build arguments are passed to the build command in the form of __--build-arg__ .
      You can set the upstream artifact download address, upstream image download address as parameters
      and also define custom parameters.

    ![Pipeline Configuration](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/amamba/images/git02.png)

4. Fill in the container configuration details based on the instructions and click __Next__ .

    - Service Configuration: Specify how the service can be accessed within the
      cluster, node, or load balancer. Example values:

        name | protocol | port | targetPort
        ---- | -------- | ---- | ----------
        http | TCP      | 8081 | 8081
        health-http | TCP | 8999 | 8999
        service | TCP      | 9555 | 9555

        > For more detailed information about service configuration, refer to
        > [Creating Services](../../../kpanda/user-guide/network/create-services.md).

    - Resource Limits: Specify the resource limits for the application, including CPU and memory.

    - Lifecycle: Set commands that need to be executed during container startup, after startup,
      and before shutdown. For more details, refer to
      [Container Lifecycle Configuration](../../../kpanda/user-guide/workloads/pod-config/lifecycle.md).

    - Health Checks: Define health checks to determine the health status of the container and application,
      improving availability. For more details, refer to
      [Container Health Check Configuration](../../../kpanda/user-guide/workloads/pod-config/health-check.md).

    - Environment Variables: Configure container parameters, add environment variables, or pass
      configurations to the Pod. For more details, refer to
      [Container Environment Variable Configuration](../../../kpanda/user-guide/workloads/pod-config/env-variables.md).

    - Data Storage: Configure data volume mounting and data persistence for containers.

    ![Container Configuration](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/amamba/images/ms04.png)

5. On the __Advanced Settings__ page, click __Access MicroServices__ .
   Configure the parameters as per the instructions and click __OK__ .

    - Framework Selection: Choose between __Spring Cloud__ and __Dubbo__ . In this case, select __Spring Cloud__ .
    - Registry Instance: Currently, only hosted Nacos registry instances from the
     [Microservices Engine](../../../skoala/trad-ms/hosted/index.md) are supported.
    - Registry Namespace: The Nacos namespace for the microservices application.
    - Registry Service Group: The service group for the microservices application.
    - Username/Password: If the registry instance requires authentication, enter the username and password.
    - Enable Service Governance: The selected registry instance should have
     [Sentinel or Mesh governance plugins enabled](../../../skoala/trad-ms/hosted/plugins/plugin-center.md).

    ![Advanced Configuration](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/amamba/images/git03.png)

## Viewing and Accessing Microservices Information

1. On the left navigation bar, click __Overview__ , and within the __Applications__ tab,
   select the native application to view its details.

    ![Native Applications](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/amamba/images/git04.png)

2. In the details page, under the __Application Resources__ tab, select the resource with
   the __Service Mesh__ label and click it.

    ![Navigate](https://docs.daocloud.io/daocloud-docs-images/docs/en/docs/amamba/images/git05.png)

3. You will be redirected to the Microservices Engine where you can view the
   [service details](../../../skoala/trad-ms/hosted/services/check-details.md).
