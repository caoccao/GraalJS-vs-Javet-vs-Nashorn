# GraalJS-vs-Javet-vs-Nashorn

A simple performance comparison of [GraalJS](https://github.com/oracle/graaljs), [Javet](https://github.com/caoccao/Javet) and Nashorn.

## Background

[Javet](https://github.com/caoccao/Javet) is Java + V8 (JAVa + V + EighT). It is an awesome way of embedding Node.js and V8 in Java.

Many potential [Javet](https://github.com/caoccao/Javet) users evaluate [Javet](https://github.com/caoccao/Javet) and GraalJS across many aspects. To save time for these users, I present a simple performance comparison of [GraalJS](https://github.com/oracle/graaljs), [Javet](https://github.com/caoccao/Javet) and Nashorn.

So I created this project based on [graal-js-jdk11-maven-demo](https://github.com/graalvm/graal-js-jdk11-maven-demo) which is a simple maven project that demonstrates how it's possible to run Graal.js on a stock JDK11. I enhanced it by adding Javet benchmark.

The test JS code snippet is a simple implementation of [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) which is an ancient algorithm for finding all prime numbers up to any given limit.

## Performance Comparison

### Windows

- CPU: AMD 5950X
- RAM: 128GB
- OS: Windows 10
- JDK: Corretto-11.0.10

### Windows with Warmup

| Iteration | GraalJS Polyglot | GraalJS ScriptEngine | Nashorn ScriptEngine | Javet |
|-----------|------------------|----------------------|----------------------|-------|
| 1         | 50               | 43                   | 171                  | 34    |
| 2         | 49               | 44                   | 169                  | 36    |
| 3         | 45               | 42                   | 172                  | 35    |
| 4         | 51               | 45                   | 169                  | 34    |
| 5         | 49               | 43                   | 171                  | 36    |
| 6         | 43               | 44                   | 170                  | 35    |
| 7         | 43               | 46                   | 175                  | 35    |
| 8         | 47               | 45                   | 171                  | 35    |
| 9         | 46               | 43                   | 170                  | 35    |
| 10        | 48               | 46                   | 171                  | 35    |

### Windows without Warmup

| Iteration | GraalJS Polyglot | GraalJS ScriptEngine | Nashorn ScriptEngine | Javet |
|-----------|------------------|----------------------|----------------------|-------|
| 1         | **639**          | **135**              | **292**              | **51**|
| 2         | **109**          | **71**               | 188                  | 27    |
| 3         | **84**           | 39                   | 177                  | 36    |
| 4         | **86**           | 41                   | 174                  | 38    |
| 5         | **67**           | 38                   | 176                  | 35    |
| 6         | **84**           | 48                   | 176                  | 38    |
| 7         | 43               | 46                   | 174                  | 35    |
| 8         | 46               | 42                   | 175                  | 36    |
| 9         | 43               | 45                   | 173                  | 37    |
| 10        | 49               | 49                   | 174                  | 35    |

### MacOS

- CPU: M2 Max
- RAM: 64GB
- OS: Ventura 13.5.2
- JDK: Corretto-11.0.19.7.1

### MacOS with Warmup

| Iteration | GraalJS Polyglot | GraalJS ScriptEngine | Nashorn ScriptEngine | Javet |
|-----------|------------------|----------------------|----------------------|-------|
| 1         | 84               | 63                   | 778                  | 32    |
| 2         | 84               | 70                   | 789                  | 31    |
| 3         | 82               | 60                   | 778                  | 33    |
| 4         | 85               | 73                   | 779                  | 34    |
| 5         | 84               | 60                   | 776                  | 31    |
| 6         | 84               | 63                   | 780                  | 31    |
| 7         | 82               | 73                   | 780                  | 31    |
| 8         | 82               | 61                   | 773                  | 30    |
| 9         | 82               | 75                   | 784                  | 30    |
| 10        | 82               | 61                   | 775                  | 32    |

### MacOS without Warmup

| Iteration | GraalJS Polyglot | GraalJS ScriptEngine | Nashorn ScriptEngine | Javet |
|-----------|------------------|----------------------|----------------------|-------|
| 1         | **329**          | **101**              | **862**              | **39**|
| 2         | **117**          | 90                   | 788                  | 28    |
| 3         | 88               | 95                   | 774                  | 31    |
| 4         | 83               | 75                   | 794                  | 33    |
| 5         | 92               | 76                   | 778                  | 31    |
| 6         | 82               | 78                   | 772                  | 38    |
| 7         | 85               | 80                   | 785                  | 31    |
| 8         | 87               | 81                   | 778                  | 32    |
| 9         | 87               | 67                   | 795                  | 32    |
| 10        | 92               | 72                   | 783                  | 32    |

## Conclusion

TODO

## Benchmark

### Pre-requirements

- Windows, Linux or MacOS
- [Maven](https://maven.apache.org)
- [JDK11](https://jdk.java.net/11/)

### Setup

- Clone this repository

```sh
git clone https://github.com/caoccao/GraalJS-vs-Javet-vs-Nashorn.git
```

- Navigate to the newly cloned directory

```sh
cd GraalJS-vs-Javet-vs-Nashorn
```

- Make sure that `JAVA_HOME` is pointed at a JDK11

```sh
# Windows
set JAVA_HOME=\path\to\jdk11

# Linux or MacOS
export JAVA_HOME=/path/to/jdk11
```

- Package the project using Maven

```sh
mvn package
```

### Run

- To Execute with Graal run

```sh
mvn exec:exec
```

- To Execute without Graal run

```sh
mvn exec:exec@nograal
```

The benchmark prints the time per iteration in milliseconds, so lower values are better.

## License

[APACHE LICENSE, VERSION 2.0](blob/main/LICENSE)
