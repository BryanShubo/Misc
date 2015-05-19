###Maven Life Cycle

生命周期Maven有三套相互独立的生命周期，请注意这里说的是“三套”，而且“相互独立”，这三套生命周期分别是： 
```
1. Clean Lifecycle 在进行真正的构建之前进行一些清理工作。 
2. Default Lifecycle 构建的核心部分，编译，测试，打包，部署等等。 
3. Site Lifecycle 生成项目报告，站点，发布站点。
```
 
再次强调一下它们是相互独立的，你可以仅仅调用clean来清理工作目录，仅仅调用site来生成站点。
当然你也可以直接运行 mvn clean install site 运行所有这三套生命周期。 

clean生命周期每套生命周期都由一组阶段(Phase)组成，我们平时在命令行输入的命令总会对应于一个特定的阶段。
比如，运行mvn clean ，这个的clean是Clean生命周期的一个阶段。有Clean生命周期，也有clean阶段。

####1. Clean生命周期一共包含了三个阶段： 

pre-clean 执行一些需要在clean之前完成的工作 
clean 移除所有上一次构建生成的文件 
post-clean 执行一些需要在clean之后立刻完成的工作 
mvn clean 中的clean就是上面的clean，在一个生命周期中，运行某个阶段的时候，它之前的所有阶段都会被运行，
也就是说，mvn clean 等同于 mvn pre-clean clean ，如果我们运行 mvn post-clean ，那么 pre-clean，clean 都会被运行。这是Maven很重要的一个规则，可以大大简化命令行的输入。 

####2. Site生命周期pre-site 执行一些需要在生成站点文档之前完成的工作 
site 生成项目的站点文档 
post-site 执行一些需要在生成站点文档之后完成的工作，并且为部署做准备 
site-deploy 将生成的站点文档部署到特定的服务器上 
这里经常用到的是site阶段和site-deploy阶段，用以生成和发布Maven站点，这可是Maven相当强大的功能，Manager比
较喜欢，文档及统计数据自动生成，很好看。 

####3. Default生命周期Default生命周期是Maven生命周期中最重要的一个，绝大部分工作都发生在这个生命周期中。
这里，只解释一些比较重要和常用的阶段： 

validate 
generate-sources 
process-sources 
generate-resources 
process-resources 复制并处理资源文件，至目标目录，准备打包。 
compile 编译项目的源代码。 
process-classes 
generate-test-sources 
process-test-sources 
generate-test-resources 
process-test-resources 复制并处理资源文件，至目标测试目录。 
test-compile 编译测试源代码。 
process-test-classes 
test 使用合适的单元测试框架运行测试。这些测试代码不会被打包或部署。 
prepare-package 
package 接受编译好的代码，打包成可发布的格式，如 JAR 。 
pre-integration-test 
integration-test 
post-integration-test 
verify 
install 将包安装至本地仓库，以让其它项目依赖。 
deploy 将最终的包复制到远程的仓库，以让其它开发人员与项目共享。 
运行任何一个阶段的时候，它前面的所有阶段都会被运行，这也就是为什么我们运行mvn install 的时候，代码会被编译，测试，打包。此外，Maven的插件机制是完全依赖Maven的生命周期的，因此理解生命
周期至关重要。 




Maven Build Life Cycles, Phases and Goals

When Maven builds a software project it follows a build life cycle. The build life cycle is divided 
into build phases, and the build phases are divided into build goals. Maven build life cycles, build 
phases and goals are described in more detail in the Maven Introduction to Build Phases, but here I 
will give you a quick overview.

Build Life Cycles
Maven has 3 built-in build life cycles. These are:

default
clean
site
Each of these build life cycles takes care of a different aspect of building a software project. Thus, 
each of these build life cycles are executed independently of each other. You can get Maven to execute 
more than one build life cycle, but they will be executed in sequence, separately from each other, as 
if you had executed two separate Maven commands.

The default life cycle handles everything related to compiling and packaging your project. The clean 
life cycle handles everything related to removing temporary files from the output directory, including
generated source files, compiled classes, previous JAR files etc. The site life cycle handles everything 
related to generating documentation for your project. In fact, site can generate a complete website with 
documentation for your project.

Build Phases
Each build life cycle is divided into a sequence of build phases, and the build phases are again subdivided
into goals. Thus, the total build process is a sequence of build life cycle(s), build phases and goals.

You can execute either a whole build life cycle like clean or site, a build phase like install which is 
part of the default build life cycle, or a build goal like dependency:copy-dependencies. Note: You cannot
execute the default life cycle directly. You have to specify a build phase or goal inside the default 
life cycle.

When you execute a build phase, all build phases before that build phase in this standard phase sequence 
are executed. Thus, executing the install build phase really means executing all build phases before the 
install phase, and then execute the install phase after that.

The default life cycle is of most interest since that is what builds the code. Since you cannot execute 
the default life cycle directly, you need to execute a build phase or goal from the default life cycle. 
The default life cycle has an extensive sequence of build phases and goals, ,so I will not describe them
all here. The most commonly used build phases are:

Build Phase	Description
validate	Validates that the project is correct and all necessary information is available. 
This also makes sure the dependencies are downloaded.
compile	Compiles the source code of the project.
test	Runs the tests against the compiled source code using a suitable unit testing framework. 
These tests should not require the code be packaged or deployed.
package	Packs the compiled code in its distributable format, such as a JAR.
install	Install the package into the local repository, for use as a dependency in other projects 
locally.
deploy	Copies the final package to the remote repository for sharing with other developers and projects.
You execute one of these build phases by passing its name to the mvn command. Here is an example:

mvn package
This example executes the package build phase, and thus also all build phases before it in Maven's 
predefined build phase sequence.

If the standard Maven build phases and goals are not enough to build your project, you can create 
Maven plugins to add the extra build functionality you need.

Build Goals
Build goals are the finest steps in the Maven build process. A goal can be bound to one or more 
build phases, or to none at all. If a goal is not bound to any build phase, you can only execute 
it by passing the goals name to the mvn command. If a goal is bound to multiple build phases, 
that goal will get executed during each of the build phases it is bound to.
