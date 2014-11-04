1. Using maven to build jar file




1. Using mavn to build jar file
1) add this plugin to pom.xml
	<plugin>
				<artifactId>maven-assembly-plugin</artifactId>
				<version>2.2</version>
				<configuration>
					<appendAssemblyId>false</appendAssemblyId>
					<descriptorRefs>
						<descriptorRef>jar-with-dependencies</descriptorRef>
					</descriptorRefs>
					<archive>
						<manifest>
							<mainClass>com.velogica.cte.App</mainClass>
						</manifest>
					</archive>
				</configuration>
			</plugin>
			
2) mvn clean compile assembly:assembly
3) For oracle jdbc (make sure the jar file is in local repository):
		<dependency>
			<groupId>ojdbc</groupId>
			<artifactId>ojdbc6</artifactId>
			<version>18</version>
		</dependency>
