# Custom Speech DevOps Sample

With this template repository, continuously improve [Custom Speech](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/how-to-custom-speech) models using a CI/CD workflow running on GitHub Actions. Run the project with minimal configuration and adapt it for use with your own project:

* Automatically create new Custom Speech models when training data is updated.
* Create and manage release endpoints when an improved model is built.
* Update the benchmark accuracy when testing data is updated.
* Version Custom Speech data, test results, endpoints, models, and more out of the box.

## Walk Through the Sample

Work through this guide completely to ensure everything is working in your environment. After the sample is working, it can serve as customizable starting point for your project.

***Required:*** Follow step 1, then 2, and then 3 to run this workflow in your personal GitHub repository:

1. [Project Setup](./documentation/1-project-setup.md)
2. [Create the Initial Custom Speech Model](./documentation/2-create-the-initial-custom-speech-model.md)
3. [Improve Custom Speech Models](./documentation/3-improve-custom-speech-models.md)

***Optional:*** After completing steps 1 through 3, follow step 4 to customize the sample to fit your project's specific needs:

4. [Advanced Project Setup](./documentation/4-advanced-project-setup.md)