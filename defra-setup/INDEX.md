# Defra Developer Config Guide
## Summary
This document details the set-up of a MacBook to use for software development within the FCP (or FFC) under Defra. The original guide detailing the set-up can be found on [Defra's official GitHub](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/index.md). Use the original guide as the main set of instructions and only refer to this guide for troubleshooting. The following information is simply the documentation of my own set-up across multiple Defra issues Macbooks. Spoiler alert, Homebrew solved a lot of problems ([installing Homebrew](https://brew.sh/) should probably be the first thing you do, alongside making sure your Mac has the latest MacOS updates). [I created some scripts](https://github.com/rtasalem/dffc-mac-scripts) (which are still a WIP!) to help install *most* (not all) of the packages that are listed in the FFC local development guide to cut down on time finding installation commands.
***
## Contents (when you arrive at one of the sections listed below, click on the section heading to be directed to the corresponding instructions within Defra's set up guide)
1. [Developer Tools](#developer-tools)
2. [Docker Desktop](#docker-desktop)
3. [Signing Commits](#signing-commits-aka-ensuring-your-commits-on-github-have-the-verified-tag-next-to-your-username)
4. [Visual Studio Code](#visual-studio-code)
5. [SonarLint](#sonarlint)
6. [Docker Compose](#docker-compose)
7. [detect-secrets](#detect-secrets)
8. [Node Version Manager (NVM)](#node-version-manager-nvm)
9. [StandardJS](#standardjs)
10. [.NET SDK](#net-sdk)
11. [kubectl](#kubectl)
12. [Helm](#helm)
13. [Azure CLI](#azure-cli)
14. [Snyk CLI](#snyk-cli)
15. [GitHub CLI](#github-cli)
16. [OpenVPN](#openvpn)
17. [Other](#other):
    - [Another Redis Desktop](#another-redis-desktop-manager)
    - [Microsoft Azure Storage Explorer](#microsoft-azure-storage-explorer)
    - [GraphQL Syntax Highlighting](#graphql-syntax-highlighting)
    - [Jenkins](#jenkins)
    - [Lens](#lens)
    - [env Set-up](#env-set-up)
    - [yq](#yq)
    - [NPM Package Version Prefix](#npm-package-version-prefix)
    - [Azure Data Studio](#azure-data-studio)
    - [SSH Key](#ssh-key)
***
## [Developer Tools](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/setup-macos-command-line-tools.md)
### Instructions
- Open the `terminal` and run the following command: 
```
xcode-select --install
````
- A pop-up window will appear stating that the `xcode-select` command requires the command line developer tools, click install and wait for the process to finish.
- Run the command again to verify installation. The output should say something along the lines of `Command line tools are already installed...`.
### Comments
- This one may take a wee while.
***
## [Docker Desktop](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-docker-desktop.md)

### Instructions
- [Download Docker Desktop for Mac](https://docs.docker.com/desktop/install/mac-install/).
### Comments
- If your Mac is not fully updated to the latest OS, then Docker Desktop may not open. Open `System Settings` and begin the OS update (this step can take a while, but Docker Desktop should be able to open just fine afterwards).
- An alternative to Docker Desktop is [Rancher Desktop](https://rancherdesktop.io/).
***
## [Signing Commits (a.k.a ensuring your commits on GitHub have the Verified tag next to your username)](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/sign-commits.md)
### Instructions
- Follow the instructions in the guide as is.
### Comments
- Test that your commits are being signed by creating a dummy repo and pushing to that repo (or just make a commit to any draft/open PR on any repo).
- If for whatever reason commits are not shown as `Verified` on GitHub, don't fret, the same happened to me. Here's what I did:
	- Some frantic Googling, which led me to [the answer](https://dev.to/devmount/signed-git-commits-in-vs-code-36do).
	- In the above link, skip to the section titled *Set up GitHub*. It explains that you can tell Git your GPG key ID. First, get the ID of the GPG key you just created using this command:
```
gpg --list-secret-keys --keyid-format=long
```
- In the following example the GPG key ID is `3AA5C34371567BD2`:
		  ![gpg-key-id-example.png](pngs/gpg-key-id-example.png)
- Take this ID and run the following commands:
```
git config --global user.signingkey 3AA5C34371567BD2
git config --global commit.gpgsign true
```
- Note that when I was setting up the second Mac, commit signing didn't work after using the two commands above. Needed to set the global name and email for Git:
```
git config --global user.name "<first-and-last-name>"
git config --global user.email "<email-address>"
```
- Once I had set global config for Git, I ran the two commands (here referring to the `git config --global user.signingkey...` and `git config --global commit.gpgsign true` commands) and once I tested my commit signing (through pushing to a dummy branch/PR) my commits were shown as `Verified`.
- If your commits are still not showing as `Verified`, ensure via your `settings.json` file for VS Code that you have included the follwing line:
```
"git.enableCommitSigning" : true
```
- Test your commits again and with all fingers crossed, your commits should now appear as `Verified`.
***
## [Visual Studio Code](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-vs-code.md)
### Instructions
- Follow the guide, ignore the section titled `WSL Configuration` (this applies to Windows Devices only).
### Comments
- This section has a lot of bits that need to be added to your `settings.json` file in VS Code. To find your `settings.json`, open VS Code and hit `cmd` + `,` this will open the User Settings screen. From here, click the `Open Settings (JSON)` button in the top right corner (see below).
![locating-settings-json.png](pngs/locating-settings-json.png)
- After following the entire guide, your `settings.json` should look something similar to the following:
```
{
    "javascript.validate.enable": false,
    "standard.autoFixOnSave": true,
    "standard.options": {},
    "standard.enableGlobally": true,
    "standard.validate": [
        "javascript",
        "javascriptreact",
        "typescript",
        "typescriptreact"
    ],
    "standard.nodePath": "",
    "files.autoSave": "afterDelay",
    "files.autoSaveDelay": 600,
    "editor.tabSize": 2,
    "[csharp]":{
        "editor.tabSize": 4,
    },
    "git.enableCommitSigning": true,
    "sonarlint.ls.javaHome": "/usr/local/opt/openjdk/libexec/openjdk.jdk",
    "sonarlint.connectedMode.connections.sonarcloud": [
        {
        "organizationKey": "insert-organisation-here",
        "token": "insert-token-here"
        }
    ],
    "sonarlint.rules": {
        "javascript:S4138": {
            "level": "on"
        },
    },
    "[javascript]": {
        "editor.defaultFormatter": "vscode.typescript-language-features"
    },
    "[typescriptreact]": {
        "editor.defaultFormatter": "vscode.typescript-language-features"
    },
    "editor.tokenColorCustomizations": {
        "comments": "#DAA49A"
    },
    "editor.indentSize": "tabSize",
    "javascript.updateImportsOnFileMove.enabled": "always",
    "typescript.updateImportsOnFileMove.enabled": "always",
} 
```
- Note the above example may not match your entire `settings.json` file exactly, other extensions you have installed may add further configuration settings to this file.
***
## [SonarLint](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-sonarlint.md)
### Instructions
- Instead of using `sudo apt-get install openjdk-11-jre` to install JDK (Java Development Kit), use Homebrew: `brew install openjdk`. 
	- After installing OpenJDK, run the following commands:
```
echo 'export PATH="/usr/local/opt/openjdk/bin:$PATH"' >> ~/.zshrc
sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
```
- Then run `java -version` and you should see 3 lines of output as the response, this confirms that OpenJDK was successfully installed.
- After installing the [SonarLint extension](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarlint-vscode) in VS Code, the guide mentions setting the location of the JRE (Java Runtime Environment) in your VS Code settings (i.e. the `settings.json`), but the path specified in the guide is incorrect (at least it was for me). 
- The correct path I had to use (and which I have in my `settings.json`) was:
```
"sonarlint.ls.javaHome": "/usr/local/opt/openjdk/libexec/openjdk.jdk"`
```
-  A good way of finding the path to the JRE is to open finder then `cmd` + `shift` + `G`, which will open the `Go To Folder` pop up, here you can start typing in the path e.g. `user/local/opt/openjdk...` etc. until you find the path to your JRE to include in your `settings.json`.
- Continue to follow the instructions, ignoring step 4 under the section titled *SonarLint Installation (VS Code)* as this applies to individual projects rather than your VS Code environment.
### Comments
- Ignore the section titled [*Configure Sonar for C#*](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-sonarlint.md#configure-sonar-for-c) (unless you'll be writing C#, at the time of setting up the Mac I was primarily working on a team that uses JavaScript).
- Also note that step 5 will not work if the correct location for the JRE isn't set (not 100% sure if this is a bad thing, haven't encountered any issues with it so far).
- By the end of this sections, your `setting.json` should include the following lines:
```
"sonarlint.ls.javaHome": "/usr/local/opt/openjdk/libexec/openjdk.jdk",
"sonarlint.connectedMode.connections.sonarcloud": [
  {
  "organizationKey": "defra",
  "token": "955b256f17533499a7974a94e645706cb49286e6"
  }
],
"sonarlint.rules": {
  "javascript:S4138": {
    "level": "on"
	}
}
```
- The location of the JRE might not be the same for everyone. I.e. the one I ended up using may not be (but hopefully will be) the same location on a different device.
***
## [Docker Compose](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-docker-compose.md)
### Instructions
- There aren't any instructions for this step. If you downloaded Docker Desktop, then you already have Docker Compose.
- You can verify installation using the following command:
```
docker compose version
```
***
 ## [detect-secrets](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-detect-secrets.md)
### Instructions
- Follow the original guide as described.
### Comments
- Note that once Python is installed, Pip is also automatically installed as well.
- At first thought I did not properly install Python as the `python --version` command was not showing the version post-installation, but actually the correct command to run was `python3 --version` (i.e. version 3 of Python). Same issue occurred with Pip, had to run the version command as `pip3 --version` (worth noting that in some cases just running `pip --version` does still work).
- After using Homebrew to install pre-commit, verify installation by running `pre-commit --version`.
- Generally if there are any installation issues during this step, just use Homebrew.
- Open terminal, run the following command to verify installation: `detect-secrets --version`.
***
## [Node Version Manager (NVM)](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-node-version-manager.md)
### Instructions
- Personally, I just used [Homebrew to install NVM](https://formulae.brew.sh/formula/nvm).
- If Homebrew doesn't work (which was the case when I got a second Mac to replace my first one), then just run the curl command provided on the `nvm` repo which is where the original Defra guide directs you to.
### Comments
- Open terminal, run the following command to verify installation:
```
nvm -v
```
- If after running the `curl` command you get `command not found: nvm` as a response, load up your root directory, create a file called `.zshrc` (use the command: `touch .zshrc` and gain ensure you are `cd`-ed into the root directory). Once you've created this file, open it using TextEdit and paste in the following:
```
export NVM_DIR="$HOME/.nvm
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
- The reason for needing to do this is because your terminal isn't loading `nvm` automatically whenever you open a new terminal session, by having the above script in your `.zshrc` file (which you can think of as a terminal config/profile), `nvm` will now be accessible and running the above version command should now work.
- Use NVM to install Node.js and NPM. This is highly recommended as installing Node.js and NPM this way prevents permission issues/blockers that other ways of installing often introduce (e.g. installing Node.js & NPM from the web or using Homebrew resulted in not being able to globally install certain NPM packages).
- Run the command `nvm ls-remote` to list all the current versions of Node.js. Find the latest version with LTS (Long Term Support) written next to it, this is the version you'll want to install.
- Run the install command: `nvm install --lts` to install the latest LTS version.
- Note that installing Node.js also installs NPM (run both `node -v` and `npm -v` to verify both were installed).
- If in future you come across any issues with install a new LTS version e.g. for myself, I've found that trying to install the `lts` version at any point after the initial installation that a new terminal session would show the previous version I had been using. For this I would recommend that you uninstall `nvm` by removing the `.nvm` file from your root directory and also remove the above lines from your `.zshrc` profile and then do a fresh reistall of `nvm` altogther.
***
## [StandardJS](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-standard-js.md)
### Instructions
- Follow the guide as is.
### Comments
- If permission issues are encountered when installing the StandardJS NPM package, that is most likely because of the way Node.js & NPM were installed on the machine. The best approach for installing Node.js & NPM is to use NVM (see [previous section on NMV](#node-version-manager-nvm) for instructions).
- To see a full list of globally installed NPM packages, use the following command:
```
npm ls -g
```
- Additionally, can also verify StandardJS was installed by checking the version (although the previous command will also show the version of all globally installed packages):
```
standard --version
```

***
## [.NET SDK](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-dotnet-sdk.md)
### Instructions
- Follow the guide as is.
### Comments
- Just like in the guide, verify the installation by opening terminal and running
```
dotnet --version
```
- Run the final command in the guide as a finishing step to installing .NET SDK:
```
dotnet tool install --global dotnet-ef
```
- You can verify the previous command successfully installed .NET tools:
```
dotnet-ef --version
```
***
## [kubectl](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-kubectl.md)
### Instructions
- In the instructions, Homebrew was one of the recommendations for [installing kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/#install-with-homebrew-on-macos), this is what I used. 
### Comments
- Verify installation by running the following command:
```
kubectl version
```
- Note that the instructions mention running the command `kubectl version -client`, but running the above command will list the client version regardless and will provide additional information too.
- If the output from `kubectl version` mentions that connection to the server is unsuccessful, this is likely because your OpenVPN is not switched on (you should see a different terminal output *without* the mention of an unsuccessful server connection).
***
## [Helm](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-helm.md)
### Instructions
- Again, Homebrew was one of the recommendations for [installing Helm](https://helm.sh/docs/intro/install/#through-package-managers).
### Comments
- Verify the installation by running the following command:
```
helm version
```
***
## [Azure CLI](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-azure-cli.md)
### Instructions
- Once again, Homebrew can be used to install [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-macos).
- Log in to Azure Tenant using the command provided in the guide via your terminal. 
- You'll need to get your credentials from CCoE (Cloud Centre of Excellence) - a ServiceNow request will need to be raised.
### Comments
- Verify installation using the following command:
```
az version
```
***
## [Snyk CLI](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-snyk.md)
### Instructions
- No surprise, you can [install the Snyk CLI using Homebrew](https://docs.snyk.io/snyk-cli/install-or-update-the-snyk-cli#install-with-homebrew-macos-linux).
### Comments
- Run the following command to verify installation:
```
snyk --version
```
***
## [GitHub CLI](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-github.md)
### Instructions
- Yes, of course you can [install the GitHub CLI using Homebrew](https://github.com/cli/cli).
### Comments
- Verify installation by running the following command:
```
gh --version
```
***
## [OpenVPN](https://github.com/DEFRA/ffc-development-guide/blob/main/docs/local-development-setup/install-openvpn.md)
### Instructions
- Run the following commands:
```
brew install openvpn
```
- You will need to get your OpenVPN credentials from the CCoE:
	1. Navigate to the OpenVPN link provided in the email.
	2. You'll see a login page, select `Sign In via SAML`.
	3. Enter your Defra credentials.
	4. Most likely a MFA prompt will pop-up, complete this.
	5. Once authenticated, you will be able to download the latest VPN client software i.e. OpenVPN Connect, download the version under the heading `Recommended for your device`.
	6. Launch the installed OpenVPN Connect app, you'll see a pop-up showing your Defra VPN profile.
	7. Next to your name/credentials there will be a on/off toggle, toggle this on.
	8. If it appears to be taking some time to connect to OpenVPN, click the menu icon in the top left (this will appear as 3 stacked horizontal lines) and if you see an option to install the latest OpenVPN update, do this.
	9. Once the update is installed, try again to turn on the connection and this should get you connected a lot faster.
	10. Now you're all connected with OpenVPN and there's nothing left to do.
### Comments
- Verify installation of OpenVPN using:
```
openvpn --version
```
- If OpenVPN isn't connecting, repeat steps 1-10 above (note you may not need to update to the latest version) and the VPN should now connect.
- Note that you will not be able to log into the Azure Portal/view resources if OpenVPN is not first installed and connected.
***
## Other
Below this point is other additional config that I've done for my Mac that is not in the original guide.
***
## Another Redis Desktop Manager
- Installed when building a POC (proof of concept) for FFD (now known as SFD), didn't really use it but worth keeping in mind since some SFD services will use/are using Redis.
### Instructions
- [Download from GitHub](https://github.com/qishibo/AnotherRedisDesktopManager) (includes the Homebrew command for installation).
***
## Microsoft Azure Storage Explorer
- Recommended by the lead developer while going through different FFD repositories, later became relevant when the team was developing a solution for uploading/storing documents using Azure Storage Accounts.
### Instructions
- [Download from Microsoft](https://azure.microsoft.com/en-gb/products/storage/storage-explorer)
- Can also be installed by Homebrew: 
```
brew install --cask microsoft-azure-storage-explorer
```
***
## GraphQL Syntax Highlighting
- First used when implementing GraphQL for a couple of POCs for FFD.
### Instructions
- Install the [GraphQL: Syntax Highlighting Extension](https://marketplace.visualstudio.com/items?itemName=GraphQL.vscode-graphql-syntax) via VS Code
- To implement the extension when writing out `typeDefs` (type definitions), add `#graphql` at the top of the `typeDefs` (see example below):
![graphql-syntax-highlighting.png](pngs/graphql-syntax-highlighting.png)
***
## Jenkins
- Is needed to access CI/CD pipelines.
### Instructions
- You will need to get your Jenkins credentials from CCoE.
- In the email invite, a link will be provided to access the Jenkins dashboard.
- Enter the username and password provided in the email and you should now be able to log into the Jenkins dashboard.
- Note that logging into Jenkins will not be possible unless your OpenVPN is switched on.
***
## Lens
- Kubernetes IDE used to access pods.
### Instructions
- [Download and install Lens](https://formulae.brew.sh/cask/lens).
- Ensure that kubectl and Azure CLI have been installed (these are prerequisites and should have already been installed when going through initial Mac set-up.
- Follow the steps in the documentation (on Confluence) for connecting Lens to Kubernetes Clusters.
- You may also need to install [kubelogin](https://azure.github.io/kubelogin/install.html) to be able to properly connect to a cluster.
### Comments
- Lens is no longer an open source piece of software and therefore requires a license to use. One alternative currently being explored is [k9s](https://k9scli.io/) (has a really cool terminal UI, navigating via the keyboard can be a bit tricky to get the hand of).
***
## env Set-up
- Easy way to set up environment variables across multiple repos on a Mac.
### Instructions
- Simon D (senior developer at Defra) taught me about this one (and he learned it from Steve H, former developer at Defra).
- On Mac, you can set up [symbolic links (or symlinks)](https://www.howtogeek.com/297721/how-to-create-and-use-symbolic-links-aka-symlinks-on-a-mac/). You can set up a directory for a specific team or a set of microservices where a "master" `.env` file will be created/stored.
- E.g. for the Farming Front Door (FFD) team under the Future Farming & Countryside (FFC) programme you could name the directory `ffc-ffd-env` (Simon also showed me this naming system which works really well considering all repos under the FFD namespace are prefixed with `ffc-ffd`) and all that this directory needs to contain is a single `.env` file where we can store all the environment variables for all `ffc-ffd` microservices).
- Once you have collated all the environment variables across the set of related repos and pasted them into the master `.env`, all that's left to do is is to create the symlink in any repos where you need to include environment variables.
- The following command is used to achieve this:
```
ln -nfsv source_file link_name
```
- You would execute this command in the repo for which you want the environment variables linked with the master `.env`. As an example, here's what the command would look like if being executed from the root of the repo itself:
```
ln -nfsv ../ffc-sfd-env/.env .env
```
- This makes it a lot easier to update `.env` files across a set of microservices because when a new environment variable comes along or a variable needs updating, you can simply copy/paste or edit the variable(s) into any `.env` file regardless of which repo you have open and the symlink will ensure that it is updated in the master `.env` as well.
***
## yq
- Need this to be able to run commands from Defra's [ffc-azure-service-bus-scripts](https://github.com/defra/ffc-azure-service-bus-scripts) repo.
### Instructions
- Not a requirement to be installed on an offnet machine, but I did need to install this in order to run the scripts in the repo mentioned above so I could provision Service Bus infrastructure.
- Install using [Homebrew](https://github.com/mikefarah/yq?tab=readme-ov-file#macos--linux-via-homebrew):
```
brew install yq
```
***
## NPM Package Version Prefix
- Configuring save prefix to remove the `^` that is prefixed to the version number of NPM packages after installing them/when they are listed in the `package.json`.
### Instructions
- Open terminal and run the following command:
```
npm config set save-exact true
```
- This will remove the caret (`^`) from the version numbers of NPM packages in the `package.json`. The caret means that it will install the latest version and the versions succeeding (from my understanding at least). This is not needed for Defra projects, hence why we use the above command to get rid of the caret.
***
## Azure Data Studio
- Originally used this to clean up databases (remove duplicate data/rows etc.) from the SND3 database on ADP using PostgreSQL syntax.
### Instructions
- Install [Azure Data Studio](https://azure.microsoft.com/en-gb/products/data-studio).
- Once installed, open the application, add your onmicrosoft account.
- Navigate to the Extensions tab and search for PostgreSQL, install the official PostgreSQL extension.
- Select `New connection` and connect to desired database.
***
## SSH Key
- An SSH key is a credential that allows you to connect to GitHub ==without entering your username and personal access token each time==. An SSH key is a pair of keys that uses the Secure Shell (SSH) protocol to establish a secure connection between a local machine and a remote server.
### Instructions
- To generate an SSH key, follow the instructions on GitHub for [generating a new key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). Stop when you reach the section about "copying contents into the config file for ssh".
- The next step is to follow a second set of instructions for [adding your SSH key to Github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account). 
- Test by cloning a repo using the SSH option and then go back to your settings to check the key is green and is highlighted as having been recently used.