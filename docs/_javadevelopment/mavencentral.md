---
layout: default
title: Maven Central
---

# Maven Central

Maven Central, located at [https://central.sonatype.com/](https://central.sonatype.com/), is a repository that is used to store Java libraries.  It is the default repository for Maven and Gradle builds and therefore publishing libraries to Maven Central is a common practice for Java developers making them easily available to other developers.

UnitVectorY Labs publishes various Java libraries under the component namespace `com.unitvectory`.

## Publishing to Maven Central

Publish to Maven Central requires several steps to be completed on Sonatype's website, which are best described in their [Getting Started](https://central.sonatype.org/publish/publish-guide/) guide.

The rest of this document will focus on the specific setup used by UnitVectorY labs.

Credit is due to [the Over Engineering Blog](https://theoverengineered.blog/posts/publishing-my-first-artifact-to-maven-central-using-github-actions) that has a post which walks through the process of publishing to Maven Central with a GitHub action.

The GitHub action used to publish to Maven Central requires the following secrets to be added to the GitHub repository: `OSSRH_USERNAME` and `OSSRH_TOKEN` which are generated from Sonatype and will be used by the GitHub Action.

## Maven Plugins for Publishing

Maven Central has several requirements for publishing libraries. This includes signing the library with a GPG key, providing a POM file, and providing a source and javadoc jar file.  These requirements are met by including various plugins in the POM file.

The first is the GPG plugin that is used to sign the library.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-gpg-plugin</artifactId>
    <version>3.2.4</version>
    <executions>
        <execution>
            <id>sign-artifacts</id>
            <phase>verify</phase>
            <goals>
                <goal>sign</goal>
            </goals>
            <configuration>
                <gpgArguments>
                    <arg>--pinentry-mode</arg>
                    <arg>loopback</arg>
                </gpgArguments>
            </configuration>
        </execution>
    </executions>
</plugin>
```

The next plugin is the Javadoc plugin that is required to create the Javadoc jar file.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-javadoc-plugin</artifactId>
    <version>3.6.3</version>
    <executions>
        <execution>
            <id>attach-javadoc</id>
            <goals>
                <goal>jar</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

A related plugin is the Source plugin that is required to create the source jar file.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-source-plugin</artifactId>
    <version>3.3.1</version>
    <executions>
        <execution>
            <id>attach-source</id>
            <goals>
                <goal>jar</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

The last required plugin is the plugin that is used to publish the library to Maven Central.

```xml
<plugin>
    <groupId>org.sonatype.central</groupId>
    <artifactId>central-publishing-maven-plugin</artifactId>
    <version>0.4.0</version>
    <extensions>true</extensions>
    <configuration>
        <publishingServerId>central</publishingServerId>
        <tokenAuth>true</tokenAuth>
        <autoPublish>true</autoPublish>
    </configuration>
</plugin>
```

That is it for the required plugins.  This is enough that the `mvn deploy` command can be used to publish the library to Maven Central.  However, it is recommended approach is to utilize a GitHub Action to perform this deployment.

## GPG Signing Key

Maven Central requires a GPG signing key to be used to sign the library.

A GPG key must be generated and published to a key server.  This guide will not go into the details of generating a GPG key.

Since the goal is to use GitHub Actions to sign and deploy the library, the GPG key must be added to the GitHub repository as a secret.  The GPG key should be added as a secret named `OSSRH_GPG_SECRET_KEY` and the passphrase for the GPG key should be added as a secret named `OSSRH_GPG_SECRET_KEY_PASSWORD`.


## Deploying with GitHub Actions

This requires setting up a GitHub Action that will build the library and then deploy it to Maven Central.

A working example can be found at [https://github.com/UnitVectorY-Labs/fileparamunit/blob/main/.github/workflows/release.yml](https://github.com/UnitVectorY-Labs/fileparamunit/blob/main/.github/workflows/release.yml)

```
name: Publish Java version to Maven Central
on:
  release:
    types: [published]
jobs:
  publish:
    runs-on: ubuntu-latest
    timeout-minutes: 30

    permissions:
      contents: write
      id-token: write
      attestations: write

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up Java for publishing to Maven Central Repository
        uses: actions/setup-java@v4
        with:
          java-version: 17
          distribution: corretto
          server-id: central
          server-username: MAVEN_USERNAME
          server-password: MAVEN_PASSWORD
          gpg-private-key: ${{ secrets.OSSRH_GPG_SECRET_KEY }}
          gpg-passphrase: MAVEN_GPG_PASSPHRASE

      - name: Extract Maven Artifacts
        id: maven_artifact
        run: |
          echo "version=$(mvn help:evaluate -Dexpression=project.version -q -DforceStdout)" >> $GITHUB_OUTPUT
          echo "artifactId=$(mvn help:evaluate -Dexpression=project.artifactId -q -DforceStdout)" >> $GITHUB_OUTPUT

      - name: Build Java Project
        run: mvn clean package -ntp

      - name: Publish to the Maven Central Repository
        run: mvn deploy -ntp
        env:
          MAVEN_USERNAME: ${{ secrets.OSSRH_USERNAME }}
          MAVEN_PASSWORD: ${{ secrets.OSSRH_TOKEN }}
          MAVEN_GPG_PASSPHRASE: ${{ secrets.OSSRH_GPG_SECRET_KEY_PASSWORD }}

      - name: Publish Java Artifacts to GitHub Release
        run: |
          cp pom.xml ${{ steps.maven_artifact.outputs.artifactId }}-${{ steps.maven_artifact.outputs.version }}.pom
          gh release upload ${{github.event.release.tag_name}} "${{ steps.maven_artifact.outputs.artifactId }}-${{ steps.maven_artifact.outputs.version }}.pom"
          for jar in target/*.jar; do
            [ -e "$jar" ] || continue
            gh release upload ${{github.event.release.tag_name}} "$jar"
          done
        env:
          GITHUB_TOKEN: ${{ github.TOKEN }}

      - name: GitHub Attestation for JAR files
        uses: actions/attest-build-provenance@v1
        with:
          subject-path: "target/*.jar"

      - name: GitHub Attestation for POM file
        uses: actions/attest-build-provenance@v1
        with:
          subject-path: "pom.xml"
          subject-name: "${{ steps.maven_artifact.outputs.artifactId }}-${{ steps.maven_artifact.outputs.version }}.pom"
```

This GitHub action is triggered when a release is published.  It sets up the Java environment, builds the library, and then deploys it to Maven Central with the appropriate signatures.

Additionally the JAR and POM artifacts are uploaded to the GitHub Release for reference.

The JAR and POM file aalso use a GitHub Attestation to provide proof of their provenance.  This is not yet uploaded to Maven Central and is only available through GitHub to verify the artifact.
