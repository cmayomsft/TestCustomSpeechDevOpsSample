# 4. Advanced Project Setup

The workflow is configured to run without customization, but can optionally be customized in a number of ways for your project.

## Table of Contents

* [Changing Resource Parameters](#Changing-Resource-Parameters)
* [Configuring Git Workflows](#Configuring-Git-Workflows)
* [Protect the Master Branch](#Protect-the-Master-Branch)
* [Tracking Data with Git Large File Storage](#Tracking-Data-with-Git-Large-File-Storage)
* [Set Values in the Pipeline](#Set-Values-in-the-Pipeline)
   * [Pipeline Trigger](#Pipeline-Trigger)
   * [Environment Variables](#Environment-Variables)

## Changing Resource Parameters

TODO

## Configuring Git Workflows

TODO

[Click here](https://help.github.com/en/github/administering-a-repository/configuring-protected-branches) to learn more ways to customize and configure protected branches in GitHub.

## Protect the Master Branch

Branch policies should be implemented to prevent developers from pushing directly to the master branch. They should require developers to check-in changes by creating a Pull Request and getting these changes approved by other developers working in the repository.

***Important:*** *Individual GitHub accounts must be public or have a GitHub Pro subscription to enforce branch protections. If you are using a private repository with a personal GitHub account, you will have to change your repository to be public in repository settings.*

To configure these protections:

1. In the home page for your repository on **GitHub.com**, click on **Settings**.
2. On the Settings page, click on **Branches** in the Options menu.
3. Under **Branch protection rules**, click the **Add rule** button.
4. Configure the rule:
   1. In the **Branch name pattern** box, enter **master**.
   2. Check **Require pull request reviews before merging**.
   3. Do **not** check **Include administrators**. The fact that you are an administrator of this repository will allow bypassing restrictions on merging later in this tutorial. However for a real project, consider configuring these restrictions for administrators as well.
   4. Click the **Create** button at the bottom of the page.

After walking through the sample, you can [click here](./4-advanced-project-setup.md#Configuring-Git-Workflows) to learn how to configure the specific branching workflows you require in your own software engineering organization.

## Managing Endpoints

TODO

## Tracking Data with Git Large File Storage

TODO

## Set Values in the Pipeline

If you copy the project as-is, none of the values in this section need to be edited. However, you may wish to edit them to match your own project's configuration, in which case this section provides a deeper explanation behind some possible values to edit.

### Pipeline Trigger

The pipeline will trigger on any push to master, including Pull Requests, that includes changes to training data. With the file structure in the sample, the YAML implementing this is:

```YAML
on:
  push:
    # Execute on pushes to master.
    branches:
      - master
    # The push must include updates to testing or training data.
    paths:
      - 'testing/audio-and-trans.zip'
      - 'training/audio-and-trans.zip'
      - 'training/pronunciation.txt'
      - 'training/related-text.txt'
```

Update `branches` to reflect your git branching workflow. Update `paths` to include all Custom Speech training data - pronunciation, language, and audio and human-labeled transcripts.

### Environment Variables

The following variables in `speech-ci.yml` should be set as follows:

| Variable | Value |
| --- | --- |
| **pronunciationFilePath** | The path from the root of the repository to the pronunciation data file.<br><br>E.g. `training/pronunciation.txt`<br><br>*Note: This should be the same value as one of the three entries for `on.push.paths`.* |
| **relatedTextFilePath** | The path from the root of the repository to the related text data file.<br><br>E.g. `training/related-text.txt`<br><br>*Note: This should be the same value as one of the three entries for `on.push.paths`.* |
| **testTransFile** | The name and extension of the .txt transcript file that will be extracted from `testZipSourcePath`. <br><br>E.g. `test-trans.txt` |
| **testZipSourcePath** | The path from the root of the repository to a .zip with .wav files and a .txt transcript used for testing.<br><br>E.g. `testing/audio-and-trans.zip` |
| **trainTransFile** | The name and extension of the .txt transcript file that will be extracted from `trainZipSourcePath`. <br><br>E.g. `train-trans.txt` |
| **trainZipSourcePath** | The path from the root of the repository to a .zip with .wav files and a .txt transcript used for training.<br><br>E.g. `training/audio-and-trans.zip`<br><br>*Note: This should be the same value as one of the three entries for `on.push.paths`.* |
