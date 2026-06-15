# Information on how Github is administered and managed within CDL

> [!Note]
> This information to move into the CDL User Guides Repo that is maintained by IAS once the GitHub working group has this document in a more final state.

## What GitHub Account Should I use for my work at CDL?

GitHub accounts are stongly tied to individual emails.  

The use of shared/administrative accounts in actively discouraged by GitHub through multi-factor authentication policies.

GitHub organization policies should be created with an assumption that multiple individual users will adminster policies.  These users should be removed from the GitHub organization when the users separate from CDL.

### Options
- Re-use a pre-existing GitHub account
  - Many CDL developers have chosen this option in order to showcase a portfolio of work before and after joining CDL. 
- Create a new GitHub account dedicated for my work at CDL
  - Many CDL staff have chosen this option as well. 
- Create a separate GitHub account in order to administer a GitHub organization
  - Our CDL Systems Adminstrators have chosen this option for administering GitHub.
  - This requires the use of a secondary email or an email alias.
 
### Server-based deployments 
- Create a [machine user](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys#machine-users)

## What email(s) should I associate with my GitHub account

A GitHub account can be configured with multiple email addresses.  

We recommend that you associate your UCOP email address with the GitHub account that you use for your work at CDL.

## Multi-factor authentication (MFA) Requirement
All CDL Github users are required to enable MFA.  These can be configured in your [account security settings](https://github.com/settings/security).   
It is recommended to enable (2) two-factor methods.  Selecting 2 methods provides a backup method if one method is unavailable.  It is not recommended to use SMS as this is an insecure method.  

## Performing Git operations using my GitHub account

Many Git/GitHub operations can be performed within the GitHub web interface.
- Create issues
- Comment on issues
- Create pull requests
- Merge pull requests
- View Code
- Edit Code - this option is ok for simple edits to a single file

For work that you perform on your desktop or on a CDL server, you will likely need to authorize a **git client** to use your GitHub credentials.
- pull code from a public repo - no authorization is needed
- pull code from a private repo - authorization is needed
- push code to a repo (public or private) - authorization is needed

### Examples of a Git Client
- GitHub desktop
- VSCode
- [`git`](https://cli.github.com) command line tool

### Authorizing a Git Client
> [!NOTE]
> GitHub no longer allows you to use your GitHub password to authorize a git client.

Authorization Options
- #### GitHub Desktop
  - in this instance, the url to your repo will look like `https://github.com...` 
  - when you attempt to clone a private repository, GitHub desktop will prompt you for authentication on GitHub.com
  - GitHub desktop relies on an active web connection to GitHub.com
- #### `git` command line client
  - in this instance, the url to your repo will look like `https://github.com...` 
  - when you attempt to clone a private repository, the git tool will prompt you for a username/password
    - the username does not matter
    - for the password, provide a GitHub personal access token
      - GitHub fine-grained personal access tokens have an expiration date and will require periodic regeneration
- #### Configure an ssh key
  - in this instance, the url to your repo will look like `git@github.com...`
  - from **your desktop**, you must create an ssh key using a command line tool such as `ssh-keygen` and name it something like `~/.ssh/github_rsa`
  - you must load your PUBLIC ssh key to your GitHub account
    - Settings / SSH and GPG Keys
    - Note that SSH keys have no expiration on GitHub
  - you must add the following to your `~/.ssh/config`
  - when connecting to a CDL server, it is recommended that you forward your ssh credentials to the server rather than duplicating your ssh key on the server.
    - `ssh -A` 
```
Host github.com
	HostName github.com
	User git
	IdentityFile ~/.ssh/github_rsa
```

### GitHub Access Tokens vs SSH Keys

- GitHub Access Tokens
  - Access rights can be revoked at any time 
  - Can be configured with an expiration
  - Access rights can be scoped to particular behaviors
  - Can perform git operations (clone/push/pull)
  - Can perform GitHub API operations
- SSH Keys
  - Access rights can be revoked at any time
  - Cannot be configured with an expiration
  - Can be "forwarded" to a server
  - Can perform git operations (clone/push/pull)
  - Cannot perform GitHub API operations

## What Type of Billing Plan should my GitHub account have?

GitHub offers 3 types of plans
- Personal
- Pro
- Enterprise

Due to cost, CDL does not have an enterprise plan. 
Most CDL users have been able to qualify for a free pro account using [GitHub for Education](https://github.com/education) benefits.

## What is a GitHub Organization?  How does CDL utilize GitHub Organizations?
Github organizations are for teams operating shared code and policies. Each CDL program typically has it's own organization.  
Examples:
- [UC Curation Center](https://github.com/CDLUC3)
- [PAD Archives](https://github.com/ucldc)
- [PAD Publishing](https://github.com/eScholarship/)


## What is a Github Team?
Within each organization there are teams. A GitHub team is a subgroup inside an organization used to manage repo-level access.  A member can belong to many teams.

## I need to create a new repo, which organization should I use?
If it is a repo that all of CDL would benefiit from, use CDLIB Organization, otherwise it probably works best in your program's organization or in cases with new projects/partnerships, create a new organization.

## I need to create a new repo, should it be public or private?
Repositories should be private by default. Make a repository public only when there is a clear need for open source, open collaboration, or public documentation, and only after confirming that it contains no sensitive or internal process details/content.

## What content should *never* be stored it git (even in a private repo?)
Secrets and credentials (API keys & tokens, passwords, private keys, connection strings)
Sensitive Data (env vars, configuration files with secrets, PII date)

## What CI/CD tools should I utilize with my repository?
Options
- GitHub actions
- AWS CodePipeline
- Jenkins

## When should I authorize an application to access my GitHub repo?
Applications may be authorized only for approved use, with least-privilege access, scoped repository permissions, and periodic review by organization administrators.Use cases examples include CI/CD and backups.

## GitHub Apps
We should be very selecitve about the apps that are approved at an Org level.

This is the primary mechanism that we use to enable AWS Code Build/Pipeline tools to access GitHub events.

<img width="1096" alt="image" src="https://github.com/user-attachments/assets/b3c46347-d978-4cdc-99d1-cbf949f0798d" />

## When should I create an Access Token?
- Access tokens can be created to authorize a github client (as a login credential)
- Access tokens can be used to authorize a script to perform git operations
- Access tokens can be used to authorize a program to make GitHub api calls

## What type of access token should I use?
Access token creation is configured under **Settings/Developer Settings/Personal Access Tokens**.

If the creator of an access token is not a GitHub Organization owner, the token must be approved by a GitHub Organization Owner before it can be used.

An organization owner can revoke fine-graned tokens that have been granted organization access rights.

### Options
- Classic token (`ghp...`)
  - can be configured with/without an expiration
  - permission scopes are too broad and generally grant more rights than is desireable.
- Fine-grained Access Token (`github_pat_...`)
  - users are discourged from creating one without an expiration
  - access rights can be scoped
    - to particular github apis
    - to particular repositories
    - to a particular organization

> [!NOTE]
> At this time, CDL recommends the use of fine-grained access tokens

### Access Token Alternatives
- SSH keys
- GitHub Apps

## How can I access the GitHub api?
[API Reference](https://docs.github.com/en/developers)

## Which GitHub api should I use?

Options
- GraphQL
- API

CDL uses the Github API for Disaster Recovery to backup repositories to external storage areas.  


## Can we use GitHub Codespaces?
CDL doesn't utilize these due to costs and alternative options such as Docker.

## Best Practices

### Developer Best Practices

#### What collaboration settings are recommended for my new GitHub repo?
Use protected default branches with required PR reviews, required passing checks, least-privilege permissions, and mandatory security scanning for all repositories.

Each repository should have at least 1 admin assigned to it to manage access.

### GitHub Notifications Best Practices
Github notifications can be quite noisy.  Some teams utilize Slack-Github integration for repositories they watch.  

#### Forking CDL repositories

#### Signed Commits

### Organization Admin Best Practices
At least 2 members should be assigned as an organizational admin.  Create an admin account and assign it as an owner. You can use the + email trick to create a separate account for this.  (ex: johndoe+gh-adming@ucop.edu). This user can approve Github app connections, access tokens, manage members, and have access to all repositories in the organization.

### Product/Project Management Best Practices
Most teams at CDL utilize Github Project Boards to manage agile development.  Project Boards are very flexible, supporting many views and configurations to track work across a single or multiple repositories. They are typically set to private since they track internal work.  Examples of public Github Project Boards can be found here: 
- [CDLUC3 Public Projects](https://github.com/orgs/CDLUC3/projects)
- [ROR Community Roadmap](https://github.com/orgs/ror-community/projects/17)

## How do our teams use CoPilot?  ###
CDL Users that have Pro accounts via Github Education, were able to request Github CoPilot for free.  As of June 1, 2026 [Github transitioned CoPilot to usage-based billing](https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/).  As a result of that, Github [paused signups for CoPilot](https://github.blog/news-insights/company-news/changes-to-github-copilot-individual-plans/).  Users which already have CoPilot can continue to use it until they reach their usage limit each month.  Teams find Github CoPilot beneficial utilizing within the browser, helping to write unit tests, review PRs, and embed within their IDE of choice. 

## Github is a dynamic platform.  How can I stay up-to-date with changes?
Read the [Github Blog](https://github.blog/) for news and updates and [subscribe to the Github Newsletter](https://github.com/newsletter/) for developer updates. [Github Status](https://www.githubstatus.com/) reports performance and issues with certain Github services. 