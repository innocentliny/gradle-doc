# fat-jar
Implementations of building fat (all-in-one) jar

## Option 1 - Jar task
```groovy
task fatJar(type: Jar) {
    manifest {
        attributes 'Implementation-Title': 'ooxx',
                   'Implementation-Version': version,
                   'Main-Class': 'com.abc.MyMain'
    }
    baseName = project.name + '-all'
    from { configurations.compile.collect { it.isDirectory() ? it : zipTree(it) } }
    with jar
}
```

## Option 2 - Shadow plugin
See [Gradle Shadow Plugin](https://imperceptiblethoughts.com/shadow/)
