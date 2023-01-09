**Github Actions CI/CD**

## Github Actions

GitHub Actions are automated processes that you can set up in your repository to build, test, package, release, or deploy your code. You can use them to automate your workflow and add custom behaviors to your repository.

Here is an example of a GitHub Action that deploys a static website to GitHub Pages:

## Github Workflows

GitHub Workflows are a way to automate tasks that you use in your software development workflows. Workflows are made up of individual Jobs, which are defined by a series of steps. Each step in a job can run a script, an action, or an external command. 

- Workflows can be triggered by a variety of events, such as pushes to a repository, the creation of a pull request, or the opening of an issue.

- GitHub Workflows are automated processes that you can set up in your repository to build, test, package, release, or deploy any code project on GitHub. You can create Workflows by defining them in a .github/workflows directory in your repository.

1. Build and test: This Workflow could be triggered whenever you push new code to your repository. It could run your test suite to ensure that the code is working as expected, and then build a production-ready version of your code.

2. Release: This Workflow could be triggered whenever you create a new release tag in your repository. It could build and package your code, and then upload the package to a package repository or a deployment service.

3. Deploy: This Workflow could be triggered whenever you push new code to a specific branch (e.g. production). It could build and package your code, and then deploy it to your production environment.

Here are a few examples of Workflows that you could use:

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






