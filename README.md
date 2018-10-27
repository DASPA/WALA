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

Before publishing new artifacts to the artifacts repository, please update the version identifier in the file  `build.gradle` by removing the `SNAPSHOT` postfix
and updating the `<WALAVERSION>` identifier.

``` gradle
version '<WALAVERSION>.[R|S].DASCA.<DASCAVERSION>'
```

with the version that should be published. Next, commit your changes and tag the
new version:

``` gradle
git commit -m "Preparing release of version <VERSION>." build.gradle
git tag -s "<VERSION>" -m "Tagging version <VERSION>."
```

Finally, mark the development version by appending `-SNAPSHOT`

``` gradle
version '<WALAVERSION>.[R|S].DASCA.<DASCAVERSION>-SNAPSHOT'
```

and commit your changes:

``` gradle
git commit -m "Marked development version" build.gradle
```

### Uploading Artifacts

Publishing artifacts is as easy as calling

``` sh
./gradlew publish
```