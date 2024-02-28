# VS Code Config
### Settings
 - Press `cmd` + `Shift` + `P` and type *install code*. Choose the option that reads `Shell Command: Install 'code' in PATH`. When you want to open a project in VS Code: right click > New Terminal at Folder > run the command `code .` > this will open the project in VS Code (cuts out navigation/searching for workspaces).
### Extensions
#### Theme & Appearance
- [ ] [One Dark Pro Monokai Darker Theme (Eser Ozvataf)](https://marketplace.visualstudio.com/items?itemName=eserozvataf.one-dark-pro-monokai-darker)
- [ ] [VS Code Icons (VS Code Icons Team)](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons) 
- [ ] [Rainbow Brackets (Mhammed Talhaouy)](https://marketplace.visualstudio.com/items?itemName=tal7aouy.rainbow-bracket) 
- [ ] [indent-raindow (oderwat)](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow) 
- [ ] [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) - within the `settings.json` ensure to set the following configuration for Prettier:
```
	"prettier.singleQuote": true,
	"pretter.semi": false,
	"prettier.trailingComma": "none"
```
- The above is simply for formatting code for a desired "look" and matches how I should format code for work.
- [ ]  Set the colour of comments so that they stand out, don't have a similar colour to the actual code, and aren't so faded that they are hard to read. The photo below shows what should be added into the `settings.json` to set the comments to a light pinkish colour which is mostly distinct from the colour applied to actual code:
![comments-colour.png](https://github.com/rtasalem/macbook-config/blob/main/personal-setup/comments-colour.png)
#### Java
- [ ] [Java IDE Pack (Paul Verest)](https://marketplace.visualstudio.com/items?itemName=pverest.java-ide-pack) - includes the following extensions/extension packs:
	- [ ] [Extension Pack for Java (Microsoft)](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack) - includes the following extensions:
		- [ ] [Debugger for Java (Microsoft)](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug)
		- [ ] [Language Support for Java by Red Hat (Red Hat)](https://marketplace.visualstudio.com/items?itemName=redhat.java)
		- [ ] [Test Runner for Java (Microsoft)](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-test)
		- [ ] [Maven for Java (Microsoft)](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-maven)
		- [ ] [Project Manager for Java (Microsoft)](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-dependency)
		- [ ] [IntelliCode (Microsoft)](https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode)
	- [ ] [Spring Initializr Java Support (Microsoft)](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr)
	- [ ] [Spring Boot Dashboard (Microsoft)](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-boot-dashboard)
	- [ ] [Java Properties (ithildir)](https://marketplace.visualstudio.com/items?itemName=ithildir.java-properties) - Java properties syntax highlighting
	- [ ] [Java Decompiler (David Gileadi)](https://marketplace.visualstudio.com/items?itemName=dgileadi.java-decompiler)
	- [ ] [Tomcat for Java (Wei Shen)](https://marketplace.visualstudio.com/items?itemName=adashen.vscode-tomcat)
	- [ ] [Java IDE (JavaHub)](https://marketplace.visualstudio.com/items?itemName=YouMayCallMeV.vscode-java-saber)
- [ ] [Lombok Annotations Support for VS Code (Microsoft)](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-lombok)
- [ ] [Spring Boot Tools (VMware)](https://marketplace.visualstudio.com/items?itemName=vmware.vscode-spring-boot)
#### APIs
- [ ] [Postman](https://marketplace.visualstudio.com/items?itemName=Postman.postman-for-vscode) 
- [ ] [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) (optional, similar to Postman)
- [ ] [IntelliCode API Usage Examples (Microsoft)](https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.intellicode-api-usage-examples)
#### Docker
- [ ] [Docker (Microsoft)](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker#:~:text=Docker%20for%20Visual%20Studio%20Code,NET%20inside%20a%20container.) 
- [ ] [Docker Compose (p1c2u)](https://marketplace.visualstudio.com/items?itemName=p1c2u.docker-compose)
- [ ] [Dev Containers (Microsoft)](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
#### Kubernetes
- [ ] [Kubernetes](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools)
#### .NET & C#
- [ ] [.NET Install Tool (Microsoft)](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.vscode-dotnet-runtime) 
- [ ] [C# (Microsoft)](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)
- [ ] [IntelliCode for C# Dev Kit (Microsoft)](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.vscodeintellicode-csharp)
#### Other
- [ ] [Live Server (Ritwick Dey)](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) 
- [ ] [Red Hat Dependency Analytics (Red Hat)](https://marketplace.visualstudio.com/items?itemName=redhat.fabric8-analytics)
- [ ] [Error Lens (Alexander)](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens)
