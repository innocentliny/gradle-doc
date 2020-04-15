# maven-publish plugin
Documents about maven-publish plugin.

## Customized artifact example
```groovy
task MyJar_1(type: Jar) {
    from sourceSets.main.output
    exclude 'com/jar_2/**'
}

task MyJar_1_SourcesJar(type: Jar, dependsOn: classes) {
    classifier = 'sources'
    from sourceSets.main.allSource
    exclude 'com/jar_2/**'
}

task MyJar_1_JavadocJar(type: Jar, dependsOn: javadoc) {
    classifier = 'javadoc'
    from javadoc.destinationDir
    exclude 'com/jar_2/**'
}

task MyJar_2(type: Jar) {
    from sourceSets.main.output
    include 'com/jar_1/**'
}

task MyJar_2_SourcesJar(type: Jar, dependsOn: classes) {
    classifier = 'sources'
    from sourceSets.main.allSource
    include 'com/jar_1/**'
}

task MyJar_2_JavadocJar(type: Jar, dependsOn: javadoc) {
    classifier = 'javadoc'
    from javadoc.destinationDir
    include 'com/jar_1/**'
}

publishing
{
    repositories
    {
        maven
        {
            url "${project.version.endsWith('-SNAPSHOT') ? maven_snapshot_url : maven_release_url }"
            credentials
            {
                username maven_username
                password maven_password
            }
        }
    }

    publications
    {
        mavenUtilCloud(MavenPublication)
        {
            groupId 'com.jar_1'
            artifactId 'my_jar_1'

            from components.java
            artifacts = [MyJar_1, MyJar_1_SourcesJar, MyJar_1_JavadocJar]
        }

        mavenEventData(MavenPublication)
        {
            groupId 'com.jar_2'
            artifactId 'my_jar_2'

            from components.java
            artifacts = [MyJar_2, MyJar_2_SourcesJar, MyJar_2_JavadocJar]
        }
    }
}
```
