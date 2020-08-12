# maven
This repository acts as a central maven repository for all my java packages. When a project has a new release I will publish it in this repository.

## Configuration
At first you need to generate a github token to access the repository. You go to your [developer settings](https://github.com/settings/tokens) and select the scopes for the token. You need at least write and read privileges (see screenshot) in order to publish and install packages.

![GitHub Token Scopes](/docs/screenshots/token-privileges.png)

Then you have to configure a server for GitHub in your `~/.m2/settings.xml` with your username and the github token. You can just copy the [settings-template.xml](/templates/settings-template.xml) to configure your maven.
```xml
<servers>
    ...
    <server>
        <id>github</id>
        <username>Your GitHub Username</username>
        <password>Insert your token here</password>
    </server>
    ...
</servers>
```

## Deployment
To deploy a package to the repository you have to specify the location in the `distributionManagement` in your project's pom.xml.
```xml
<distributionManagement>
	<repository>
		<id>github</id>
		<name>GitHub DonColon Apache Maven Packages</name>
		<url>https://maven.pkg.github.com/doncolon/maven</url>
	</repository>
</distributionManagement>
```

After that you open your console in the project's directory und enter the following command. Maven builds the package and publish it to the github package registry.
```bash
mvn publish
```