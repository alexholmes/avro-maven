Avro Maven
==========

Some simple examples of how to use the Avro Maven plugin to generate Avro sources given an Avro
schema, protocol or IDL file.

## License

Apache version 2.0 (for more details look at [LICENSE](LICENSE).

## Usage

Download the sources:

``bash
$ git clone git://github.com/alexholmes/avro-maven.git
``

Run Avro's code generation against the Avro files contained in [src/main/avro](src/main/avro) (
[weather.avsc](src/main/avro/weather.avsc),
[weather.avpr](src/main/avro/weather.avpr) and
[weather.avdl](src/main/avro/weather.avdl) ) using Maven:

```bash
$ cd avro-maven/
$ mvn clean compile
```

Examine the code-generated sources:

```bash
$ find . -type f -name *.java src/main/java/com/alexholmes/avro/Weather.java
./target/generated-sources/avro/com/alexholmes/avro/Weather.java
./target/generated-sources/avro/com/alexholmes/avro/weatherstation1/Station.java
./target/generated-sources/avro/com/alexholmes/avro/weatherstation1/WeatherStation.java
./target/generated-sources/avro/com/alexholmes/avro/weatherstation2/Simple.java
./target/generated-sources/avro/com/alexholmes/avro/weatherstation2/WeatherStation.java
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
        <goal>protocol</goal>
        <goal>idl-protocol</goal>
      </goals>
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
    <dependency>
      <groupId>org.apache.avro</groupId>
      <artifactId>avro-ipc</artifactId>
      <version>${avro.version}</version>
    </dependency>
</dependencies>
```

## Customizing the plugin

If you want to customize the location of the source or destination files, as well as other settings, take a look at
[pom-schema-fulldefs.xml](pom-schema-fulldefs.xml), as well as my blog post giving more details on the subject at
[http://grepalex.com/2013/05/24/avro-maven/](http://grepalex.com/2013/05/24/avro-maven/).

To see the customized pom.xml in action, use the following command:

```bash
$ mvn clean compile -f pom-schema-fulldefs.xml
```

The generated output files can be seen with the `find` command:

```bash
$ find . -type f -name *.java
./src/main/altjava/com/alexholmes/avro/Weather.java
./src/test/altjava/com/alexholmes/avro/Test.java
```
