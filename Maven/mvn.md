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
```
1) pre-clean 执行一些需要在clean之前完成的工作 
2) clean 移除所有上一次构建生成的文件 
3) post-clean 执行一些需要在clean之后立刻完成的工作 
4) mvn clean 中的clean就是上面的clean，在一个生命周期中，运行某个阶段的时候，它之前的所有阶段都会被运行.
```
也就是说，mvn clean 等同于 mvn pre-clean clean ，如果我们运行 mvn post-clean ，那么 pre-clean，clean 都会被运行。这是Maven很重要的一个规则，可以大大简化命令行的输入.

####2. Site生命周期pre-site 执行一些需要在生成站点文档之前完成的工作 
```
1) site 生成项目的站点文档 
2) post-site 执行一些需要在生成站点文档之后完成的工作，并且为部署做准备 
3) site-deploy 将生成的站点文档部署到特定的服务器上 
```
这里经常用到的是site阶段和site-deploy阶段，用以生成和发布Maven站点，这可是Maven相当强大的功能，
Manager比较喜欢，文档及统计数据自动生成，很好看。

####3. Default生命周期Default生命周期是Maven生命周期中最重要的一个，绝大部分工作都发生在这个生命周期中。
```
1) validate 
2) generate-sources 
3) process-sources 
4) generate-resources 
5) process-resources: 复制并处理资源文件，至目标目录，准备打包。 
6) compile: 编译项目的源代码。 
7) process-classes 
8) generate-test-sources 
9) process-test-sources 
10) generate-test-resources 
11) process-test-resources: 复制并处理资源文件，至目标测试目录。 
12) test-compile: 编译测试源代码。 
13) process-test-classes 
14) test: 使用合适的单元测试框架运行测试。这些测试代码不会被打包或部署。 
15) prepare-package 
15) package: 接受编译好的代码，打包成可发布的格式，如 JAR 。 
17) pre-integration-test 
18) integration-test 
19) post-integration-test 
20) verify 
21) install: 将包安装至本地仓库，以让其它项目依赖。 
22) deploy: 将最终的包复制到远程的仓库，以让其它开发人员与项目共享。 
```
运行任何一个阶段的时候，它前面的所有阶段都会被运行，这也就是为什么我们运行mvn install 的时候，代码会被编译，测试，打包。此外，Maven的插件机制是完全依赖Maven的生命周期的，
因此理解生命
周期至关重要。 
