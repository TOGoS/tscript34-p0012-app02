# TScript34-P0012-App02

The purpose of this project, along with [Lib01](https://github.com/TOGoS/tscript34-p0012-lib01/),
is to demonstrate publishing and importing a package using Maven
in the simplest way possible while still maintaining control over
the package name and version number (so JitPack is a no-go).

I found that it can be done by letting GitHub build and
serve your packages, but even this requires some putzing
about with GitHub-specific configuration files,
and packages won't be public.

The whole Maven package-publishing scene is disappointingly complex to deal with.


## Accessing the GitHub package repo

You'll need to add something like the folllwing to `~/.m2/settings.xml`,
replacing `YourGitHubUsername` and `YourGitHubAccessToken`
with a personal access token, which you can generate at https://github.com/settings/tokens.

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd"
>
	<activeProfiles>
		<activeProfile>github</activeProfile>
	</activeProfiles>

	<profiles>
		<profile>
			<id>github</id>
			<repositories>
				<repository>
					<id>central</id>
					<url>https://repo1.maven.org/maven2</url>
				</repository>
				<repository>
					<id>github</id>
					<url>https://maven.pkg.github.com/TOGoS/tscript34-p0012-lib01</url>
					<snapshots>
						<enabled>true</enabled>
					</snapshots>
				</repository>
			</repositories>
		</profile>
	</profiles>

	<servers>
		<server>
			<id>github</id>
			<username>YourUsername</username>
			<password>YourGitHubAccessToken</password>
		</server>
	</servers>
</settings>
```

If that still doesn't work, try downloading the .jar
and other files from GitHub into
`~/.m2/repository/net/nuke24/tscript34/p0012/tscript34-p0012-lib01/0.0.6`
(or whatever; adjust package name and version as appropriate).

## Running the application

Try `mvn compile exec:java`.
