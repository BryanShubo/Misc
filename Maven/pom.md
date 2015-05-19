###POM Reference

####1. The Basics
The POM 4.0.0 XSD and descriptor reference documentation
#####1.1 What is the POM?
POM stands for "Project Object Model". A project contains configuration files, as well as the developers 
involved and the roles they play, the defect tracking system, the organization and licenses, the URL of 
where the project lives, the project's dependencies, and all of the other little pieces that come into 
play to give code life. It is a one-stop-shop for all things concerning the project. 

#####1.2 Quick Overview
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
 
  <!-- The Basics -->
  <groupId>...</groupId>  // package
  <artifactId>...</artifactId>  //project name or module name
  <version>...</version>
  <packaging>...</packaging> //default: war. Options: pom, jar, maven-plugin, ejb, war, ear, rar, par.
  <dependencies>...</dependencies> // required jars
  <parent>...</parent> // 
  <dependencyManagement>...</dependencyManagement>
  <modules>...</modules>
  <properties>...</properties>
 
  <!-- Build Settings -->
  <build>...</build>
  <reporting>...</reporting>
 
  <!-- More Project Information -->
  <name>...</name>
  <description>...</description>
  <url>...</url>
  <inceptionYear>...</inceptionYear>
  <licenses>...</licenses>
  <organization>...</organization>
  <developers>...</developers>
  <contributors>...</contributors>
 
  <!-- Environment Settings -->
  <issueManagement>...</issueManagement>
  <ciManagement>...</ciManagement>
  <mailingLists>...</mailingLists>
  <scm>...</scm>
  <prerequisites>...</prerequisites>
  <repositories>...</repositories>
  <pluginRepositories>...</pluginRepositories>
  <distributionManagement>...</distributionManagement>
  <profiles>...</profiles>
</project>
```

#####1.3 POM Relationships
"Jarmageddon" quickly ensues as the dependency tree becomes large and complicated. "Jar Hell" follows, 
where versions of dependencies on one system are not equivalent to versions as those developed with, 
either by the wrong version given, or conflicting versions between similarly named jars. Maven solves 
both problems through a common local repository from which to link projects correctly, versions and all.

######1.3.1 Dependencies
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  ...
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.0</version>
      <type>jar</type>
      <scope>test</scope>
      <optional>true</optional>
    </dependency>
    ...
  </dependencies>
  ...
</project>
```
```
type: Corresponds to the dependant artifact's packaging type. This defaults to jar. 
Some examples are jar, ejb-client and test-jar. New types can be defined by plugins that 
set extensions to true, so this is not a complete list.

scope: There are five scopes available:
1) compile - default scope. Compile dependencies are available in all classpaths. Furthermore, 
those dependencies are propagated to dependent projects.
2) provided - this is much like compile, but indicates you expect the JDK or a container to 
provide it at runtime. It is only available on the compilation and test classpath, and is not 
transitive.
3) runtime - this scope indicates that the dependency is not required for compilation, but is 
for execution. It is in the runtime and test classpaths, but not the compile classpath.
4) test - this scope indicates that the dependency is not required for normal use of the application, 
and is only available for the test compilation and execution phases.
5) system - this scope is similar to provided except that you have to provide the JAR which contains 
it explicitly. The artifact is always available and is not looked up in a repository.

systemPath: is used only if the the dependency scope is system. Otherwise, the build will fail 
if this element is set. The path must be absolute, so it is recommended to use a property to 
specify the machine-specific path (more on properties below), such as ${java.home}/lib. Since it 
is assumed that system scope dependencies are installed a priori, Maven will not check the repositories 
for the project, but instead checks to ensure that the file exists. If not, Maven will fail the build 
and suggest that you download and install it manually.

optional:
Marks optional a dependency when this project itself is a dependency. Confused? For example, 
imagine a project A that depends upon project B to compile a portion of code that may not be 
used at runtime, then we may have no need for project B for all project. So if project X adds 
project A as its own dependency, then Maven will not need to install project B at all. Symbolically, 
if => represents a required dependency, and --> represents optional, although A=>B may be the case 
when building A X=>A-->B would be the case when building X.
In the shortest terms, optional lets other projects know that, when you use this project, you do not 
require this dependency in order to work correctly.
```
######1.3.2 Exclusions

Exclusions explicitly tell Maven that you don't want to include the specified project that is a 
dependency of this dependency (in other words, its transitive dependency). For example, the maven-embedder 
requires maven-core, and we do not wish to use it or its dependencies, then we would add it as an exclusion.
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  ...
  <dependencies>
    <dependency>
      <groupId>org.apache.maven</groupId>
      <artifactId>maven-embedder</artifactId>
      <version>2.0</version>
      <exclusions>
        <exclusion>
          <groupId>org.apache.maven</groupId>
          <artifactId>maven-core</artifactId>
        </exclusion>
      </exclusions>
    </dependency>
    ...
  </dependencies>
  ...
</project>
```
It is also sometimes useful to clip a dependency's transitive dependencies. A dependency may 
have incorrectly specified scopes, or dependencies that conflict with other dependencies in 
your project. Using wildcard excludes makes it easy to exclude all a dependency's transitive 
dependencies. In the case below you may be working with the maven-embedder and you want to manage
the dependencies you use yourself, so you clip all the transitive dependencies:
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  ...
  <dependencies>
    <dependency>
      <groupId>org.apache.maven</groupId>
      <artifactId>maven-embedder</artifactId>
      <version>3.1.0</version>
      <exclusions>
        <exclusion>
          <groupId>*</groupId>
          <artifactId>*</artifactId>
        </exclusion>
      </exclusions>
    </dependency>
    ...
  </dependencies>
  ...
</project>
```
exclusions: Exclusions contain one or more exclusion elements, each containing a groupId and 
rtifactId denoting a dependency to exclude. Unlike optional, which may or may not be installed 
and used, exclusions actively remove themselves from the dependency tree.

#####1.4 Inheritance
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
 
  <groupId>org.codehaus.mojo</groupId>
  <artifactId>my-parent</artifactId>
  <version>2.0</version>
  <packaging>pom</packaging>
</project>
```
The packaging type required to be pom for parent and aggregation (multi-module) projects. These types 
define the goals bound to a set of lifecycle stages. For example, if packaging is jar, then the package 
phase will execute the jar:jar goal. If the packaging is pom, the goal executed will be site:
attach-descriptor. Now we may add values to the parent POM, which will be inherited by its children. 
The elements in the parent POM that are inherited by its children are:

* dependencies
* developers and contributors
* plugin lists
* reports lists
* plugin executions with matching ids
* plugin configuration
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
 
  <parent>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>my-parent</artifactId>
    <version>2.0</version>
    <relativePath>../my-parent</relativePath> // optional
  </parent>
 
  <artifactId>my-project</artifactId>
</project>
```
#####1.5 The Super POM
```
<project>
  <modelVersion>4.0.0</modelVersion>
 
  <repositories>
    <repository>
      <id>central</id>
      <name>Central Repository</name>
      <url>http://repo.maven.apache.org/maven2</url>
      <layout>default</layout>
      <snapshots>
        <enabled>false</enabled>
      </snapshots>
    </repository>
  </repositories>
 
  <pluginRepositories>
    <pluginRepository>
      <id>central</id>
      <name>Central Repository</name>
      <url>http://repo.maven.apache.org/maven2</url>
      <layout>default</layout>
      <snapshots>
        <enabled>false</enabled>
      </snapshots>
      <releases>
        <updatePolicy>never</updatePolicy>
      </releases>
    </pluginRepository>
  </pluginRepositories>
 
  <build>
    <directory>${project.basedir}/target</directory>
    <outputDirectory>${project.build.directory}/classes</outputDirectory>
    <finalName>${project.artifactId}-${project.version}</finalName>
    <testOutputDirectory>${project.build.directory}/test-classes</testOutputDirectory>
    <sourceDirectory>${project.basedir}/src/main/java</sourceDirectory>
    <scriptSourceDirectory>src/main/scripts</scriptSourceDirectory>
    <testSourceDirectory>${project.basedir}/src/test/java</testSourceDirectory>
    <resources>
      <resource>
        <directory>${project.basedir}/src/main/resources</directory>
      </resource>
    </resources>
    <testResources>
      <testResource>
        <directory>${project.basedir}/src/test/resources</directory>
      </testResource>
    </testResources>
    <pluginManagement>
      <!-- NOTE: These plugins will be removed from future versions of the super POM -->
      <!-- They are kept for the moment as they are very unlikely to conflict with lifecycle mappings (MNG-4453) -->
      <plugins>
        <plugin>
          <artifactId>maven-antrun-plugin</artifactId>
          <version>1.3</version>
        </plugin>
        <plugin>
          <artifactId>maven-assembly-plugin</artifactId>
          <version>2.2-beta-5</version>
        </plugin>
        <plugin>
          <artifactId>maven-dependency-plugin</artifactId>
          <version>2.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-release-plugin</artifactId>
          <version>2.0</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
 
  <reporting>
    <outputDirectory>${project.build.directory}/site</outputDirectory>
  </reporting>
 
  <profiles>
    <!-- NOTE: The release profile will be removed from future versions of the super POM -->
    <profile>
      <id>release-profile</id>
 
      <activation>
        <property>
          <name>performRelease</name>
          <value>true</value>
        </property>
      </activation>
 
      <build>
        <plugins>
          <plugin>
            <inherited>true</inherited>
            <artifactId>maven-source-plugin</artifactId>
            <executions>
              <execution>
                <id>attach-sources</id>
                <goals>
                  <goal>jar</goal>
                </goals>
              </execution>
            </executions>
          </plugin>
          <plugin>
            <inherited>true</inherited>
            <artifactId>maven-javadoc-plugin</artifactId>
            <executions>
              <execution>
                <id>attach-javadocs</id>
                <goals>
                  <goal>jar</goal>
                </goals>
              </execution>
            </executions>
          </plugin>
          <plugin>
            <inherited>true</inherited>
            <artifactId>maven-deploy-plugin</artifactId>
            <configuration>
              <updateReleaseInfo>true</updateReleaseInfo>
            </configuration>
          </plugin>
        </plugins>
      </build>
    </profile>
  </profiles>
</project>
```
#####1.6 Dependency Management

Besides inheriting certain top-level elements, parents have elements to configure values for 
child POMs and transitive dependencies. One of those elements is dependencyManagement.
```
dependencyManagement: is used by POMs to help manage dependency information across all of its children. 
If the my-parent project uses dependencyManagement to define a dependency on junit:junit:4.0, then POMs 
inheriting from this one can set their dependency giving the groupId=junit and artifactId=junit only, 
then Maven will fill in the version set by the parent. The benefits of this method are obvious. 
Dependency details can be set in one central location, which will propagate to all inheriting POMs. 
In addition, the version and scope of artifacts which are incorporated from transitive dependencies 
may also be controlled by specifying them in a dependency management section.
```
```
传递性依赖原则：

A-->B
A-->C

1.路径最近者优先
2.路径相同，第一声明者优先 in makeFriend’s pom.xml

注意：
1.dependencyManagement中定义的依赖子module不会共享
2.dependencies中定义的依赖子module可以共享
```

#####1.7 Aggregation (or Multi-Module)

A project with modules is known as a multimodule, or aggregator project. Modules are projects that 
this POM lists, and are executed as a group. An pom packaged project may aggregate the build of a 
set of projects by listing them as modules, which are relative directories to those projects.
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
 
  <groupId>org.codehaus.mojo</groupId>
  <artifactId>my-parent</artifactId>
  <version>2.0</version>
  <packaging>pom</packaging>
 
  <modules>
    <module>my-project</module>
    <module>another-project</module>
  </modules>
</project>
```
A final note on Inheritance v. Aggregation
```
Inheritance and aggregation create a nice dynamic to control builds through a single, high-level POM. 
You will often see projects that are both parents and aggregators. For example, the entire maven core runs 
through a single base POM org.apache.maven:maven, so building the Maven project can be executed by a 
single command: mvn compile. However, although both POM projects, an aggregator project and a parent 
project are not one in the same and should not be confused. A POM project may be inherited from - 
but does not necessarily have - any modules that it aggregates. Conversely, a POM project may aggregate 
projects that do not inherit from it.
```

#####1.8 Properties
Properties are the last required piece in understanding POM basics. Maven properties are value 
placeholder, like properties in Ant. Their values are accessible anywhere within a POM by using 
the notation ${X}, where X is the property.
```
They come in five different styles:
1) env.X: Prefixing a variable with "env." will return the shell's environment variable. 
For example, ${env.PATH} contains the PATH environment variable.
Note: While environment variables themselves are case-insensitive on Windows, lookup of 
properties is case-sensitive. In other words, while the Windows shell returns the same value for 
%PATH% and %Path%, Maven distinguishes between ${env.PATH} and ${env.Path}. As of Maven 2.1.0, 
the names of environment variables are normalized to all upper-case for the sake of reliability.

2) project.x: A dot (.) notated path in the POM will contain the corresponding element's value. 
For example: <project><version>1.0</version></project> is accessible via ${project.version}.

3) settings.x: A dot (.) notated path in the settings.xml will contain the corresponding element's 
value. For example: <settings><offline>false</offline></settings> is accessible via ${settings.offline}.

4) Java System Properties: All properties accessible via java.lang.System.getProperties() are available 
as POM properties, such as ${java.home}.

5) x: Set within a <properties /> element in the POM. The value of <properties><someVar>value
</someVar></properies> may be used as ${someVar}.
```

####2. Build Settings
Build element, that handles things like declaring your project's directory structure and managing plugins; 
Reporting element, that largely mirrors the build element for reporting purposes.

######2.1 Build
The build element is conceptually divided into two parts: 
1) BaseBuild type, which contains the set of elements common to both build elements (the top-level build 
element under project and the build element under profiles, covered below); 

2) Build type, which contains the BaseBuild set as well as more elements for the top level definition. 

Note: These different build elements may be denoted "project build" and "profile build".
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  ...
  <!-- "Project Build" contains more elements than just the BaseBuild set -->
  <build>...</build>
 
  <profiles>
    <profile>
      <!-- "Profile Build" contains a subset of "Project Build"s elements -->
      <build>...</build>
    </profile>
  </profiles>
</project>
```
######2.2 The BaseBuild Element Set

BaseBuild is exactly as it sounds: the base set of elements between the two build elements in the POM.
```
<build>
  <defaultGoal>install</defaultGoal>
  <directory>${basedir}/target</directory>
  <finalName>${artifactId}-${version}</finalName>
  <filters>
    <filter>filters/filter1.properties</filter>
  </filters>
  ...
</build>
```

filter: Defines *.properties files that contain a list of properties that apply to resources which 
accept their settings (covered below). In other words, the "name=value" pairs defined within the 
filter files replace ${name} strings within resources on build. The example above defines the 
filter1.properties file under the filter/ directory. Maven's default filter directory is 
${basedir}/src/main/filters/.


######2.3 Resources
Another feature of build elements is specifying where resources exist within your project. 
Resources are not (usually) code. They are not compiled, but are items meant to be bundled 
within your project or used for various other reasons, such as code generation.

For example, a Plexus project requires a configuration.xml file (which specifies component 
configurations to the container) to live within the META-INF/plexus directory. Although we 
could just as easily place this file within src/main/resource/META-INF/plexus, we want instead 
to give Plexus its own directory of src/main/plexus. In order for the JAR plugin to bundle the
resource correctly, you would specify resources similar to the following:
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <build>
    ...
    <resources> <!--resource elements -->
      <resource>
        <targetPath>META-INF/plexus</targetPath>
        <filtering>false</filtering>
        <directory>${basedir}/src/main/plexus</directory>
        <includes>
          <include>configuration.xml</include>
        </includes>
        <excludes>
          <exclude>**/*.properties</exclude>
        </excludes>
      </resource>
    </resources>
    <testResources>
      ...
    </testResources>
    ...
  </build>
</project>
```
```
targetPath: Specifies the directory structure to place the set of resources from a build. Target path 
defaults to the base directory. A commonly specified target path for resources that will be packaged 
in a JAR is META-INF.

filtering: is true or false, denoting if filtering is to be enabled for this resource. Note, that filter 
*.properties files do not have to be defined for filtering to occur - resources can also use properties 
that are by default defined in the POM (such as ${project.version}), passed into the command line using 
the "-D" flag (for example, "-Dname=value") or are explicitly defined by the properties element. Filter 
files were covered above.

directory: This element's value defines where the resources are to be found. The default directory for 
a build is ${basedir}/src/main/resources.

includes: A set of files patterns which specify the files to include as resources under that specified 
directory, using * as a wildcard.

excludes: The same structure as includes, but specifies which files to ignore. In conflicts between 
include and exclude, exclude wins.

testResources: The testResources element block contains testResource elements. Their definitions 
are similar to resource elements, but are naturally used during test phases. The one difference 
is that the default (Super POM defined) test resource directory for a project is ${basedir}/src/test/
resources. Test resources are not deployed.
```

######2.4 Plugins
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <build>
    ...
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>2.0</version>
        <extensions>false</extensions>
        <inherited>true</inherited>
        <configuration>
          <classifier>test</classifier>
        </configuration>
        <dependencies>...</dependencies>
        <executions>...</executions>
      </plugin>
    </plugins>
  </build>
</project>
```
Beyond the standard coordinate of groupId:artifactId:version, there are elements which 
configure the plugin or this builds interaction with it.
```
extensions: true or false, whether or not to load extensions of this plugin. It is by default 
false. Extensions are covered later in this document.
 
inherited: true or false, whether or not this plugin configuration should apply to POMs which 
inherit from this one. Default value is true.

configuration: This is specific to the individual plugin. Without going too in depth into the 
mechanics of how plugins work, suffice it to say that whatever properties that the plugin Mojo 
may expect (these are getters and setters in the Java Mojo bean) can be specified here. In the 
above example, we are setting the classifier property to test in the maven-jar-plugin's Mojo. It 
may be good to note that all configuration elements, wherever they are within the POM, are intended 
to pass values to another underlying system, such as a plugin. In other words: values within a 
configuration element are never explicitly required by the POM schema, but a plugin goal has every 
right to require configuration values.
If your POM declares a parent, it will inherit plugin configuration from either the build/plugins 
or pluginManagement sections of the parent.
```
To illustrate, consider the following fragment from a parent POM:
```
<plugin>
<groupId>my.group</groupId>
<artifactId>my-plugin</artifactId>
<configuration>
  <items>
    <item>parent-1</item>
    <item>parent-2</item>
  </items>
  <properties>
    <parentKey>parent</parentKey>
  </properties>
</configuration>
</plugin>
```
And consider the following plugin configuration from a project that uses that parent as its parent:
```
<plugin>
<groupId>my.group</groupId>
<artifactId>my-plugin</artifactId>
<configuration>
  <items>
    <item>child-1</item>
  </items>
  <properties>
    <childKey>child</childKey>
  </properties>
</configuration>
```
The default behavior is to merge the content of the configuration element according to element name. 
If the child POM has a particular element, that value becomes the effective value. if the child POM 
does not have an element, but the parent does, the parent value becomes the effective value. Note 
that this is purely an operation on XML; no code or configuration of the plugin itself is involved.
Only the elements, not their values, are involved.

Applying those rules to the example, Maven comes up with:
```
<plugin>
<groupId>my.group</groupId>
<artifactId>my-plugin</artifactId>
<configuration>
  <items>
    <item>child-1</item>
  </items>
  <properties>
    <childKey>child</childKey>
    <parentKey>parent</parentKey>
  </properties>
</configuration>
```
You can control how child POMs inherit configuration from parent POMs by adding attributes to 
the children of the configuration element. The attributes are combine.children and combine.self. 
Use these attributes in a child POM to control how Maven combines plugin configuration from the 
parent with the explicit configuration in the child.

Here is the child configuration with illustrations of the two attributes:
```
<configuration>
  <items combine.children="append">
    <!-- combine.children="merge" is the default -->
    <item>child-1</item>
  </items>
  <properties combine.self="override">
    <!-- combine.self="merge" is the default -->
    <childKey>child</childKey>
  </properties>
</configuration>
```
Now, the effective result is the following:
```
<configuration>
  <items combine.children="append">
    <item>parent-1</item>
    <item>parent-2</item>
    <item>child-1</item>
  </items>
  <properties combine.self="override">
    <childKey>child</childKey>
  </properties>
</configuration>
```
combine.children="append" results in the concatenation of parent and child elements, 
in that order. combine.self="override", on the other hand, completely suppresses parent 
configuration. You cannot use both both combine.self="override" and combine.children="append" 
on an element; if you try, override will prevail.

Note that these attributes only apply to the configuration element they are declared on, and 
are not propagated to nested elements. That is if the content of an item element from the child 
POM was a complex structure instead of text, its sub-elements would still be subject to the 
default merge strategy unless they were themselves marked with attributes.

The combine.* attributes are inherited from parent to child POMs. Take care when adding those 
attributes a parent POM as this might affect child or grand-child POMs.

dependencies: Dependencies are seen a lot within the POM, and are an element under all plugins 
element blocks. The dependencies have the same structure and function as under that base build. 
The major difference in this case is that instead of applying as dependencies of the project, 
they now apply as dependencies of the plugin that they are under. The power of this is to alter 
the dependency list of a plugin, perhaps by removing an unused runtime dependency via exclusions, 
or by altering the version of a required dpendency. See above under Dependencies for more information.
executions: It is important to keep in mind that a plugin may have multiple goals. Each goal may 
have a separate configuration, possibly even binding a plugin's goal to a different phase 
altogether. executions configure the execution of a plugin's goals.
For example, suppose you wanted to bind the antrun:run goal to the verify phase. We want the task 
to echo the build directory, as well as avoid passing on this configuration to its children 
(assuming it is a parent) by setting inherited to false. You would get an execution like this:
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  ...
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-antrun-plugin</artifactId>
        <version>1.1</version>
        <executions>
          <execution>
            <id>echodir</id>
            <goals>
              <goal>run</goal>
            </goals>
            <phase>verify</phase>
            <inherited>false</inherited>
            <configuration>
              <tasks>
                <echo>Build Dir: ${project.build.directory}</echo>
              </tasks>
            </configuration>
          </execution>
        </executions>
 
      </plugin>
    </plugins>
  </build>
</project>
```
id: Self explanatory. It specifies this execution block between all of the others. When the 
phase is run, it will be shown in the form: [plugin:goal execution: id]. In the case of this 
example: [antrun:run execution: echodir]
goals: Like all pluralized POM elements, this contains a list of singular elements. In this 
case, a list of plugin goals which are being specified by this execution block.
phase: This is the phase that the list of goals will execute in. This is a very powerful 
option, allowing one to bind any goal to any phase in the build lifecycle, altering the 
default behavior of Maven.
inherited: Like the inherited element above, setting this false will supress Maven from 
passing this execution onto its children. This element is only meaningful to parent POMs.
configuration: Same as above, but confines the configuration to this specific list of goals,
rather than all goals under the plugin.
Plugin Management

pluginManagement: is an element that is seen along side plugins. Plugin Management contains 
plugin elements in much the same way, except that rather than configuring plugin information 
for this particular project build, it is intended to configure project builds that inherit 
from this one. However, this only configures plugins that are actually referenced within the 
plugins element in the children. The children have every right to override pluginManagement definitions.
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  ...
  <build>
    ...
    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-jar-plugin</artifactId>
          <version>2.2</version>
          <executions>
            <execution>
              <id>pre-process-classes</id>
              <phase>compile</phase>
              <goals>
                <goal>jar</goal>
              </goals>
              <configuration>
                <classifier>pre-process</classifier>
              </configuration>
            </execution>
          </executions>
        </plugin>
      </plugins>
    </pluginManagement>
    ...
  </build>
</project>
```
If we added these specifications to the plugins element, they would apply only to a single 
POM. However, if we apply them under the pluginManagement element, then this POM and all 
inheriting POMs that add the maven-jar-plugin to the build will get the pre-process-classes 
execution as well. So rather than the above mess included in every child pom.xml, only the 
following is required:
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  ...
  <build>
    ...
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
      </plugin>
    </plugins>
    ...
  </build>
</project>
```
