---
layout: default
title: Code Coverage
parent: Java Development
nav_order: 1
---

# Code Coverage

One of the key predictors of high quality code is effective test coverage.  UnitVectorY Labs applications written in Java use the JaCoCo library to measure code coverage.  The following are the steps to add code coverage to a Java project.

## Add JaCoCo to the POM file

Add the following to the POM file to add JaCoCo to the project.

```xml
            <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>0.8.12</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>report</id>
                        <phase>test</phase>
                        <goals>
                            <goal>report</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
```

## Configure GitHub Actions

Add the following to the GitHub Actions workflow file to upload the code coverage to Codecov.

```yaml
    - name: Upload coverage reports to Codecov
      uses: codecov/codecov-action@v4.3.1
      with:
        token: ${{ secrets.CODECOV_TOKEN }}
        slug: UnitVectorY-Labs/fileparamunit
```

The above example is taken from: https://github.com/UnitVectorY-Labs/fileparamunit/blob/main/.github/workflows/build.yml