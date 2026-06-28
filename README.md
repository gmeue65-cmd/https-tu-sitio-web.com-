https-tu-sitio-web.com
The Kubernetes documentation
Netlify Status GitHub release

This repository contains the assets required to build the Kubernetes website and documentation. We're glad that you want to contribute!

Contributing to the docs
Localization READMEs
Using this repository
You can run the website locally using Hugo (Extended version), or you can run it in a container runtime. We strongly recommend using the container runtime, as it gives deployment consistency with the live website.

Prerequisites
To use this repository, you need the following installed locally:

npm
Go
Hugo (Extended version)
A container runtime, like Docker.
Note

Make sure to install the Hugo extended version specified by the HUGO_VERSION environment variable in the netlify.toml file.

Before you start, install the dependencies. Clone the repository and navigate to the directory:

git clone https://github.com/kubernetes/website.git
cd website
The Kubernetes website uses the Docsy Hugo theme, which can be installed via npm. You can also download a pre-configured development container image that includes Hugo and Docsy. Additionally, a Git submodule is used for tools that generate the reference documentation.

Windows
# fetch submodule dependencies
git submodule update --init --recursive --depth 1
Linux / other Unix
# fetch submodule dependencies
make module-init
Running the website using a container
To build the site in a container, run the following:

# You can set $CONTAINER_ENGINE to the name of any Docker-like container tool

# Render the full website
make container-serve

# Render only a specific language segment (e.g., English)
make container-serve segments=en

# Render multiple languages (e.g., English and Korean)
make container-serve segments=en,ko
💡 Tip: Using Hugo segments speeds up local preview builds, by rendering only selected language(s).

If you see errors, it probably means that the Hugo container did not have enough computing resources available. To solve it, increase the amount of allowed CPU and memory usage for Docker on your machine (macOS and Windows).

Open up your browser to http://localhost:1313 to view the website. As you make changes to the source files, Hugo updates the website and forces a browser refresh.

Running the website locally using Hugo
To install dependencies, deploy and test the site locally, run:

For macOS and Linux

npm ci

# Render the full site (default)
make serve

# Render only a specific language segment
make serve segments=en

# Render multiple language segments
make serve segments=en,ko
💡 Tip: Hugo segments are defined in hugo.toml and allow faster rendering by limiting the scope to specific language(s).

For Windows (PowerShell)

npm ci
hugo.exe server --config hugo.toml,hugo.server.toml --buildFuture --environment development
This will start the local Hugo server on port 1313. Open up your browser to http://localhost:1313 to view the website. As you make changes to the source files, Hugo updates the website and forces a browser refresh.

Building the API reference pages
The API reference pages located in content/en/docs/reference/kubernetes-api are built from the Swagger specification, also known as OpenAPI specification, using https://github.com/kubernetes-sigs/reference-docs/tree/master/gen-resourcesdocs.

To update the reference pages for a new Kubernetes release follow these steps:

Pull in the api-ref-generator submodule:

git submodule update --init --recursive --depth 1
Update the Swagger specification:

curl 'https://raw.githubusercontent.com/kubernetes/kubernetes/master/api/openapi-spec/swagger.json' > api-ref-assets/api/swagger.json
In api-ref-assets/config/, adapt the files toc.yaml and fields.yaml to reflect the changes of the new release.

Next, build the pages:

make api-reference
You can test the results locally by building and serving the site from a container:

make container-serve
In a web browser, go to http://localhost:1313/docs/reference/kubernetes-api/ to view the API reference.

When all changes of the new contract are reflected into the configuration files toc.yaml and fields.yaml, create a Pull Request with the newly generated API reference pages.

Troubleshooting
If you experience any issues with running website locally, please refer to the Troubleshooting section of the contributing documentation.

Get involved with SIG Docs
Learn more about SIG Docs Kubernetes community and meetings on the community page.

You can also reach the maintainers of this project at:

Slack
Get an invite for this Slack
Mailing List
Contributing to the docs
You can click the Fork button in the upper-right area of the screen to create a copy of this repository in your GitHub account. This copy is called a fork. Make any changes you want in your fork, and when you are ready to send those changes to us, go to your fork and create a new pull request to let us know about it.

Once your pull request is created, a Kubernetes reviewer will take responsibility for providing clear, actionable feedback. As the owner of the pull request, it is your responsibility to modify your pull request to address the feedback that has been provided to you by the Kubernetes reviewer.

Also, note that you may end up having more than one Kubernetes reviewer provide you feedback or you may end up getting feedback from a Kubernetes reviewer that is different than the one initially assigned to provide you feedback.

Furthermore, in some cases, one of your reviewers might ask for a technical review from a Kubernetes tech reviewer when needed. Reviewers will do their best to provide feedback in a timely fashion but response time can vary based on circumstances.

For more information about contributing to the Kubernetes documentation, see:

Contribute to Kubernetes docs
Page Content Types
Documentation Style Guide
Localizing Kubernetes Documentation
Introduction to Kubernetes Docs
New contributor ambassadors
If you need help at any point when contributing, the New Contributor Ambassadors are a good point of contact. These are SIG Docs approvers whose responsibilities include mentoring new contributors and helping them through their first few pull requests. The best place to contact the New Contributors Ambassadors would be on the Kubernetes Slack. Current New Contributors Ambassadors for SIG Docs:

Name	Slack	GitHub
Sreeram Venkitesh	@sreeram.venkitesh	@sreeram-venkitesh
Localization READMEs
Language	Language
Bengali	Korean
Chinese	Polish
French	Portuguese
German	Russian
Hindi	Spanish
Indonesian	Ukrainian
Italian	Vietnamese
Japanese	
Code of conduct
Participation in the Kubernetes community is governed by the CNCF Code of Conduct.

Thank you
Kubernetes thrives on community participation, and we appreciate your contributions to our website and our documentation!