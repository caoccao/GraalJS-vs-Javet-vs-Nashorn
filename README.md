# GraalJS vs. Javet vs. Nashorn

A simple performance comparison of [GraalJS](https://github.com/oracle/graaljs), [Javet](https://github.com/caoccao/Javet) and Nashorn.

## Background

[Javet](https://github.com/caoccao/Javet) is Java + V8 (JAVa + V + EighT). It is an awesome way of embedding Node.js and V8 in Java.

Many potential [Javet](https://github.com/caoccao/Javet) users evaluate [Javet](https://github.com/caoccao/Javet) and [GraalJS](https://github.com/oracle/graaljs), across many aspects. To save time for these users, I present a simple performance comparison of [GraalJS](https://github.com/oracle/graaljs), [Javet](https://github.com/caoccao/Javet) and Nashorn.

I created this project based on [graal-js-jdk11-maven-demo](https://github.com/graalvm/graal-js-jdk11-maven-demo) which is a simple maven project that demonstrates how it's possible to run Graal.js on a stock JDK11. I enhanced it by adding Javet benchmark.

The JS benchmark code snippet is a simple implementation of [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) which is an ancient algorithm for finding all prime numbers up to any given limit.

## Performance Comparison

### Environment

- Javet v2.2.3 (V8 v11.7)
- GraalJS v22.2.0
- Windows
  - CPU: AMD 5950X
  - RAM: 128GB
  - OS: Windows 10 22H2
  - JDK: Corretto-11.0.10.9.1
- MacOS
  - CPU: M2 Max
  - RAM: 64GB
  - OS: Ventura 13.5.2
  - JDK: Corretto-11.0.19.7.1

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

![Performance comparison with warmup on Windows](https://miro.medium.com/v2/resize:fit:960/format:webp/1*Sw2pd1wvo-en4hgKF8P0Sg.png)

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

![Performance comparison without warmup on Windows](https://miro.medium.com/v2/resize:fit:960/format:webp/1*4tUFO3w5kijc8AUYcVSttA.png)

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

![Performance comparison with warmup on MacOS](https://miro.medium.com/v2/resize:fit:960/format:webp/1*xbzQhJ8qtUApsta03XHnJA.png)

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

![Performance comparison without warmup on MacOS](https://miro.medium.com/v2/resize:fit:960/format:webp/1*ZFiFNYaHzX09AH6iLHaK3g.png)

### Throughput

![Throughput comparison](https://miro.medium.com/v2/resize:fit:960/format:webp/1*C8pRTGOv4sJGOEHkfRxMVQ.png)

## Conclusion

- GraalJS is ~10x slower than Javet is in the first round of the script execution.
- GraalJS is ~1.3x slower on Windows and ~2.5x slower on MacOS than Javet is with enough rounds of the warmup.
- Nashorn is ~5x slower on Windows and 20+x slower on MacOS than Javet is regardless of the warmup.
- In ad-hoc script execution scenarios, Gaming (e.g. Minecraft), PaaS + SaaS (e.g. Low code, no code), Time Critical (e.g. MQTT), etc., GraalJS is ~10x slower than Javet is. That makes Javet the de facto scripting engine on JVM.
- If the scripts are well warmed up, GraalJS performs not too bad and is acceptable. However, it's quite tricky to give even warmup chances to all the branches of the scripts. In practice, the cold branches slow down the execution so that the actual performance improvement from JIT is not that significant. Javet is still a much better solution.

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
