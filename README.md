**Github Actions CI/CD**

# Github Actions

GitHub Actions are automated processes that you can set up in your repository to build, test, package, release, or deploy your code. You can use them to automate your workflow and add custom behaviors to your repository.

## Advantages of GIthub Actions

1. **Automation:** 
 
- GitHub Actions allow you to automate your workflow, so you don't have to manually build, test, package, release, or deploy your code. This can save you time and effort, and help you ensure that your code is always up-to-date and working as expected.

2. **Customization:**

- GitHub Actions are highly customizable, so you can tailor your workflow to fit your specific needs. You can define custom triggers, use different actions and services, and configure your workflow to run on different platforms and environments.

3. **Integration:**

- GitHub Actions integrate seamlessly with your repository, so you can easily set up and manage your workflow from within GitHub. You can also use them in combination with other tools and services, such as deployment platforms, package repositories, and continuous integration servers.

4. **Collaboration:**

- GitHub Actions are collaborative, so you can share your workflow with your team and contribute to the development of open-source projects. You can also use them to automate tasks that involve multiple repositories or organizations.

## Key functionality of GitHub Actions

GitHub Actions is a continuous integration and delivery (CI/CD) platform that allows you to automate your software development workflows. 

Some key functionality of GitHub Actions includes:

1. Running tests and code checks automatically when you push code to your repository.

2. Building and deploying your code to various environments automatically.

3. Automating the release process for your code.

4. Running custom scripts or actions in response to specific events such as creating or merging a pull request.

Overall, GitHub Actions allows you to automate many of the tasks involved in the software development process, helping you save time and reduce the chance of errors.

## Events

1. **Push events:** 

- Triggered when you push code to a repository.

2. **Pull request events:** 

- Triggered when you create or update a pull request.

3. **Issue events:** 

- Triggered when you open, close, or update an issue.

4. **Release events:** 

- Triggered when you create or publish a release.

5. **Comment events:** 

- Triggered when you comment on a commit, issue, or pull request.

6. **Schedule events:** 

- Triggered on a schedule that you specify (e.g., daily, weekly).

Example:

    on:
        push:
            branches:
                - master
    pull_request:
        branches:
            - master

In this example, the workflow is named "CI" and it is triggered by two types of events: push events and pull request events. The workflow will run only when code is pushed to the master branch or when a pull request is created against the master branch.









# Github Workflows

GitHub Workflows are a way to automate tasks that you use in your software development workflows. Workflows are made up of individual Jobs, which are defined by a series of steps. Each step in a job can run a script, an action, or an external command. 

- Workflows can be triggered by a variety of events, such as pushes to a repository, the creation of a pull request, or the opening of an issue.

- A workflow in GitHub Actions is defined in a YAML file that is stored in the .github/workflows directory in your repository. The file must have a .yml or .yaml extension.


1. **Build and test:** 

- This Workflow could be triggered whenever you push new code to your repository. It could run your test suite to ensure that the code is working as expected, and then build a production-ready version of your code.

2. **Release:** 

- This Workflow could be triggered whenever you create a new release tag in your repository. It could build and package your code, and then upload the package to a package repository or a deployment service.

3. **Deploy:** 

- This Workflow could be triggered whenever you push new code to a specific branch (e.g. production). It could build and package your code, and then deploy it to your production environment.

Example:

Here is a simple example of a workflow file that runs a test job whenever code is pushed to the repository:

    name: CI

        on: push

        jobs:
            test:
            runs-on: ubuntu-latest
            steps:
                - uses: actions/checkout@v2
                - run: npm install
                - run: npm test

This workflow is named "CI" and it is triggered by push events. It consists of a single job called "test" that runs on an Ubuntu environment. 

The job has three steps: 

1. checking out the code

2. Installing dependencies

3. Running tests.

Whenever code is pushed to the repository, the "CI" workflow will run and execute the steps in the "test" job. This can help ensure that the code is always tested and working properly.


## Actions

Here is an example of a GitHub Action that deploys a static website to GitHub Pages:

    name: Deploy to GitHub Pages

    on:
        push:
            branches:
                - master

    jobs:
        build:
            runs-on: ubuntu-latest
            steps:
                - uses: actions/checkout@v2
                - name: Build and Deploy
                uses: peaceiris/actions-gh- pages@v3
                with:
                    github_token: ${{     secrets.GITHUB_TOKEN }}
                    publish_dir: ./public

This action is triggered whenever you push new code to the *master* branch of your repository. 

It runs on the latest version of Ubuntu, checks out the code, and then uses the *peaceiris/actions-gh-pages* action to build and deploy the code to GitHub Pages.

The *publish_dir* parameter specifies the directory that contains the static files to be deployed, and the *github_token* parameter allows the action to authenticate with GitHub and push the changes to the *gh-pages* branch.

## Monolithic actions

In a monolithic action, all the steps for an action are included in a single file. 

This can make it easier to manage and maintain the action, as all the code is in one place. However, monolithic actions can also be more difficult to test and debug, as it can be harder to isolate issues to a specific step.

Here is an example of a monolithic action that builds and pushes a Docker image to a registry:

    name: Build and push Docker image

        on: [push]

        jobs:
            build:
                runs-on: ubuntu-latest
                steps:
                    - uses: actions/checkout@v2
                    - name: Build and push image
                    run: |
                        docker build -t my-image .
                        docker login -u username -p password
                        docker push my-image

This action is triggered whenever a push event occurs on the repository. It consists of a single job with two steps:

1. The **actions/checkout** action retrieves the code from the repository.

2. The **Build and push image** step builds a Docker image from the code and pushes it to a registry.

This action is monolithic because all the steps are included in a single file.






# Github Marketplace

GitHub Marketplace is a platform that allows developers to find and purchase tools and services that integrate with GitHub. Some examples of tools and services that are available on GitHub Marketplace include project management tools, code review tools, continuous integration and deployment services, and performance monitoring tools. To use GitHub Marketplace, you need to have a GitHub account.

You can browse the Marketplace by visiting the GitHub Marketplace website or by accessing the Marketplace from the GitHub website.

[Github Marketplace](https://github.com/marketplace?type=)

## Starter Workflow

A starter workflow is a pre-configured GitHub Actions workflow that you can use as a starting point for your own workflow. GitHub provides a number of starter workflows that you can use to automate common tasks, such as building and deploying code or running tests.

To use a starter workflow, you can copy the workflow file to your repository and modify it to fit your needs. 

For example, here is a starter workflow for building and deploying a static site:

    name: Deploy

        on:
            push:
                branches: [ master ]

    jobs:
        build:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v2
        - name: Install dependencies
        run: npm install
        - name: Build
        run: npm run build
        - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
         with:
            github_token: ${{ secrets.GITHUB_TOKEN }}
            publish_dir: ./public

This workflow is triggered whenever a push event occurs on the master branch. It consists of a single job with four steps:

1. The **actions/checkout** action retrieves the code from the repository.

2. The **Install dependencies** step installs the required dependencies for the project.

3. The **Build** step builds the static site.

4. The **Deploy** step uses the **peaceiris/actions-gh-pages** action to deploy the built site to GitHub Pages.

## Action Creation

To create a GitHub Action, you need to create a workflow file in your repository. A workflow is a defined series of steps that can be automated on GitHub.

Here's an example of a simple workflow that runs a Python script whenever a push event occurs on the repository:

    name: Run Python script

    on: [push]

    jobs:
        build:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v2
        - name: Run script
         run: python script.py

To create a GitHub Action, you need to create a workflow file in your repository. A workflow is a defined series of steps that can be automated on GitHub.

Here's an example of a simple workflow that runs a Python script whenever a push event occurs on the repository:

Copy code
name: Run Python script

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Run script
      run: python script.py

This workflow consists of a single job with two steps:

1. The **actions/checkout** action retrieves the code from the repository.

2. The **Run script** step runs a Python script called **script.py**.

To create this workflow, you would create a file called **main.yml** in the **.github/workflows** directory of your repository, and copy the above code into the file.

There are many other options and configurations that you can use to customize your workflow. You can find more information about creating GitHub Actions in the GitHub Actions documentation.

## Github Action Governance

The ability to run code comes the need for governance to ensure that Actions are used safely and responsibly. Here are some ways you can practice good governance when using GitHub Actions:

1. Use the least privilege principle: when creating a workflow, make sure to only grant the permissions that are absolutely necessary for the Action to run. This helps to reduce the risk of unintended consequences.

2. **Use secret scanning:** 

- GitHub provides a secret scanning feature that can help you detect and prevent the accidental exposure of secrets such as API keys in your code.

3. **Use gated workflows:** 

- you can set up a gated workflow that requires a code review and/or approval before it can be run. This can help to ensure that the code being run is reviewed and approved by multiple people before it is executed.

4. **Use branch protection rules:** 

- you can set up branch protection rules to require that all code changes are reviewed before they are merged. This can help to prevent malicious code from being merged into your repository.

5. **Monitor your workflows:** 

- it is important to regularly monitor your workflows to ensure that they are running as expected and to detect any issues or security concerns.

## Troubleshooting Tools and Techniques

1. **Workflow logs:** 

- The most basic tool for troubleshooting issues with your workflows is the workflow logs. You can access the logs for a workflow by clicking on the "Actions" tab in your repository, selecting the workflow you want to view, and then clicking on the specific run you want to view the logs for. The logs will show you the output from each action in the workflow, as well as any errors that occurred.

2. **Debugging actions:** 

- You can use the debug action in your workflow to print debug messages to the workflow logs. This can be helpful for understanding what is happening in your workflow and identifying the source of any issues.

3. **Using environment variables:** 

- You can use environment variables to pass information between actions in your workflow. For example, you might set an environment variable in one action and then use it in a later action to customize its behavior.

4. **Using workflow commands:** 

- GitHub Actions provides a set of workflow commands that you can use to control the execution of your workflows. For example, you can use the if command to conditionally execute actions based on the value of an environment variable.

5. **Using third-party tools:** 

- There are a number of third-party tools that can be helpful for troubleshooting issues with your workflows. For example, you might use a linting tool to check your workflow file for syntax errors, or a testing tool to validate the behavior of your actions.

## Debug Workflows

There are a few different ways you can debug your GitHub Actions workflows:

1. **Print debug messages:** 

- One of the most basic ways to debug your workflows is to use the echo command or the debug action to print debug messages to the workflow logs. This can be helpful for understanding what is happening in your workflow and identifying the source of any issues.

2. **Set breakpoints:** 

- You can use the workflow-debug command in your workflow to set a breakpoint, which will pause the execution of your workflow at that point. This can be useful for inspecting the state of your workflow and debugging issues.

3. **Use environment variables:** 

- You can use environment variables to pass information between actions in your workflow. For example, you might set an environment variable in one action and then use it in a later action to customize its behavior.

4. **Use third-party tools:** 

- There are a number of third-party tools that can be helpful for debugging issues with your workflows. For example, you might use a linting tool to check your workflow file for syntax errors, or a testing tool to validate the behavior of your actions.

# Github Actions CI/CD Workflows

CI/CD (continuous integration/continuous delivery). With GitHub Actions, you can define a workflow that automatically builds, tests, and deploys your code to a specific environment every time you push a commit or create a pull request.

Here's an example of a simple CI/CD workflow that you could use with GitHub Actions:

1. When you push a commit to the repository, the workflow is triggered and runs a series of tasks, such as building the code and running tests.

2. If all of the tasks are successful, the workflow proceeds to the next step, which is to deploy the code to a staging environment.

3. Once the code is deployed to the staging environment, you can manually test it to ensure that everything is working as expected.

4. If the code is working as expected, you can then use the workflow to deploy it to the production environment.

## CI Workflow

GitHub Actions can be used to set up a continuous integration (CI) workflow, which is a series of automated steps that are triggered when code is pushed to a repository. 

A CI workflow can help you automatically build, test, and deploy your code, saving you time and reducing the risk of errors.

To set up a CI workflow using GitHub Actions, you will need to create a configuration file called a "workflow" in your repository. This file is written in YAML and defines the steps that make up your CI workflow.

Here is an example of a more complex CI workflow that builds and deploys a static website to GitHub Pages:

    name: CI

    on: [push]

    jobs:
        build:
            runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v2
        - name: Install dependencies
          run: |
            npm install
        - name: Build site
        run: |
            npm run build
        - name: Deploy to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@3.6.1
        with:
            ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
            BRANCH: gh-pages
            FOLDER: build

This workflow is triggered whenever code is pushed to the repository (on: [push]). It consists of a single job called "build" that runs on the latest version of Ubuntu. The job has four steps:

1. The first step checks out the code from the repository.

2. The second step installs the dependencies for the project using npm.

3. The third step builds the static website using the command npm run build.

4. The fourth step deploys the built website to GitHub Pages using the github-pages-deploy-action Action.

To use this workflow, you will need to create a personal access token and store it as a secret in your repository. You can then reference the secret in your workflow using ${{ secrets.ACCESS_TOKEN }}. This allows you to authenticate with the GitHub API and deploy your website to GitHub Pages.


## Super Linter 

Super Linter is an open-source project that provides a unified interface for running a variety of code linters. It can be used to lint code written in languages such as:

- Bash
- CoffeeScript
- Go
- JSON
- Python
- Ruby
- Terraform
and many more

To use Super Linter in GitHub Actions, you will need to create a workflow file in your repository. 

This file defines a set of tasks that will be run whenever a certain trigger occurs (e.g. when you push code to your repository). Here is an example workflow file that uses Super Linter to lint the code in your repository:

    name: Lint Code

    on: [push]

    jobs:
        lint:
            runs-on: ubuntu-latest
            steps:
                - uses: actions/checkout@v2
                - name: Install Dependencies
                  run: |
                    apt-get update
                    apt-get install -y curl
                - name: Install Super Linter
                run: |
                    curl -L <https://git.io/super-linter> | bash
                - name: Lint Code
                run: |
                    super-linter

This workflow will run whenever you push code to your repository. It will install the necessary dependencies (e.g. curl), install Super Linter, and then run the super-linter command to lint your code.

## CD Workflow

Here's an example of a simple CD workflow using GitHub Actions:

1. Create a new repository in GitHub and push your code to it.
2. In the root of your repository, create a new directory called **.github/workflows**.
3. In the **.github/workflows** directory, create a new file called **deploy.yml**. This file will contain the instructions for your CD workflow.
4. In the **deploy.yml** file, define your workflow by specifying a name and the trigger that will start the workflow:

    name: Deploy

    on:
        push:
            branches:
                - master

This workflow will be triggered every time you push to the master branch of your repository.

5. Add a build step to your workflow by using the **actions/setup-node** action and the **actions/npm** action:

    jobs:
        build:
            runs-on: ubuntu-latest
            steps:
                - uses: actions/setup-node@v1
                with:
                    node-version: 12
            - run: npm install
            - run: npm run build

This will install the necessary dependencies and build your code.

6. Add a step to test your code by using the **actions/setup-node** action and the **actions/npm** action:

    - run: npm test

This will run any tests you have defined in your project.

7. Add a step to deploy your code to a hosting platform, such as GitHub Pages or Heroku:

    - name: Deploy to GitHub Pages
    uses: peaceiris/actions-gh-pages@v3
    with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./build

This will publish the contents of the build directory to GitHub Pages.

    name: Deploy

    on:
        push:
            branches:
                - master

    jobs:
        build:
            runs-on: ubuntu-latest
            steps:
                - uses: actions/setup-node@v1
                 with:
                    node-version: 12
                - run: npm install
                - run: npm run build
                - run: npm test
                - name: Deploy to GitHub Pages
                uses: peaceiris/actions-gh-pages@v3
                with:
                    github_token: ${{ secrets.GITHUB_TOKEN }}
                    publish_dir: ./build

# Environments

In GitHub Actions, environments are a way to define a set of variables that can be used in your workflow. 

They are useful for storing information such as API keys, connection strings, or other secrets that your workflow needs to use.
Environments can be defined in your repository and then referenced in your workflow file.

To create an environment in your repository, go to the "Actions" tab, then click on the "Environments" link in the left sidebar. From here, you can create a new environment by clicking the "New environment" button. You can then give your environment a name and define the variables that should be included in the environment.

Once you have defined an environment, you can use it in your workflow by using the env keyword and the name of the environment.

For example:

    jobs:
        build:
            runs-on: ubuntu-latest
            env:
                MY_SECRET: ${{ env.MY_ENVIRONMENT_NAME }}
            steps:
                - run: echo "The value of MY_SECRET is $MY_SECRET"

Environments are a great way to separate sensitive information from your code and keep it secure. They are also useful for managing different configurations for different environments, such as staging and production environments.

## Protection rules

Protection rules in GitHub are a way to ensure that certain actions cannot be performed on a repository unless certain conditions are met. 

For example, you might want to require that all pull requests be reviewed by at least one other person before they can be merged, or that all pushes to the **master** branch must be made by a designated group of maintainers.

To create protection rules for a repository, go to the "Settings" tab of the repository, then click on the "Branches" link in the left sidebar. From here, you can choose a branch for which you want to set protection rules, and then click the "Add rule" button. You can then specify the conditions that must be met before certain actions can be performed on the branch.

Some common protection rules include:

- Requiring a certain number of approving reviews on pull requests

- Requiring that pull requests be up to date with the target branch before they can be merged

- Requiring that only certain users or teams can push to the branch

- Enabling status checks and requiring that all checks pass before a pull request can be merged


