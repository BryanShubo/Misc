#####1. Using command to create a project
```
mvn archetype:generate -DgroupId={project-packaging} 
   -DartifactId={project-name} 
   -DarchetypeArtifactId=maven-archetype-quickstart 
   -DinteractiveMode=false

mvn archetype:generate -DgroupId=org.apache.cli
   -DartifactId=apache_cli
   -DarchetypeArtifactId=maven-archetype-quickstart 
   -DinteractiveMode=false
```

#####2. Using mavn to build jar file
```
1) add this plugin to pom.xml
        <build>
                <plugins>        
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
		</plugins>
	<build>	
```
			
2) mvn clean compile assembly:assembly

3) For oracle jdbc (make sure the jar file is in local repository):
```
		<dependency>
			<groupId>ojdbc</groupId>
			<artifactId>ojdbc6</artifactId>
			<version>18</version>
		</dependency>
```

2. Install maven on mac

Since your installation works on the terminal you installed, all the exports you did, work on the current bash and its child process. but is not spawned to new terminals.

env variables are lost if the session is closed; using .bash_profile, you can make it available in all sessions, since when a bash session starts, it 'runs' its .bashrc and .bash_profile

```

Now follow these steps and see if it helps:

type env | grep M2_HOME on the terminal that is working. This should give something like

M2_HOME=/usr/local/apache-maven/apache-maven-3.1.1

typing env | grep JAVA_HOME should give like this:

JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0_40.jdk/Contents/Home

Now you have the PATH for M2_HOME and JAVA_HOME.

If you just do ls /usr/local/apache-maven/apache-maven-3.1.1/bin, you will see mvn binary there. All you have to do now is to point to this location everytime using PATH. since bash searches in all the directory path mentioned in PATH, it will find mvn.

now open .bash_profile, if you dont have one just create one

vi ~/.bash_profile

Add the following:

#set JAVA_HOME
JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0_40.jdk/Contents/Home
export JAVA_HOME


M2_HOME=/usr/local/apache-maven/apache-maven-3.1.1
export M2_HOME

PATH=$PATH:$JAVA_HOME/bin:$M2_HOME/bin
export PATH
save the file and type source ~/.bash_profile. This steps executes the commands in the .bash_profile file and you are good to go now.

open a new terminal and type mvn that should work.
```
