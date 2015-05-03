[![Build Status](https://travis-ci.org/nerdle/nerdle.svg?branch=master)](https://travis-ci.org/nerdle/nerdle)

Nerdle
======

Topic-Specific Question Answering Using Wikia Seeds

## Summary

The WIKIA project maintains wikis across a diverse range of subjects from areas of popular culture. Each wiki consists of collaboratively authored content and focuses on a particular topic, including franchises such as “Star Trek”, “Star Wars” and “The Simpsons”. Nerdle is a topic-expert Question Answering system which can answer questions on a particular topic and supports factoid question types.

## Get Started

### Prerequisites

* Apache Maven 3
* Java >= 1.7

### Build from source
```
git clone https://github.com/nerdle/nerdle.git
cd nerdle
mvn clean package
```
_Nerdle_ is now installed in `nerdle/target`

### Maven dependency
```shell
git clone https://github.com/nerdle/nerdle.git
cd nerdle
mvn clean install
```
_Nerdle_ is now installed in your local maven repository.

```xml
<dependency>
   <groupId>de.textmining</groupId>
   <artifactId>nerdle-core</artifactId>
   <version>0.0.1-SNAPSHOT</version>
</dependency>
```
## Demo

We present a Web demonstrator in which users can query the fact base. http://www.textmining.tu-berlin.de/nerdle/

## Sample Usage

Use a question answering system to answer natural language questions. Lets take a simple example for how to use the system.

Using `NerdleAnswerer` and a `FactProvider` you can now pose natural language questions to the system. The system can run on a rational database (`DBFactProvider`) over jdbc.

* DBFactProvider

```java
public class MyNerdle {

    public static void main(String[] args) throws Exception {
        String topic = "nerdle_test";
        DBSingleton dbSingleton = new DBSingleton();
        DBConnection dbConnection = dbSingleton.getConnections().get(topic);
        FactProvider factProvider = new DBFactProvider(dbConnection);

        NerdleAnswerer nerdleAnswerer = new NerdleAnswerer();
        nerdleAnswerer.getAnswers(factProvider, "Who is funny?", 1);
    }

}
```

For each _topic_ you have to provide a `FactProvider` using the `nerdle_config.properties` file. To create the file use the `nerdle_config_template.properties`. Put this file in `src/main/resources/nerdle_config.properties`.

```data
# H2 database configuration

jdbc=jdbc:h2:
db.db1.name=simpsons
db.db1.path=/path/to/db
db.db2.name=star-trek
db.db2.path=/path/to/db
db.db3.name=star-wars
db.db3.path=/path/to/db

# MV key-value configuration

mv.mv1.name=simpsons
mv.mv1.path=/path/to/db
mv.mv2.name=star-trek
mv.mv2.path=/path/to/db
mv.mv3.name=star-wars
mv.mv3.path=/path/to/db
```

For junits tests the `src/test/resources/nerdle_test_config.properties` file is used.

## Citing Nerdle

If you use Nerdle in your academic work, please cite Nerdle with the following BibTeX citation:

```latex
@InProceedings{maqsud-EtAl:2014:ColingDemo,
  author    = {Maqsud, Umar  and  Arnold, Sebastian  and  H\"{u}lfenhaus, Michael  and  Akbik, Alan},
  title     = {Nerdle: Topic-Specific Question Answering Using Wikia Seeds},
  booktitle = {Proceedings of COLING 2014, the 25th International Conference on Computational Linguistics: System Demonstrations},
  month     = {August},
  year      = {2014},
  address   = {Dublin, Ireland},
  publisher = {Dublin City University and Association for Computational Linguistics},
  pages     = {81--85},
  url       = {http://www.aclweb.org/anthology/C14-2018}
}
```

## License

_Nerdle_ is licensed under the Apache Software License Version 2.0. For more
information please consult the LICENSE file.
