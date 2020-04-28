# 1. Project Setup

Create the Azure resources and Git infrastructure necessary to begin developing Custom Speech models. The setup instructions here are the quickest and the recommended path to running the sample as-is. **They assume you have not moved or changed any files in the repository that you'll create shortly.**

That being said, after running the sample you may [click here](./4-advanced-project-setup.md) for advanced project setup options that may make more sense for a team of engineers or incorporating existing infrastructure.

### Table of Contents

* [Get the Code](#Get-the-Code)
* [Create Resource Group and Resources](#Create-Resource-Group-and-Resourcess)
* [Set GitHub Secrets](#Set-GitHub-Secrets)
* [Install Git Large File Storage](#Install-Git-Large-File-Storage)
* [Next Steps](#Next-Steps)

## Get the Code

You must create a new repository to hold the code and the GitHub Actions pipelines. To create your repository:

1. Log in to GitHub, or [click here](https://github.com/join) to create an account.
2. [Click here](https://github.com/KatieProchilo/CustomSpeechDevOpsSample/generate) to generate a clean copy of this repository to your own GitHub account.
    1. Enter a name for the repository where prompted.
    2. Leave **Include all branches** unchecked. You only need to copy the master branch of this repository.
    3. Click **Create repository from template** to create your copy.
3. Clone your repository. [See here](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository) for instructions on how to clone a repository. Use this repository to walk through this guide and for your own experimentation.

## Create Resource Group and Resources

Developing Custom Speech models with the CI/CD pipeline requires an Azure Resource Group, under which an Azure Storage Account and an Azure Speech Resource must be created. To create these resources, click the Azure Deploy button below:

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FKatieProchilo%2FCustomSpeechDevOpsSample%2Fmaster%2Fazuredeploy.json)

Enter a name for the Resource Group and save it for later. Leave the other fields filled in as-is so that copying and pasting commands is easy throughout the sample. Save these values for later as well. After completing the sample, you may [click here](4-advanced-project-setup.md#Changing-Resource-Parameters) to learn how to customize the names and regions of your resources.

## Set GitHub Secrets

GitHub Secrets serve as parameters to the workflow, while also hiding secret values. When viewing an executed workflow on GitHub, secrets will appear as `***`.

To add GitHub Secrets:

1. In your project's GitHub repository, go to **Settings**.
2. In the left blade, click **Secrets**.
3. Click **Add a new secret**.

Add each of the following secrets and set them to the described value:

* **`AZURE_CREDENTIALS`:** [Click here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) to install the Azure CLI if it is not already installed. Then log in to Azure:

    ```bash
    az login
    ```

    Find the Resource Group name and Storage subscription ID. Use them to set `AZURE_CREDENTIALS` to the JSON output from the following command, and take note that you will be passing in `stcustomspeech000`, the name of the Storage Account you just created:

    ```bash
    az ad sp create-for-rbac --name stcustomspeech000 --role "Storage Blob Data Contributor" --scopes /subscriptions/<<STORAGE_SUBSCRIPTION_ID>>/resourceGroups/<<RESOURCE_GROUP_NAME>> --sdk-auth
    ```

    For example:

    ```json
    {
      "clientId": "########-####-####-####-############",
      "clientSecret": "########-####-####-####-############",
      "subscriptionId": "########-####-####-####-############",
      "tenantId": "########-####-####-####-############",
      "activeDirectoryEndpointUrl": "https:...",
      "resourceManagerEndpointUrl": "https:...",
      "activeDirectoryGraphResourceId": "https:...",
      "sqlManagementEndpointUrl": "https:...",
      "galleryEndpointUrl": "https:...",
      "managementEndpointUrl": "https:..."
    }
    ```

* **`SPEECH_RESOURCE_REGION`:** Set to `westus`, the region of the Azure Speech resource created previously.
* **`SPEECH_SUBSCRIPTION_ID`:** Set to the subscription ID of the Speech resource created previously. For example, `################################`.
* **`SPEECH_PROJECT_NAME`:** Set to the Speech project's name. To create a Speech project:
    * [Click here](https://speech.microsoft.com/portal/) to navigate to the Speech Studio.
    * If needed, use the cog in the upper-right corner to switch to the correct subscription.
    * Click the Speech resource created previously.
    * Click **Go to Studio**.
    * Click **New project** and fill in the fields. The project's name will be the value of the GitHub secret `SPEECH_PROJECT_NAME`.
* **`STORAGE_ACCOUNT_NAME`:** Set to `stcustomspeech000`, the name of the Azure Storage Account created previously.

## Install Git Large File Storage

Custom Speech uses .zip files of .wav audio files for both testing and training models. It is not common practice to store these large files locally or in a Git repository because simple actions like pulling or checking out take a lot of time. However, the testing and training data needs to be versioned and should be stored in some way that enables versioning. There are many possible solutions to this versioning problem, and one is Git Large File Storage (Git LFS); [Click here](https://git-lfs.github.com/) for its homepage.

Git LFS allows developers to use Git in the same way it's always been used, only now Git will not bother with large files until developers interact with them specifically. Now, Custom Speech models can be quickly developed with traceability between the models created, the data that built each model, and the data each model was tested on.

To set up Git LFS:
1. `cd` into the root of the repository you just cloned.
2. Install Git LFS:

    ```bash
    git lfs install
    ```

2. Select the files for Git LFS to manage. To track all training and testing data as it is currently set up:

    ```bash
    git lfs track "testing/**" "training/**"
    ```

    After successfully running the sample, you may [click here](./4-advanced-project-setup.md#Tracking-Data-with-Git-Large-File-Storage) for detailed information on which files should be tracked.

3. Now track **.gitattributes**:

    ```bash
    git add .gitattributes
    ```

4. It will not be necessary for the purposes of the sample, but [click here](https://help.github.com/en/github/setting-up-and-managing-billing-and-payments-on-github/upgrading-git-large-file-storage) to purchase more Git Large File Storage.

## Next Steps

The infrastructure has been created to begin development. [Click here](./2-create-the-initial-custom-speech-model.md) to run the workflow for the first time and create an initial Custom Speech model.