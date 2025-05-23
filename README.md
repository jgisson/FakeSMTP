# FakeSMTP (jgisson fork)

Fork: build and run with latest Java LTS (21)

FakeSMTP is a Free Fake SMTP Server with GUI for testing emails in applications easily.
It is written in Java.

<img src="http://nilhcem.github.io/FakeSMTP/images/screenshot_mac.png" width="664" height="463" />

Configure your application to use `localhost` as your SMTP server, and all
emails will be intercepted and displayed in this software.

FakeSMTP uses SubEthaSMTP: an easy-to-use server-side SMTP library for Java.

FakeSMTP is free to use for commercial and non-commercial projects and the
source code is provided.

It is licensed under the very free BSD or GPL license, whichever you prefer.

## Requirements

You need Java ~~JVM 1.6~~ JVM 21 or newer installed on your machine.

If you are on a "Unix-like" machine (Mac, GNU/Linux, BSD...), you may have
to be "root" to start the port `25`, otherwise, try another port >= `1024`.

## Usage

The fakeSMTP.jar is auto-executable.
If your desktop environment supports it, you can directly double click
on the .jar file.
Otherwise, run the following command:

    java -jar fakeSMTP-VERSION.jar

For Mac OS:

    java --add-exports java.desktop/com.apple.eawt=ALL-UNNAMED -jar target/fakeSMTP-VERSION.jar

If you want to specify the directory where emails will be saved when starting the application, you can use the `-o` argument:

    java -jar fakeSMTP-VERSION.jar -o output_directory_name
    java -jar fakeSMTP-VERSION.jar --output-dir output_directory_name

If you want to autostart the SMTP server at launch, you can use the `-s` argument:

    java -jar fakeSMTP-VERSION.jar -s
    java -jar fakeSMTP-VERSION.jar --start-server

If you want to autostart the SMTP server without a GUI (background) on a different port and bound to the loopback address:

    java -jar fakeSMTP-VERSION.jar -s -b -p 2525 -a 127.0.0.1
    java -jar fakeSMTP-VERSION.jar --start-server --background --port 2525 --bind-address 127.0.0.1

If you don't need to save emails on the filesystem (to improve the overall performances), you can use the `-m` (memory mode) argument:

    java -jar fakeSMTP-VERSION.jar -m

To see all the available options (relay domains, custom eml-viewer...):

    java -jar fakeSMTP-VERSION.jar --help

## Alternatives

FakeSMTP was created because we couldn't find any free (as in freedom) and
cross-platform SMTP server with GUI for testing emails in applications or websites.
Listed below are some greats alternatives to Fake SMTP:

**[SMTP4dev](http://smtp4dev.codeplex.com/)**

- Nice features;
- Open source;
- Windows only (written in .Net).

**[DevNull SMTP](http://www.aboutmyip.com/AboutMyXApp/DevNullSmtp.jsp)**

- Lightweight;
- Closed source;
- Cross-Platform (written in Java 1.4).

## Building it

You need to download and setup Maven.
Once installed, go to project directory and run the following command:

    mvn package -Dmaven.test.skip

This command will create an executable jar on the target folder.

We recommend you not to skip unit tests.

Once you know how to configure unit tests for this project, stop skipping them.

## Running integration tests

To run integration tests, you will first need to launch the application
and start the server on port `2525`.

    java -jar fakeSMTP-VERSION.jar -p 2525 -s

You can then run the following command:

    mvn integration-test

## Change the default port for unit/integration tests

You need to modify the following file:
`src/test/java/com/nilhcem/fakesmtp/core/test/TestConfig.java`.

Please note that it is better to have two different ports for unit and integrations tests, to avoid any port binding exception while running Maven's `integration-test` goal.

## Usage on Docker

- Build from source

Build the docker image after Maven build

    docker buildx build -t fakesmtp .

Build the docker image (Maven)

    mvn package docker:build -DskipTests

Run the docker image

    docker run -ti -d fakesmtp

Configure container

- Map the SMTP port 25 to host:

  `-p 2525:25`

- Map volume for received mails:

  `--privileged=true  -v /home/fakesmtp/mail:/output`

Full command

- Foward fakesmtp:25 to host port 2525,
- mount host folder user home ~/temp/fakesmtp/mail as container folder /output

  `docker run -ti -d -p 2525:25 --privileged=true -v ~/temp/fakesmtp/mail:/output fakesmtp`

## Contact me

Use my github's nickname (at) gmail (dot) com
