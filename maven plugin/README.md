# maven plugin
Documents about learing maven plugin.

## Basic build.gradle example with Nexus
```groovy
plugins {
    id 'java-library'
    id 'maven'
}

group = 'com.abc'
version = '1.0.0-SNAPSHOT'

sourceCompatibility = '1.7'
targetCompatibility = '1.7'
[compileJava, compileTestJava, javadoc]*.options*.encoding = 'UTF-8'

configurations.all {
    // check for updates every build
    resolutionStrategy.cacheChangingModulesFor 0, 'seconds'
}

repositories {
  maven {
      name "nexus"
      url maven_public_url
      credentials {
          username maven_username
          password maven_password
      }
  }
}
```
> Nexus is self-hosted maven repository server here.

1. Add local maven repository properties
   * Open gradle.properties file
     * Windows platform
       * in %userprofile%/.gradle folder
   * Add
     ```properties
     maven_username=<your_nexus_username>
     maven_password=<your_nexus_password>
     maven_public_url=http://<your_nexus_server_host>/nexus/content/groups/public/
     maven_release_url=http://<your_nexus_server_host>/nexus/content/repositories/releases/
     maven_snapshot_url=http://<your_nexus_server_host>/nexus/content/repositories/snapshots/
     ```
     > Create related folder or file if not exists.


