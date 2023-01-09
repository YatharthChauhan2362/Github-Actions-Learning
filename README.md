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






