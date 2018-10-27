# WALA for DASCA

This is a fork of WALA, tracking minor bug-fixes and enhancements required for 
[DASCA](https://git.logicalhacking.com/DASCA/DASCA).

## Integrating Updates from Upstream

After cloning the repostistory, you need to manually configure the upstream URL
of the remote fork:

``` sh
git remote add upstream https://github.com/wala/WALA.git
```

The default steps for merging with upstream are:

``` sh
  git fetch upstream
  git checkout master
  git merge upstream/master
```

## Building Artifacts

This fork uses the gradle setup of the WALA build system. Thus, for details, please
consult the instructions in the file [README-Gradle](README-Gradle.md). In general, 
for rebuilding all WALA artifacts, use:

``` sh
./gradlew clean assemble
```

## Publishing Artifacts

### Configuration

For publishing artifacts, you need to configure the username and password required
for uploading to the remote artifacts repository, i.e., you need  to add the following
properties to your  `GRADLE_USER_HOME/gradle.properties`  (default: `$HOME/.gradle/gradle.properties`)
file:

``` gradle
comLogicalhackingArtifactsUser=<USER>
comLogicalhackingArtifactsPassword=<PASSWORD>
```

### Preparation

Before publishing new artifacts to the artifacts repository, please update the version identifier in
the file  `build.gradle` by replacing the second `SNAPSHOT`

``` gradle
version '1.5.1-SNAPSHOT-DASCA-SNAPSHOT'
```

with the version that should be published. Next, tag the new version:

``` gradle
git tag -s "<VERSION>" -m "Tagging version <VERSION>."
```

### Uploading Artifacts

Publishing artifacts is as easy as calling

``` sh
./gradlew publish
```