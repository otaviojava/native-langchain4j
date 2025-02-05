# Native LangChain4J example

This example is based on a [LangChain4j tutorial](https://github.com/langchain4j/langchain4j-examples). It produces a GraalVM native version of a chatbot leveraging LangChain4j and the OPENAI API.

### Prerequisites

* GraalVM (`sdk install java 21.0.2-graal`)
* Maven
* (optional) OPENAI API key

Note that you need to interact with the OpenAI API you need to either get and store an OpenAI API key in an environment variable `OPENAI_API_KEY`, or replace the value with `demo`.


## Package and run on the JVM

```shell
mvn package
```

## Interact with the bot

You now chat with your bot. You can execute the jar directly:

```shell
$ java -jar ./target/native-langchchain4j-1.0-jar-with-dependencies.jar "your prompt"
```


 or use the script from the repo for conciseness:

```shell
$ ./run.sh "what is Java?"

"Java is a high-level, class-based, object-oriented programming language that is designed to have as few implementation dependencies as possible. It is a general-purpose programming language intended to let application developers write once, run anywhere (WORA), meaning that compiled Java code can run on all platforms that support Java without the need for recompilation. Java is widely used for developing web applications, software, and mobile applications."

$ ./run.sh "what is GraalVM?"

"GraalVM is a high-performance runtime that provides significant improvements in application performance and efficiency. It is designed for applications written in JavaScript, Python, Ruby, R, JVM-based languages like Java, Scala, Groovy, Kotlin, and LLVM-based languages such as C and C++. GraalVM offers capabilities like ahead-of-time compilation and the ability to compile to a native executable to improve startup time, reduce memory footprint, and enable distribution of pre-compiled executables. It also supports interoperability between different programming languages, allowing you to write polyglot applications."

$ ./run.sh "what is love?"

"Love is a complex set of emotions, behaviors, and beliefs associated with strong feelings of affection, protectiveness, warmth, and respect for another person. It can also be described as a profound, passionate affection for another person and can emerge in various forms, such as familial love, romantic love, platonic love, and self-love. Love can also be understood as a function to keep human beings together against threats and to facilitate the continuation of the species."

```

## Package and run as Native Image

This demo works out of the box, but to get rid of a warning from a 4th party dependency, build it with config files (come with the repo):

```shell
native-image  -jar ./target/native-langchchain4j-1.0-jar-with-dependencies.jar -o native-langchain4j -H:ConfigurationFileDirectories=/Users/ayurenko/native-langchain4j/native-langchain4j/resources/META-INF/native-image
```

This produces a nice self-contained executable version of the app:

```shell
$ eza -l
.rwxr-xr-x  44M ayurenko 16 Mar 16:45 native-langchain4j
```

You can now chat with the native app:

```shell
$ ./native-langchain4j "what's the answer to life, the universe, and everything?"

42, according to "The Hitchhiker's Guide to the Galaxy" by Douglas Adams

```