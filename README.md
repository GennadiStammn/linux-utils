# linux-utils

## Crontab

`[sudo] apt-get install cron`

`/etc/init.d/cron start #start cron scheduler`

`crontab -e  #edit cron job table`

# add entry
`* * * * * date > /tmp.txt`

`* * * * * find /path/to/files* -mtime +5 -exec rm {} \;`

`0 0 * * MON find /path/to/files* -mtime +5 -exec rm {} \; #every monday`


# Helm

## Basics

Chart: a package of kubernetes ressources to run an application

https://artifacthub.io/

Repository: A Place where charts can be collected and shared.
	helm search [hub | repo]
		helm search hub kafka
		healm search repo brigade
	helm repo add https://brigadecore.github.io/charts
		helm repo list
		helm repo remove [repo-name]
	helm pull

Release: An instance of a chart running on a Kubernetes Ckuster. One chart can be installed on a cluster, each time it is a new release.
	Install must have a repository!

	Search for stuff in https://artifacthub.io/
		-> e.g. grafana
		helm repo add bitnami https://charts.bitnami.com/bitnami

	helm install [releae-name] [name-of-chart]
		helm install angry-kid bitnami/grafana
		helm list
		helm status angry-kid
		
Upgrade a release:
	helm upgrade angry-kid bitnami/grafana

Rollback to a revision:
	helm rollback angry-kid 1
	

## Install/Upgrade/Rollback Example

	helm install angry-kid bitnami/grafana --version 5.0.2
	helm upgrade angry-kid bitnami/grafana --version 5.1.1
	helm list
	helm rollback angry-kid 1
	helm list

## Set Values/ Reste Values

	helm install --set replicaCount=2 angry-kid bitnami/grafana
	kubectl get pods
	helm upgrade --reset-values angry-kid bitnami/grafana
	kubectl get pods
	
## Create Own Charts

	helm create hello-world
	helm lint
	helm package hello-world
	helm install hello-world ./hello-world-0.1.0.tgz
	
	image:
		repository: docker/getting-started
		pullPolicy: IfNotPresent
		# Overrides the image tag whose default is the chart appVersion.
		tag: "latest"

# Versions Maven Plugin

Documentation: https://www.mojohaus.org/versions-maven-plugin/

Tutorial: https://www.baeldung.com/maven-dependency-latest-version

Maven Plugin

```
<build>
	<plugins>
		<plugin>
			<groupId>org.codehaus.mojo</groupId>
			<artifactId>versions-maven-plugin</artifactId>
			<version>2.8.1</version>
			<configuration>
				<includes>
					<include>com.fasterxml.jackson.core:jackson-databind</include>
				</includes>
				<excludes>
                    <exclude>org.apache.commons:commons-collections4</exclude>
                </excludes>
			</configuration>
		</plugin>
	</plugins>
</build>
```

Display outdated dependencies

`mvn versions:display-dependency-updates -Dversions.outputFile=target/outdated.txt`

Use release (replace SNAPSHOT versions)

`mvn versions:use-releases`

Use next release versions, creates a pom.xml.versionsBackup file

`mvn versions:use-next-versions`

Use latest release versions, creates a pom.xml.versionsBackup file

`mvn versions:use-latest-versions`


More finetuning options, such as providing a rules URL.
