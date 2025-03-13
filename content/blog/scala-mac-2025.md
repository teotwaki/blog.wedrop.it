+++
title = "Getting started with Scala on macOS in 2025"
date = "2025-03-12"
description = "Collection of notes on how to setup my workstation to work with Scala."

[taxonomies]
tags = ["programming", "scala"]
+++

[Scala][scala-lang] is a functional programming language that I've come across in the past, but it
never stuck in my tool belt. One of my clients has asked me to help them with a billing project, and
as this is a Scala shop, I figured it would make sense to get a head start and setup my workstation
to be ready to work with Scala again.

[scala-lang]: https://www.scala-lang.org/

The best way to get started with Scala is by using [Coursier][coursier]; an application and artifact
manager for Scala. The official docs for both [Scala][scala-lang-download] and
[Coursier][coursier-install] seem to provide ~~incorrect~~suboptimal information for installation.
Both sources recommend installing `coursier/formulas/coursier` using `brew`, however that formula seems
to install an Intel binary, which obviously doesn't run on Apple silicon.
Instead, the [following workaround][github-coursier-intel] appears to work
quite well:

```bash
brew install coursier
coursier setup
```

[coursier]: https://get-coursier.io/
[scala-lang-download]: https://www.scala-lang.org/download/
[coursier-install]: https://get-coursier.io/docs/cli-installation
[github-coursier-intel]: https://github.com/coursier/coursier/issues/3292

Once you have coursier installed and setup, you should have a fully functional Scala build
environment. Here's the usual sanity check:

```scala
@main def hello() = println("Hello, World!")
```

Which you can run with `scala run hello.scala`. The output should look something like:

```text
Compiling project (Scala 3.6.4, JVM (23))
Compiled project (Scala 3.6.4, JVM (23))
Hello, World!
```

Fantastic. Now what's left to do is to enable code completion for Scala in nvim. `:LazyExtras`
should offer scala as a suggested language if you're editing the `hello.scala` file above, after
which a `:MetalsInstall` should install everything needed to get up and running.

Once Metals is installed, you should be able to see proper code completion. Sadly, type hints in the
form of inlays doesn't seem to be supported. This is an extremely useful feature that I've come to
absolute love when writing Rust, and I don't understand that it's not a priority for most LSPs. I
find it almost universally useful, regardless of the language.
