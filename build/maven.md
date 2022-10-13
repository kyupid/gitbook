# Maven

### Lifecycle

3가지 built-in 빌드 라이프사이클이 있다.

* default
* clean
* site

default는 project deployment, clean은 project cleaning, site는 웹사이트 생성을 말한다

각 lifecycle은 다수의 phase 들로 구성되어 있다. [참고](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle\_Reference)

#### default lifecycle

* `validate` - validate the project is correct and all necessary information is available
* `compile` - compile the source code of the project
* `test` - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
* `package` - take the compiled code and package it in its distributable format, such as a JAR.
* `verify` - run any checks on results of integration tests to ensure quality criteria are met
* `install` - install the package into the local repository, for use as a dependency in other projects locally
* `deploy` - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

각 phase들은 독립적으로 실행될 수 있다.

그런데 순서가 있다.

위 리스트는 라이프사이클 순서대로 적어놓았는데, `verify` 를 실행하면 validate, compile, test, package가 자동으로 순서대로 실행 된후 verify가 실행된다.

#### phase and goal

phase와 goal 두개의 개념을 알아야한다

phase는 위에서 설명했듯이 lifecycle의 각 단계를 말하고 goal은 각 phase가 실행될때 수행해야할 업무같은 것이라고 보면된다.&#x20;

Maven에서 제공하는 모든 기능은 플러그인 기반으로 작동을 하는데 phase가 실행이되면 연결된 플러그인의 goal이 실행되는 방식이다

예를들어 phrase가 package이고  goal이 jar:jar 라고 되어있으면 package 때, jar (왼쪽) 플러그인에서 jar (오른쪽) 기능(goal)을 실행한다고 보면된다.
