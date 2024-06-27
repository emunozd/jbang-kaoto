
# JBang and Kaoto workshop

JBang simplifies Java programming, offering easy creation, editing, and running of self-contained Java programs in local environments.

With just one download and command, JBang eliminates Java's setup, making Java development as seamless as Python or JavaScript. JBang supports multiple files and dependencies from any Maven repository, compatible with Java 8 to Java 17 and beyond.

Kaoto is the acronym for Kamel Orchestration Tool. It is a low code and no code integration designer to create and edit integrations based on Apache Camel. Kaoto is extendable, flexible, and adaptable to different use cases. Only supports `.camel.yaml` extension files, so any design from any other DSL like java and/or SpringBoot needs to be transformed first.


## Prerequisites
#### JBang

Install JBang locally, please excecute the command:
```bash
$ curl -Ls https://sh.jbang.dev | bash -s - app setup
```
Finally, install the Camel JBang component with:
```bash
$ jbang app install camel@apache/camel
```
#### Kaoto

Install VisualStudio or VSCodium in your end.

To use Kaoto, install the [Language support for Apache Camel extension in VisualStudio or VSCodium](https://docs.redhat.com/en/documentation/red_hat_build_of_apache_camel/4.0/html/tooling_guide/using-vscode-language-support-extension#installing_language_support_for_apache_camel_extension)

## Demo
#### 1. Create a Hello-World Camel Route with JBang

Create a basic Camel route:
```bash
$ camel init Hello.java
```
Execute it:
```bash
$ camel run Hello.java
```
Expected output:
```bash
...
2024-06-27 10:51:28.283  INFO 5118 --- [           main] e.camel.impl.engine.AbstractCamelContext : Apache Camel 4.6.0 (Hello) started in 181ms (build:0ms init:0ms start:181ms)
2024-06-27 10:51:29.264  INFO 5118 --- [ - timer://java] Hello.java:14                            : Hello Camel from route1
2024-06-27 10:51:30.255  INFO 5118 --- [ - timer://java] Hello.java:14                            : Hello Camel from route1
...
```
Chose another runtime, for example: spring-boot:
```bash
$ camel run Hello.java --runtime=spring-boot

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v3.2.5)

2024-06-27T11:14:14.332-05:00  INFO 6214 --- [           main] o.a.c.jbangrundummy.CamelApplication     : Starting CamelApplication using Java 17.0.5 with PID 6214
...
2024-06-27T11:14:17.132-05:00  INFO 6214 --- [           main] o.a.c.impl.engine.AbstractCamelContext   : Apache Camel 4.6.0 (camel-1) started in 119ms (build:0ms init:0ms start:119ms)
2024-06-27T11:14:17.135-05:00  INFO 6214 --- [           main] o.a.c.jbangrundummy.CamelApplication     : Started CamelApplication in 3.134 seconds (process running for 3.684)
2024-06-27T11:14:18.129-05:00  INFO 6214 --- [ - timer://java] route1                                   : Hello Camel from route1
2024-06-27T11:14:19.124-05:00  INFO 6214 --- [ - timer://java] route1                                   : Hello Camel from route1
```
*Note: Please make sure you are using at least Java 17 to run the above command.*
#### 2. Open the created integration with Kaoto
Using the `camel-cli tool`, execute the following command:
```bash
$ camel transform route --format=yaml Hello.java --output=hello.camel.yaml
```
Other way to made the above transformation is using the `VS IDE`:
- Open the file that needs to be transformed.
- Press F1.
- Write "Transform" and select the option: "Camel: Transform a Camel route from YAML DSL". 
*Note: please make sure that new name ends with "camel.yaml" extension.*

Terminal console in the VS IDE should show something like follows:
```bash
 *  Executing task: jbang '-Dcamel.jbang.version=4.6.0' camel@apache/camel transform route '/path/to/Hello.java' '--format=yaml' '--output=/path/to/hello.camel.yaml' 
```
It will show the created route in the `step 1`, in a visual friendly way.

#### 3. Export to a Quarkus maven project

Execute the following command:
```bash
$ camel export Hello.java --runtime quarkus --gav com.example:redhat:1.0 --dir output
```
The above command will create a quarkus project in the `output` directory.