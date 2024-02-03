# DEFRA Developer Config Guide
## Summary
This document details the set-up of a MacBook to use for software development within the FCP under DEFRA. The original repo detailing the set-up can be found on [DEFRA's official GitHub](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/README.md). Please use the original guide as the main set of instructions and only refer to this guide when there's any problems. The following information is simply the documentation of my own set-up and any additional steps which helped my Mac set-up whenever I was having issues. Spoiler alert, Homebrew solved a lot of these problems ([installing Homebrew](https://brew.sh/) should probably be the first thing you do).
***
### Developer Tools
-> [Reference in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/setup-macbook.md#install-developer-tools).
##### Instructions
- Open `terminal` and run the following command: 
```
xcode-select --install
````
- A pop-up window will appear stating that the `xcode-select` command requires the command line developer tools, click install and wait for the process to finish.
- Run the command again to verify installation. The output should say something along the lines of `Command line tools are already installed...`.
##### Comments
- This one takes a wee while.
***
### Docker Desktop

-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/setup-macbook.md#install-docker-desktop-for-mac).
##### Instructions
- [Download Docker Desktop for Mac](https://docs.docker.com/desktop/install/mac-install/).
##### Comments
- If your Mac is not fully updated to the latest OS, then Docker Desktop may not open. Open `System Settings` and begin the OS update (this step also takes a while, but Docker Desktop should be able to open just fine afterwards).
***
### Signing Commits (a.k.a ensuring your commits on GitHub have that cool Verified tag next to your username)
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/sign-commits.md).
##### Instructions
- Follow the instructions in the reference point (see above).
##### Comments
- Test that your commits are being signed by creating a dummy repo and pushing to that repo.
- If for whatever reason commits are not shown as `Verified` on GitHub, don't fret, the same happened to me. Here's what I did:
	- Some frantic Googling, which led me to [the answer](https://dev.to/devmount/signed-git-commits-in-vs-code-36do).
	- In the above link, skip to the section titled *Set up GitHub*. It explains that you can tell Git your GPG key ID. First, get the ID of the GPG key you just created using this command:
		  ` gpg --list-secret-keys --keyid-format=long`
	  - In the following example the GPG key ID is `3AA5C34371567BD2`:
		  ![gpg-key-id-example.png](https://github.com/rtasalem/macbook-config/blob/main/defra-setup/gpg-key-id-example.png)
	- Take this ID and run the following commands:
		  `git config --global user.signingkey 3AA5C34371567BD2`
		  `git config --global commit.gpgsign true`
	- In VS Code, navigate to your `settings.json` and copy and past the following:
		`"git.enableCommitSigning" : true`
- Test your commits again, using a dummy repo and with all fingers crossed, your commits should now appear as `Verified`.
***
### Visual Studio Code
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-vs-code.md).
##### Instructions
- Follow the guide, ignore the section titled *WSL Configuration* (this applies to Windows Devices only).
##### Comments
- This section has a lot of bits that need to be added to your `settings.json` file in VS Code. To find your `settings.json`, open VS Code and hit `cmd` + `,` this will open the User Settings screen. From here, click the `Open Settings (JSON)` button in the top right corner (see below).
![locating-settings-json.png](https://github.com/rtasalem/macbook-config/blob/main/defra-setup/locating-settings-json.png)
- After following the guide, your `settings.json` should look something similar to the below image (your `settings.json` *needs* to include lines 11-17 by the end of this step):
![settings-json-post-vs-code-installation.png](https://github.com/rtasalem/macbook-config/blob/main/defra-setup/settings-json-post-vs-code-installation.png)
***
### SonarLint
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-sonarlint.md).
##### Instructions
- Instead of `using sudo apt-get install openjdk-11-jre` to install JDK (Java Development Kit), use Homebrew: `brew install openjdk`. 
- After installing the [SonarLint extension](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarlint-vscode) in VS Code, the guide mentions setting the location of the JRE (Java Runtime Environment) in your VS Code settings (i.e. the `settings.json`), put the path used is incorrect.
- For me, the correct path, which I have in my settings.json to use was: `"sonarlint.ls.javaHome": "/usr/local/opt/openjdk/libexec/openjdk.jdk"`.
- A useful way of finding the correct path to the JRE is to use open *Go* in the Mac toolbar and select *Go to Folder*. This way you can find the JRE location you want to set in the `settings.json`.
- Continue to follow the instructions, [ignoring step 4 under the section titled *SonarLint Installation (VS Code)*](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-sonarlint.md#sonarlint-installation-vs-code) as this applies to individual projects rather than your VS Code environment.
##### Comments
- Ignore the section titled [*Configure Sonar for C#*](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-sonarlint.md#configure-sonar-for-c) (unless you'll be writing C#).
- Also note that step 5 will not work if the correct location for the JRE isn't set.
- By the end of this sections, your `setting.json` should include lines 20-26 as shown below:
![settings-json-post-vs-code-installation.png](https://github.com/rtasalem/macbook-config/blob/main/defra-setup/settings-json-post-vs-code-installation.png)
- The location of the JRE might not be the same for everyone. I.e. the one I ended up using may not be (but hopefully will be) the same as location on a different device.
***
### Docker Compose
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-docker-compose.md#install-docker-compose).
##### Instructions
- There aren't any instructions for this step. If you downloaded Docker Desktop, then you already have Docker Compose.
##### Comments
- None.
***
### detect-secrets
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-detect-secrets.md).
##### Instructions
- Follow the original guide as described.
##### Comments
- At first thought I did not properly install Python as the `python --version` command was not showing the version post-installation, but actually the correct command to run was `python3 --version` (i.e. version 3). Same issue occurred with Pip, but again just had to run the version command as `pip3 --version`.
- Generally if there are any installation issues during this step, just use Homebrew.
- Open terminal, run the following command to verify installation:
```
detect-secrets --version
```
***
### Node Version Manager (NVM)
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-node-version-manager.md).
##### Instructions
- Personally, I just used [Homebrew to install NVM](https://formulae.brew.sh/formula/nvm).
##### Comments
- Open terminal, run the following command to verify installation:
```
nvm --version
```
***
### .NET SDK
-> [Reference point in DEFRA's original guide]().
##### Instructions
- Follow the guide as is.
##### Comments
- Just like in the guide, verify the installation by opening terminal and running
```
dotnet --version
```
- Run the final command in the guide as a finishing step to installing .NET SDK:
```
dotnet tool install --global dotnet-ef
```
***
### kubectl
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-kubectl.md).
##### Instructions
- In the instructions, Homebrew was one of the recommendations for [installing kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/#install-with-homebrew-on-macos), this is what I used. 
##### Comments
- Verify installation by running the following command:
```
kubectl version
```
***
### Helm
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/installing-helm.md).
##### Instructions
- Again, Homebrew was one of the recommendations for [installing Helm](https://helm.sh/docs/intro/install/#through-package-managers).
##### Comments
- Verify the installation by running the following command:
```
helm version
```
***
### Azure CLI
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-azure-cli.md).
##### Instructions
- Once again, Homebrew can be used to install [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-macos).
- Log in to Azure Tenant using the command provided in the guide (see the reference point provided above) via your terminal. 
- You'll need to get your credentials from CCoE (Cloud Centre of Excellence).
##### Comments
- Verify installation using the following command:
```
az version
```
***
### Snyk CLI
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-snyk.md).
##### Instructions
- No surprise, you can install [Snyk CLI using Homebrew](https://docs.snyk.io/snyk-cli/install-or-update-the-snyk-cli#install-with-homebrew-macos-linux).
##### Comments
- Run the following command to verify installation:
```
snyk --version
```
***
### GitHub CLI
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-github.md).
##### Instructions
- Yes, of course you can [install GitHub CLI using Homebrew](https://github.com/cli/cli).
##### Comments
- Verify installation by running the following command to check the version of GitHub CLI that was installed:
```
gh --version
```
***
### OpenVPN
-> [Reference point in DEFRA's original guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/install-openvpn.md).
##### Instructions
- Run the following commands:
```
brew install openvpn
```
- You will need to get your OpenVPN credentials from the CCoE:
	1. Navigate to the OpenVPN link provided in the email.
	2. You'll see a login page, select *Sign In via SAML*.
	3. Enter your DEFRA credentials.
	4. Most likely a MFA prompt will pop-up, complete this.
	5. Once authenticated, you will be able to download the latest VPN client software i.e. OpenVPN Connect, download the version under the heading *Recommended for your device*.
	6. Launch the installed OpenVPN Connent app, you'll see a pop-up showing your DEFRA VPN profile.
	7. Next to your name/credentials there will be a on/off toggle, toggle this to on.
	8. If it appears to be taking some time to connect to OpenVPN, click the menu icon in the top left (this will appear as 3 horizontal lines on top of each other) and if you see an option to install the latest OpenVPN update, do this.
	9. Once the update is installed, try again to turn on the connection and this should get you connected a lot faster.
	10. Now you're all connected with OpenVPN and there's nothing left to do.
##### Comments
- Verify installation of OpenVPN using:
```
openvpn --version
```
- If OpenVPN isn't connecting, repeat steps 1-10 above (you may not need to update to the latest version) and the VPN should now connect.
***
## Other
Below this point is other additional config that I've done for my Mac that is not in the original guide.
***
### Another Redis Desktop Manager
-> Installed when building the POC (proof of concept) for FFD.
##### Instructions
- [Download from GitHub](https://github.com/qishibo/AnotherRedisDesktopManager) (includes the Homebrew command to install).
***
### Microsoft Azure Storage Explorer
-> Recommended by the lead developer while going through different FFD repositories.
##### Instructions
- [Download from Microsoft](https://azure.microsoft.com/en-gb/products/storage/storage-explorer)
- Can also be installed by Homebrew: 
```
brew install --cask microsoft-azure-storage-explorer
```
***
### GraphQL Syntax Highlighting
-> Used when implementing GraphQL for a couple of POCs for FFD.
##### Instructions
- Install the [GraphQL: Syntax Highlighting Extension](https://marketplace.visualstudio.com/items?itemName=GraphQL.vscode-graphql-syntax) via VS Code
- To implement the extension when writing out `typeDefs` (type definitions), add `#graphql` at the top of the `typeDefs` (see example below):
![graphql-syntax-highlighting.png](https://github.com/rtasalem/macbook-config/blob/main/defra-setup/graphql-syntax-highlighting.png)
***
### Jenkins
-> Is needed to access CI/CD pipelines.
##### Instructions
- You will need to get your Jenkins credentials from CCoE.
- In the email invite, a link will be provided to access the Jenkins dashboard (for some reason I could only open the link on the potato, it doesn't load on the browser from my offnet device).
- Enter the username and password provided in the email and you should now be able to log into the Jenkins dashboard.
##### Comments
- None.
### Lens
-> Kubernetes IDE used to access pods.
##### Instructions
- [Download and install Lens](https://formulae.brew.sh/cask/lens).
- Ensure that kubectl and Azure CLI have been installed (these are prerequisites and should have already been installed when going through [DEFRA's original dev guide](https://github.com/DEFRA/ffc-development-guide/blob/main/guides/developer-laptop-setup/README.md)).
- Follow the steps in the documentation (on Confluence) for connecting Lens to Kubernetes Clusters.