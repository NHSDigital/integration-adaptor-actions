# integration-adaptor-actions
For github workflow actions shared between adaptors.

### The `configure-java.yml` workflow.

* Checks out a GitHub repository provided with the `github ref` and `github.repository` environment variables.
* Sets up Java based on the provided JDK version and distribution.
* Sets up Gradle.

#### Workflow Call Inputs
* `java-version` -> String -> This is required.
* `jdk-distribution` -> String -> This is optional, if nothing is provided the default `temurin` will be used.
* ``

#### Example Usage
```yml
name: Main Workflow

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened]
    branches:
      - main

jobs:
  checkstyle:
    name: Checkstyle
    runs-on: ubuntu-latest
    steps:
      - name: Configure Java
        uses: NHSDigital/integration-adaptor-actions/.github/workflows/configure-java.yml@main
        with:
          java-version: '21'
          repository: ${{ github.repository }}
          ref: ${{ github.ref }}
```