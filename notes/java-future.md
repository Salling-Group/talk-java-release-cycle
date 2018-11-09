---
title: |
  Overview of new Java\
  release and licensing strategy
subtitle: or, "_can I use `var` yet?_"
sansfont: DejaVu Sans
slide-numbers: true
links-as-notes: true
---

# watsit

## Motivation

\center\includegraphics[width=4\TPHorizModule]{../media/shot-java.jpg}

## Primary resources

- \href{https://bit.do/java-still-free}{Java Is Still Free}
- \href{https://blog.joda.org/}{Stephen Colebourne}
- \href{https://www.reddit.com/r/java}{/r/java}

## Terminology

> - "feature": new toys
> - "update": toy maintenance
> - "support": babysitters
> - "free as in beer" a.k.a. "\$free": gratis
> - "free as in speech" a.k.a. "free": unconstrained
> - "development": something that supports yourself
> - "production": something that supports others

## Guiding principles

> "_Maybe jumping on the "release train" is right for you or maybe sticking to
> LTS is, but making a big commitment to either right now, based on
> speculation, is neither wise nor necessary._" --- /u/pron98

## Guiding principles

- Reduce unnecessary risk
    - Big decisions not _necessary_ yet
    - Community has no experience with new strategy yet
    - Stay with HotSpot
- Reduce development and operational overhead
    - Spend less time on upgrades
    - Require less buy-in for upgrading
    - More toys faster
- Expect responsible maintenance
    - Updates regularly, in timely manner
- Reassess in 2020
    - Better understanding of impact of new strategy
    - Expected biggest obstacle: third-party dependencies (i.e. not JDK or JVM)

# New release strategy

## Versioning

- Java language: \$FEATURE.0.\$UPDATE (e.g. 11.0.1)
- Java SE runtime: \$YEAR.\$MONTH (e.g. 18.10)
- JRE: superseded by LTO via `jlink`
- No more "major" versions

## Release plan

- Feature release every 6 months, starting March 2018
    - Features get updates for 6 months
- Update release every 3 months, starting January 2018
    - I.e. 2 updates per feature
- LTS feature release every 3 years, starting September 2018

## "Long-term" support

- "Updates available for at least three years, possibly longer"
    - ... but not from Oracle, unless we pay
- Feature-to-feature upgrade "easy"
- LTS-to-LTS upgrade "as difficult as 7-to-8 or 8-to-9"

# New licensing

## OpenJDK by any other name

\center\includegraphics{../media/openjdk.png}

## \href{https://openjdk.java.net/}{Oracle}

- OpenJDK
    - Gratis in production
    - No extended update period\footnote{Approximately 1 month to update to new
      feature release}
    - No support
- Oracle JDK
    - Gratis for development, subscription license for production
    - Extended update period
    - Includes support

## \href{https://adoptopenjdk.net/}{AdoptOpenJDK}

- OpenJDK
    - Gratis in production
    - Best-effort extended update period
        - LTS updates by community, probably stewarded by ~~Red Hat~~ IBM
    - No support

## \href{https://www.azul.com/downloads/zulu/}{Azul}

- Zulu Community
    - Gratis in production
    - No extended update period
    - No support
- Zulu Enterprise
    - Extended update period
        - additional concept of _medium-term_ support
    - Includes support

## Distro versions

- Comparable to AdoptOpenJDK
    - ... but be mindful of which _version_ is distributed

## Others

- Basically same story

# Recommendations\
for next 18 months

## Developers

- Use distro\footnote{If not an option, use AdoptOpenJDK} OpenJDK
- Build on JDK._LTS_\footnote{Expect to be stuck on Java 8 for a while}
- Test build on
    - JDK._LTS_
    - JDK._stable_
    - JDK._next_\footnote{\textit{Super} important}\footnote{Also really easy
      in Travis CI}

## Operations

- Provide JDK._LTS_, JDK._stable_, **and** JDK._next_
    - Use distro\footnote{If not an option, use AdoptOpenJDK} OpenJDK
    - For _future option_ of paid support, use Azul Zulu
- Use JDK._LTS_ in production\footnote{We still have to keep it updated}
    - Consider shift to per-application JDK\footnote{This may happen
      automatically as LTO becomes common}

## Avoid

- Oracle JDK in production --- requires license and we don't use commercial
  support today anyway\footnote{Not because we shouldn't pay but because we
  don't use what we'd be paying for}
- Oracle JDK 8 in development --- legal but pointless
- Oracle OpenJDK 8 in development --- legal but pointless
- Oracle OpenJDK in production --- legal but irresponsible
- Neglecting JDK in production
- Relying on `--release=<platform JDK>`\footnote{We still need to specify it}
  --- too superficial guarantees
- JDK._stable_ in production --- third-party dependencies could trip us up

# _Or else..._

## What if we don't get in line?

- We'll be increasingly vulnerable to exploits
- People won't want to work for us
- Alternatively, we'll expose ourselves to litigation

# Summary

## Summary

- Prioritized list of OpenJDK builds, subject to perspective on support need
    1. Distro OpenJDK
    1. AdoptOpenJDK
    1. Azul Zulu or Oracle JDK
- Build for JDK._LTS_
- Run on JDK._LTS_
- Test on JDK._next_
- Revisit in 12-18 months
