authenticate with GitHub Package Registry or using a .npmrc file. See "Configuring npm for use with GitHub Package Registry."

$ npm install @codertocat/hello-world-npm

Or add this package to your package.json file:

"dependencies": {
    "@codertocat/hello-world-npm": "1.0.0"
  }

package.json

$ npm install @codertocat/hello-world-npm@1.0.1
Install via package.json:
"@codertocat/hello-world-npm": "1.0.1"

GitHub Docs

Working with the npm registry

Free, Pro, & Team

In this article

Limits for published npm versions

Authenticating to GitHub Packages

Publishing a package

Publishing multiple packages to the same repository

Installing a package

Further reading

You can configure npm to publish packages to GitHub Packages and to use packages stored on GitHub Packages as dependencies in an npm project.

GitHub Packages is available with GitHub Free, GitHub Pro, GitHub Free for organizations, GitHub Team, GitHub Enterprise Cloud, GitHub Enterprise Server, and GitHub AE.
















GitHub Packages is not available for private repositories owned by accounts using legacy per-repository plans. Also, accounts using legacy per-repository plans cannot access the Container registry since these accounts are billed by repository. For more information, see "GitHub's products."

Limits for published npm versions

If you publish over 1,000 npm package versions to GitHub Packages, you may see performance issues and timeouts occur during usage.

In the future, to improve performance of the service, you won't be able to publish more than 1,000 versions of a package on GitHub. Any versions published before hitting this limit will still be readable.

If you reach this limit, consider deleting package versions or contact Support for help. When this limit is enforced, our documentation will be updated with a way to work around this limit. For more information, see "Deleting and restoring a package" or "Contacting Support."

Authenticating to GitHub Packages

You need an access token to publish, install, and delete packages.

You can use a personal access token (PAT) to authenticate to GitHub Packages or the GitHub API. When you create a personal access token, you can assign the token different scopes depending on your needs. For more information about packages-related scopes for a PAT, see "About permissions for GitHub Packages."

To authenticate to a GitHub Packages registry within a GitHub Actions workflow, you can use:

GITHUB_TOKEN to publish packages associated with the workflow repository.

a PAT to install packages associated with other private repositories (which GITHUB_TOKEN can't access).

For more information about GITHUB_TOKEN used in GitHub Actions workflows, see "Authentication in a workflow."

Authenticating with a personal access token

You must use a personal access token with the appropriate scopes to publish and install packages in GitHub Packages. For more information, see "About GitHub Packages."

You can authenticate to GitHub Packages with npm by either editing your per-user ~/.npmrc file to include your personal access token or by logging in to npm on the command line using your username and personal access token.

To authenticate by adding your personal access token to your ~/.npmrc file, edit the ~/.npmrc file for your project to include the following line, replacing TOKEN with your personal access token. Create a new ~/.npmrc file if one doesn't exist.

//npm.pkg.github.com/:_authToken=TOKEN

To authenticate by logging in to npm, use the npm login command, replacing USERNAME with your GitHub username, TOKEN with your personal access token, and PUBLIC-EMAIL-ADDRESS with your email address.

If GitHub Packages is not your default package registry for using npm and you want to use the npm audit command, we recommend you use the --scope flag with the owner of the package when you authenticate to GitHub Packages.

$ npm login --scope=@OWNER --registry=https://npm.pkg.github.com > Username: USERNAME > Password: TOKEN > Email: PUBLIC-EMAIL-ADDRESS

Publishing a package

Note: Package names and scopes must only use lowercase letters.

By default, GitHub Packages publishes a package in the GitHub repository you specify in the name field of the package.json file. For example, you would publish a package named @my-org/test to the my-org/test GitHub repository. You can add a summary for the package listing page by including a README.md file in your package directory. For more information, see "Working with package.json" and "How to create Node.js Modules" in the npm documentation.

You can publish multiple packages to the same GitHub repository by including a URL field in the package.json file. For more information, see "Publishing multiple packages to the same repository."

You can set up the scope mapping for your project using either a local .npmrc file in the project or using the publishConfig option in the package.json. GitHub Packages only supports scoped npm packages. Scoped packages have names with the format of @owner/name. Scoped packages always begin with an @ symbol. You may need to update the name in your package.json to use the scoped name. For example, "name": "@codertocat/hello-world-npm".

After you publish a package, you can view the package on GitHub. For more information, see "Viewing packages."

Publishing a package using a local .npmrc file

You can use an .npmrc file to configure the scope mapping for your project. In the .npmrc file, use the GitHub Packages URL and account owner so GitHub Packages knows where to route package requests. Using an .npmrc file prevents other developers from accidentally publishing the package to npmjs.org instead of GitHub Packages.

Authenticate to GitHub Packages. For more information, see "Authenticating to GitHub Packages."

In the same directory as your package.json file, create or edit an .npmrc file to include a line specifying GitHub Packages URL and the account owner. Replace OWNER with the name of the user or organization account that owns the repository containing your project.

@OWNER:registry=https://npm.pkg.github.com

Add the .npmrc file to the repository where GitHub Packages can find your project. For more information, see "Adding a file to a repository."

Verify the name of your package in your project's package.json. The name field must contain the scope and the name of the package. For example, if your package is called "test", and you are publishing to the "My-org" GitHub organization, the name field in your package.json should be @my-org/test.

Verify the repository field in your project's package.json. The repository field must match the URL for your GitHub repository. For example, if your repository URL is github.com/my-org/test then the repository field should be git://github.com/my-org/test.git.

Publish the package:

$ npm publish

Publishing a package using publishConfig in the package.json file

You can use publishConfig element in the package.json file to specify the registry where you want the package published. For more information, see "publishConfig" in the npm documentation.

Edit the package.json file for your package and include a publishConfig entry.

"publishConfig": { "registry":"https://npm.pkg.github.com" },

Verify the repository field in your project's package.json. The repository field must match the URL for your GitHub repository. For example, if your repository URL is github.com/my-org/test then the repository field should be git://github.com/my-org/test.git.

Publish the package:

$ npm publish

Publishing multiple packages to the same repository

To publish multiple packages to the same repository, you can include the URL of the GitHub repository in the repository field of the package.json file for each package.

To ensure the repository's URL is correct, replace REPOSITORY with the name of the repository containing the package you want to publish, and OWNER with the name of the user or organization account on GitHub that owns the repository.

GitHub Packages will match the repository based on the URL, instead of based on the package name.

"repository":"https://github.com/OWNER/REPOSITORY",

Installing a package

You can install packages from GitHub Packages by adding the packages as dependencies in the package.json file for your project. For more information on using a package.json in your project, see "Working with package.json" in the npm documentation.

By default, you can add packages from one organization. For more information, see "Installing packages from other organizations."

You also need to add the .npmrc file to your project so that all requests to install packages will go through GitHub Packages. When you route all package requests through GitHub Packages, you can use both scoped and unscoped packages from npmjs.org. For more information, see "npm-scope" in the npm documentation.

Authenticate to GitHub Packages. For more information, see "Authenticating to GitHub Packages."

In the same directory as your package.json file, create or edit an .npmrc file to include a line specifying GitHub Packages URL and the account owner. Replace OWNER with the name of the user or organization account that owns the repository containing your project.

@OWNER:registry=https://npm.pkg.github.com

Add the .npmrc file to the repository where GitHub Packages can find your project. For more information, see "Adding a file to a repository."

Configure package.json in your project to use the package you are installing. To add your package dependencies to the package.json file for GitHub Packages, specify the full-scoped package name, such as @my-org/server. For packages from npmjs.com, specify the full name, such as @babel/core or @lodash. For example, this following package.json uses the @octo-org/octo-app package as a dependency.

{ "name": "@my-org/server", "version": "1.0.0", "description": "Server app that uses the @octo-org/octo-app package", "main": "index.js", "author": "", "license": "MIT", "dependencies": { "@octo-org/octo-app": "1.0.0" } } 

Install the package.

$ npm install

Installing packages from other organizations

By default, you can only use GitHub Packages packages from one organization. If you'd like to route package requests to multiple organizations and users, you can add additional lines to your .npmrc file, replacing OWNER with the name of the user or organization account that owns the repository containing your project.

@OWNER:registry=https://npm.pkg.github.com @OWNER:registry=https://npm.pkg.github.com

Further reading

"Deleting and restoring a package"

Did this doc help you?

Privacy policy

Help us make these docs great!

All GitHub docs are open source. See something that's wrong or unclear? Submit a pull request.

Make a contribution

Or, learn how to contribute.

Still need help?

Ask the GitHub community

Contact support

© 2021 GitHub, Inc.

Terms

Privacy

Security

Status

Help

Contact GitHub

Pricing

Developer API

Training

Blog

About


