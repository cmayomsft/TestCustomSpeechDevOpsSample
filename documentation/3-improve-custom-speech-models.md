# 3. Improve Custom Speech Models

At this point an initial Custom Speech model has been created. Now the objective becomes maintaining or updating the benchmark model when appropriate. [Click here](./2-initial-custom-speech-model.md) if you have not created an initial Custom Speech model.

### Table of Contents

* [Pull Request More Data Updates](#Pull-Request-More-Data-Updates)
    * [Locally Test Training Data Updates](#Locally-Test-Training-Data-Updates)
    * [Create and Merge the Pull Request](#Create-and-Merge-the-Pull-Request)
* [Workflow for Testing Data Updates](#Workflow-for-Testing-Data-Updates)
    * [Test](#Test)
* [Workflow for Training Data Updates](#Workflow-for-Training-Data-Updates)
    * [Train](#Train)
    * [Test](#Test)
    * [Release](#Release)
* [Next Steps](Next-Steps)

## Pull Request More Data Updates

`cd` into the root of the repository and checkout the **master** branch. From there, create a feature branch:

```bash
git checkout -b newSpeechModel
```

An initial model has already been created, so now attempt to create a better model by updating at least one of the training files:
* `training/related-text.txt`
* `training/pronunciation.txt`
* `training/audio-and-trans.txt`

Make changes to `testing/audio-and-trans.txt` as well. Now that an initial model has been built, updates to the test data will be reflected in the workflow.

Add and commit the changes:

```bash
git add .
git commit -m "More changes to my Custom Speech model."
```

### Locally Test Training Data Updates

Again, for the purposes of this sample it is not necessary to test updates to training data. However, for a production-worthy project [click here](2-create-the-initial-custom-speech-model.md#Locally-Test-Training-Data-Updates) for instructions on how to test updates to training data.

### Create and Merge the Pull Request

Push the changes to the remote repository:

```bash
git push -u origin newSpeechModel
```

Create and approve a Pull Request from the branch **newSpeechModel** into **master**.

Merge or rebase the Pull Request and again navigate to the **Actions** tab of the repository to check out the workflow in progress.

## Workflow for Testing Data Updates

TODO

### Test

TODO

## Workflow for Training Data Updates

TODO

### Train

TODO

### Test

TODO

### Release

TODO

## Next Steps

You have completed the sample! Now you have the tools to continuously improve Custom Speech models. [Click here](./4-advanced-project-setup.md) for more information on best practices and customizing the sample solution to work for your production-worthy project.
