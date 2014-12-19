This file is used to store jar dependency in build.gradle


apply plugin: "java"
apply plugin: "groovy"
apply plugin: "eclipse"

//configurations{ myConfig}
repositories {
    mavenCentral()
    mavenLocal()
    maven { url "http://velogica-maven.eu.scor.local:8981/nexus/content/groups/public/"}
}

dependencies {
    compile 'org.codehaus.groovy:groovy-all:2.3.6'
    testCompile group: 'junit', name: 'junit', version: '4.11'
    compile 'org.slf4j:slf4j-api:1.7.3'

}


sourceSets {
    main {
        groovy {
            srcDirs = ['src/main/groovy']
        }
    }

    test {
        groovy {
            srcDirs = ['src/test/groovy']
        }
    }

    unitTest {
        java.srcDir file('src/test/groovy')
    }
}

/*jar {
    from configurations.compile.collect { zipTree it}
	//from configurations.myConfig.collect { zipTree it}
    manifest.attributes "Main-Class":"com.velogica.App"
}*/


// add the unitTest task
task unitTest(type:Test) {
    description = "run unit tests"
    testClassesDir = sourceSets.unitTest.output.classesDir
    classpath = sourceSets.unitTest.runtimeClasspath
}


task info << {
    println "Name: $project.name"
    println 'Dependencies: '
    project.configurations.testCompile.allDependencies.each {
        println it.name
    }
}
