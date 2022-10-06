# libertydiag

`libertydiag` is a [Jakarta EE 9](https://openliberty.io/docs/latest/jakarta-ee.html) and [MicroProfile 5](https://openliberty.io/docs/latest/microprofile.html) web application for simulating diagnostic situations.

Running this application in production should be done with care because it may be used to execute various insecure functions.

## Download

Download `libertydiag.war` from the latest release at <https://github.com/IBM/libertydiag/releases/latest>

This application [requires](https://www.ibm.com/docs/en/was-liberty/base?topic=management-liberty-features) Liberty >= 22.0.0.1 and the following features to be installed: jakartaee-9.1 microProfile-5.0 requestTiming-1.0

## Screenshot

![Screenshot](screenshot.png)

## Development

1. Java >= 8 is required on your `PATH`; for example, [Semeru Java 8](https://developer.ibm.com/languages/java/semeru-runtimes/downloads/?version=8)
1. Build and run with [`mvnw liberty:dev`](https://openliberty.io/docs/latest/development-mode.html):
    * macOS and Linux:
      ```
      ./mvnw liberty:dev
      ```
    * Windows:
      ```
      mvnw liberty:dev
      ```
1. Wait for the message, "server is ready to run a smarter planet". For example:
   ```
   [INFO] [AUDIT   ] CWWKF0011I: The defaultServer server is ready to run a smarter planet. The defaultServer server started in 30.292 seconds.
   ```
1. Open your browser to the HTTP or HTTPS page:
    * <http://localhost:9080/>
    * <https://localhost:9443/>

To develop in Eclipse, click File } Import... } Maven } Existing Maven Projects

### Notes

1. Build WAR file and Liberty package: `mvnw package`
1. If you'd like to run the Liberty package as a jar: `java -jar target/libertydiag.jar`
1. Build container: `mvnw deploy`
1. Build container with normal logging:
   ```
   mvnw -Dimage.builder.arguments="--build-arg WLP_LOGGING_CONSOLE_FORMAT='SIMPLE' --build-arg WLP_LOGGING_CONSOLE_LOGLEVEL='INFO' --build-arg WLP_LOGGING_CONSOLE_SOURCE='message'" deploy
   ```

### Build Issues

1. Running `mvnw deploy` errors with `An Ant BuildException has occured: Execute failed: java.io.IOException: Cannot run program "podman"`
   \
   \
   If `podman` is not on your path and you want to use, for example, `docker` instead:
   ```
   mvnw -Dimage.builder=docker deploy
   ```
1. Running `mvnw deploy` errors with `An Ant BuildException has occured: exec returned:`
   \
   \
   Add `-X` to show full output:
   ```
   mvnw -X deploy
   ```

## New Release

1. Update the date in `pom.xml` in the line `<version>0.1.$DATE</version>` and then commit and push
    1. `git commit -a -s -S -m "Description of changes in this release"`
    1. `git push`
1. Tag with the same version and push
    1. `git tag 0.1.$DATE`
    1. `git push --tags`
