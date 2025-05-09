# GCP overview and account setup

Google cloud provides container resources such as organizations and projects to group and hierarchically manage cloud resources.

The Resource Manager API is used to programmatically manage these resources.

## Decide a resource hierarchy
> [Source](https://cloud.google.com/architecture/landing-zones/decide-resource-hierarchy)

A resource hierarchy is basically a tree structure that helps you organize your resources. It consists of the following levels:

- **Organization**: The root node in the hierarchy. It represents your company or organization. And it is usually associated with a domain name (e.g., example.com).
- **Folder**: A container for organizing projects. You can use folders to group projects by department, team, or any other logical grouping.
- **Project**: The base-level container for all Google Cloud resources. Projects are used to organize resources and manage permissions. Each project has a unique project ID and can contain multiple resources (e.g., Compute Engine instances, Cloud Storage buckets).
- **Resource**: The individual components that make up your Google Cloud environment. Resources can include virtual machines, databases, storage buckets, and more.


The following flowchart shows some of the elements to consider when designing a resource hierarchy:

![Resource Hierarchy Flowchart](./../images/image1.png)

Some examples could be: 

Hierarchy based on accountability framework: 

![Accountability Framework](./../images/image2.png)


## Compared to AWS and Azure
> [Source](https://bgiri-gcloud.medium.com/gcp-aws-azure-cloud-resource-hierarchies-and-billing-management-simplified-guide-608cf7217106)

![Resource Hierarchy Comparison](./../images/image3.png)

AWS : 

- Organization (optional): Top-level container for managing multiple accounts and enforcing centralized policies.
- Organizational Unit (OU) (optional): Sub-division within an organization for further grouping of accounts.
- Account: The core unit for managing resources and billing. You can have multiple accounts within an organization or exist independently.
- Resource: Individual cloud services like EC2 instances, S3 buckets, etc.

Azure:

- Root Management Group: The highest level, encompassing all subscriptions within your Azure environment.
- Management Group: Containers for organizing subscriptions based on needs (e.g., development, production).
- Subscription: A unit for managing resources and billing, similar to the AWS account.
- Resource Group: A collection of related Azure resources for a specific project or application.
- Resource: Individual cloud services like VMs, storage accounts, etc.


## Hands-on : Google Cloud Console and Cloud Shell

### Google Cloud Console

Services in GCP are organized into categories, and in order to use a server, we usually need to enable the API for that service. 

For instance, if I want to create a VM instance, I need to enable the Compute Engine API. And this allows to manage all the services related to Compute Engine, such as creating VM instances, managing disks, and so on.

The following image shows the Compute Engine API enabled in the Google Cloud Console:
![Compute Engine API](./../images/image4.png)

Something different from AWS is that in GCP, we need to enable the API for each service we want to use. And we can see a number of graphs and statistics related to the service we are using which seems interesting ( see the image below ).

![Compute Engine API stats](./../images/image5.png)

Another small thing to note, as opposed to AWS, in GCP, you choose the region and zone when creating a resource.

### Cloud Shell

Cloud Shell is a browser-based shell that provides command-line access to your Google Cloud resources.

**Key Features of Cloud Shell:**
*   **Pre-configured Environment:** Comes with `gcloud` CLI, `kubectl`, Docker, and other essential development tools pre-installed and authenticated.
*   **Persistent Storage:** Provides 5 GB of persistent disk storage in your `$HOME` directory, so your files and configurations persist between sessions.
*   **Language Support:** Supports various programming languages like Java, Go, Python, Node.js, PHP, and Ruby.
*   **Temporary Compute Engine VM:** Runs on a temporary Compute Engine virtual machine, which is managed by Google.

Help commands shows the following: 

```bash
$ gcloud help

NAME
    gcloud - manage Google Cloud resources and developer workflow

SYNOPSIS
    gcloud GROUP | COMMAND [--account=ACCOUNT]
        [--billing-project=BILLING_PROJECT] [--configuration=CONFIGURATION]
        [--flags-file=YAML_FILE] [--flatten=[KEY,...]] [--format=FORMAT]
        [--help] [--project=PROJECT_ID] [--quiet, -q]
        [--verbosity=VERBOSITY; default="warning"] [--version, -v] [-h]
        [--access-token-file=ACCESS_TOKEN_FILE]
        [--impersonate-service-account=SERVICE_ACCOUNT_EMAILS] [--log-http]
        [--trace-token=TRACE_TOKEN] [--no-user-output-enabled]

DESCRIPTION
    The gcloud CLI manages authentication, local configuration, developer
    workflow, and interactions with the Google Cloud APIs.

    For a quick introduction to the gcloud CLI, a list of commonly used
    commands, and a look at how these commands are structured, run gcloud
    cheat-sheet or see the `gcloud` CLI cheat sheet
    (https://cloud.google.com/sdk/docs/cheatsheet).

```

The `gcloud` CLI is the primary command-line tool for interacting with Google Cloud Platform (GCP). It allows you to manage your GCP resources and services directly from your terminal. Here's a high-level overview of how it works:

#### Command Structure

`gcloud` commands follow a hierarchical and consistent structure:

```bash
gcloud [RELEASE_TRACK] [GROUP] [SUBGROUP] [COMMAND] [ENTITY] [POSITIONAL_ARGS] [--FLAGS]
```

-   **`gcloud`**: The entry point for all commands.
-   **`RELEASE_TRACK`** (optional): Specifies the release level, e.g., `alpha`, `beta`. If omitted, it defaults to General Availability (GA).
-   **`GROUP`**: Represents a GCP product or service area, like `compute` (for Compute Engine), `sql` (for Cloud SQL), or `iam` (for Identity and Access Management).
-   **`SUBGROUP`** (optional): Further categorizes commands within a group, e.g., `instances` within `compute`.
-   **`COMMAND`**: The specific action to perform, such as `list`, `create`, `delete`, `describe`, `update`.
-   **`ENTITY`** (optional): The name or ID of the resource you're operating on.
-   **`POSITIONAL_ARGS`**: Required arguments for the command.
-   **`--FLAGS`**: Optional arguments to modify the command's behavior, like `--project=PROJECT_ID`, `--zone=ZONE`, or `--format=json`.

**Example:**
To list all Compute Engine instances in a specific project and zone:
```bash
gcloud compute instances list --project=my-gcp-project --zone=us-central1-a
```

