# Solidify Getting Started with Coursier

## Proposer

Proposed by Chris Kipp, on behalf of Lunatech, 06-08-2021

## Abstract

Coursier has become a tool that either directly or indirectly every Scala
developer depends on. It packs an incredibly impressive feature set. With the
addition of the `cs setup` functionality it's no surprise that it's becoming an
increasingly more popular option to not just setup the common Scala toolchain,
but to also maintain Java versions and launch applications. Coursier has
transitioned from a power-user tool to a tool that is now possibly the first
Scala tool a newcomer to the language encounters.

With that in mind, contrasting various UI elements to other common tools used
for somewhat similar purposes, Couriser is lagging behind. With an overwhelming
help menu (see `cs java -h`), varying installation instructions found on the
Scala website, and unclear details about what exact versions and specific
launchers (looking at you sbt) are being installed, it brings unnecessary
confusion to the individuals first time with Scala.

## Proposal

There are a few concrete things we can do ensure that the first experience
someone has with Scala through Coursier and the continued experience is a
positive one.


### 1. Unify the Scala website installation instructions

Currently depending on the which part of the site you're on you'll get different
instructions about how to get started.

#### Examples

- Here on the [Scala 3 download page](https://scala-lang.org/download/scala3.html) you'll
    notice it mentions Coursier as one of the easiest ways to get started with
    Scala. However, there is no mention of `cs setup` and instead simply
    mentions using it to install `scala3-compiler` and `scala3-repl`. This
    already causes confusion for newcomers. Which do I install? Which do I need?
    What if I don't have Java installed?
- Here on the [Scala 2 download
    page](https://scala-lang.org/download/scala2.html) there is no mention of
    Coursier anywhere, but instead tells you to install either sbt or IntelliJ
    to get started. Furthermore there is another section that mentions SDKMAN!,
    MacPorts, Brew, and directly downloading the binaries as alternative ways to
    install Scala.

#### Potential solution

If Coursier is indeed the recommended way to get started with Scala, ensure that
all the official documentation points to that. Also ensure that everything is
covered when mentioning Coursier. For example, Alex Archambault has a [fantastic
article](https://alexarchambault.github.io/posts/2020-09-21-cs-setup.html) about
setup which could be used as further inspiration.

### 2. Improve the Courser CLI user experience.

The help options in Coursier are quite overwhelming and it's unclear if all of
the options are actually relevant for a user. It's also impossible to see the
versions of an application you have installed via Coursier and also difficult to
parse some of the very long output.

#### Examples

- When using `cs java -h` you are met with almost 50 options. Some also seem to
    be irrelevant for setting up Java. To name a few: `--sbt-plugin-hack`,
    `--log-changing`, `--drop-info-attr`. Compared to other common tools to
    install Java such as [SDKMAN!](https://sdkman.io/), this is quite
    overwhelming. I'll include the full output of both options below to further
    illustrate.

<details>
<summary>cs java -h output</summary>
<br>

```
❯ cs java -h
Command: java
Usage: cs java
  --installed  <bool>
  --available  <bool>
  --jvm  <string?>
  --jvm-dir  <string?>
  --system-jvm  <bool?>
  --local-only  <bool>
  --update  <bool>
  --jvm-index  <string?>
  --repository | -r  <maven|sonatype:$repo|ivy2local|bintray:$org/$repo|bintray-ivy:$org/$repo|typesafe:ivy-$repo|typesafe:$repo|sbt-plugin:$repo|scala-integration|scala-nightlies|ivy:$pattern|jitpack|clojars|jcenter|apache:$repo>
        Repository - for multiple repositories, separate with comma and/or add this option multiple times (e.g. -r central,ivy2local -r sonatype:snapshots, or equivalently -r central,ivy2local,sonatype:snapshots)
  --no-default  <bool>
        Do not add default repositories (~/.ivy2/local, and Central)
  --sbt-plugin-hack  <bool>
        Modify names in Maven repository paths for sbt plugins
  --drop-info-attr  <bool>
        Drop module attributes starting with 'info.' - these are sometimes used by projects built with sbt
  --channel  <org:name>
        Channel for apps
  --default-channels  <bool>
        Add default channels
  --contrib  <bool>
        Add contrib channel
  --file-channels  <bool>
        Add channels read from the configuration directory
  --repository | -r  <maven|sonatype:$repo|ivy2local|bintray:$org/$repo|bintray-ivy:$org/$repo|typesafe:ivy-$repo|typesafe:$repo|sbt-plugin:$repo|scala-integration|scala-nightlies|ivy:$pattern|jitpack|clojars|jcenter|apache:$repo>
        Repository - for multiple repositories, separate with comma and/or add this option multiple times (e.g. -r central,ivy2local -r sonatype:snapshots, or equivalently -r central,ivy2local,sonatype:snapshots)
  --no-default  <bool>
        Do not add default repositories (~/.ivy2/local, and Central)
  --sbt-plugin-hack  <bool>
        Modify names in Maven repository paths for sbt plugins
  --drop-info-attr  <bool>
        Drop module attributes starting with 'info.' - these are sometimes used by projects built with sbt
  --channel  <org:name>
        Channel for apps
  --default-channels  <bool>
        Add default channels
  --contrib  <bool>
        Add contrib channel
  --file-channels  <bool>
        Add channels read from the configuration directory
  --cache  <string?>
        Cache directory (defaults to environment variable COURSIER_CACHE, or ~/.cache/coursier/v1 on Linux and ~/Library/Caches/Coursier/v1 on Mac)
  --mode | -m  <offline|update-changing|update|missing|force>
        Download mode (default: missing, that is fetch things missing from cache)
  --ttl | -l  <duration>
        TTL duration (e.g. "24 hours")
  --parallel | -n  <int>
        Maximum number of parallel downloads (default: 6)
  --checksum  <checksum1,checksum2,...>
        Checksum types to check - end with none to allow for no checksum validation if no checksum is available, example: SHA-256,SHA-1,none
  --retry-count  <int>
        Retry limit for Checksum error when fetching a file
  --cache-file-artifacts | --cfa  <bool>
        Flag that specifies if a local artifact should be cached.
  --follow-http-to-https-redirect  <bool>
        Whether to follow http to https redirections
  --credentials  <host(realm) user:pass|host user:pass>
        Credentials to be used when fetching metadata or artifacts. Specify multiple times to pass multiple credentials. Alternatively, use the COURSIER_CREDENTIALS environment variable
  --credential-file  <string*>
        Path to credential files to read credentials from
  --use-env-credentials  <bool>
        Whether to read credentials from COURSIER_CREDENTIALS (env) or coursier.credentials (Java property), along those passed with --credentials and --credential-file
  --quiet | -q  <counter>
        Quiet output
  --verbose | -v  <counter>
        Increase verbosity (specify several times to increase more)
  --progress | -P  <bool>
        Force display of progress bars
  --log-changing  <bool>
        Log changing artifacts
  --log-channel-version | --log-index-version | --log-jvm-index-version  <bool>
        Log app channel or JVM index version
  --env  <bool>
  --disable-env | --disable  <bool>
  --setup  <bool>
  --user-home  <string?>
```

</details>


<details>
<summary>sdk help output</summary>
<br>

```
❯ sdk help

Usage: sdk <command> [candidate] [version]
       sdk offline <enable|disable>

   commands:
       install   or i    <candidate> [version] [local-path]
       uninstall or rm   <candidate> <version>
       list      or ls   [candidate]
       use       or u    <candidate> <version>
       config
       default   or d    <candidate> [version]
       home      or h    <candidate> <version>
       env       or e    [init|install|clear]
       current   or c    [candidate]
       upgrade   or ug   [candidate]
       version   or v
       broadcast or b
       help
       offline           [enable|disable]
       selfupdate        [force]
       update
       flush             [archives|tmp|broadcast|version]

   candidate  :  the SDK to install: groovy, scala, grails, gradle, kotlin, etc.
                 use list command for comprehensive list of candidates
                 eg: $ sdk list
   version    :  where optional, defaults to latest stable if not provided
                 eg: $ sdk install groovy
   local-path :  optional path to an existing local installation
                 eg: $ sdk install groovy 2.4.13-local /opt/groovy-2.4.13
```

</details>


#### Potential solution

Do some initial research on other common CLI tools in various language
ecosystems to get inspiration on a cleaner user experience. Possibly draw
some inspiration from SKDMAN! as it's a popular alternative to Coursier to
manage your Java versions. After the initial research there will need to be
changes made to the CLI module of Coursier and possibly even
[`case-app`](https://github.com/alexarchambault/case-app), which is the library
Coursier uses for the CLI.

### 3. Clarify and agree on the applications in `cs setup`

It's not always clear what exact application is being installed. sbt is a great
example of this when installed with Coursier. Also, how is the default
applications determined for Coursier?

#### Examples

- While this could be an entire proposal on its own, there are multiple
    sbt launchers that are floating around the ecosystem. When using Coursier
    it's not fully clear which is actually being installed and users at times
    are met with very slight differences between the launchers that are
    extremely difficult for newcomers and at times veterans to spot, unless you
    are knowledgeable about the slight differences between launchers. The [sbt
    documentation](https://www.scala-sbt.org/download.html) makes no mention of
    Coursier being an official way to download the _official_ launcher.
- Scala 2 is installed by default, but not Scala 3. Is there a reason for this?

#### Potential solutions

- Align on what exact applications are being installed. If it's not the default
    sbt launcher, there should be an incredibly good reason that it's not. If
    you search the various Scala help channels you'll find people tripping up on
    this in every one.
- What default applications are installed with Coursier? Does the current set
    make sense? Should they include any more to make an even smoother getting
    started experience? This should be discussed, agreed upon, and updated.

## Cost

This cost of this is difficult to pin down as it's dependent on which of the 3
outlined parts of the proposal are agreed upon. In level of difficulty I'd
estimate the following order (from easiest to hardest):

1. Unify the Scala website installation instructions
2. Clarify and agree on the applications in `cs setup`
3. Improve the Courser CLI user experience

## Timescales

I see unifying the Scala website installation instructions as something that
could be done rather quickly. Parts of clarifying and agreeing on what
applications are included in `cs setup` should also be somewhat quick unless
there specific reasons for a specific distribution of an application being used.
For example, if there is a technical reason as to why the official sbt launcher
can't be included vs the Courser based sbt launcher.

The final proposal of improving the CLI user experience will be the most time
consuming as it will require research and probably a refactoring of the CLI
module in Coursier.

## Closing notes

I want to reiterate how important Coursier has become in the Scala community. I
also want to take a moment to identify the incredible amount of work and
dedication Alex Archambault has put into this project. This proposal is not
meant to reflect a frustration with Coursier at all, but rather to further
concrete it as the default way to get started with Scala and to do everything we
can to ensure that process is smooth, clear, and enjoyable.
