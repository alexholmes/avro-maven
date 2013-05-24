Avro Maven
==========

A simple example of how to use the Avro Maven plugin to generate Avro sources given an Avro
schema file.

## License

Apache version 2.0 (for more details look at [LICENSE](LICENSE).

## Usage

Run Avro's code generation against [weather.avsc](src/main/avro/weather.avsc) using Maven:

```bash
$ mvn compile
```

Examine the code-generated source:

```bash
$ ls src/main/java/com/alexholmes/avro/Weather.java
src/main/java/com/alexholmes/avro/Weather.java
```

## The Magic

The complete Maven file can be viewed in [pom.xml](pom.xml).

The key is in adding the following plugin to your `pom.xml` file:

```
<plugin>
    <groupId>org.apache.avro</groupId>
    <artifactId>avro-maven-plugin</artifactId>
    <version>${avro.version}</version>
    <executions>
        <execution>
            <phase>generate-sources</phase>
            <goals>
                <goal>schema</goal>
            </goals>
            <configuration>
                <sourceDirectory>${project.basedir}/src/main/avro/</sourceDirectory>
                <outputDirectory>${project.basedir}/src/main/java/</outputDirectory>
            </configuration>
        </execution>
    </executions>
</plugin>
```

You'll also need to include Avro as a dependency:

```
<properties>
    <avro.version>1.7.4</avro.version>
    ...
</properties>

...

<dependencies>
    <dependency>
        <groupId>org.apache.avro</groupId>
        <artifactId>avro</artifactId>
        <version>${avro.version}</version>
    </dependency>
    <dependency>
        <groupId>org.apache.avro</groupId>
        <artifactId>avro-maven-plugin</artifactId>
        <version>${avro.version}</version>
    </dependency>
    <dependency>
        <groupId>org.apache.avro</groupId>
        <artifactId>avro-compiler</artifactId>
        <version>${avro.version}</version>
    </dependency>
</dependencies>
```

Done!