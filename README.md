# d34j — DDD for Java

[![CI](https://github.com/esalbuquerquebr/d34j/actions/workflows/ci.yml/badge.svg)](https://github.com/esalbuquerquebr/d34j/actions/workflows/ci.yml)
[![Maven Central](https://img.shields.io/maven-central/v/io.github.esalbuquerquebr/d34j)](https://central.sonatype.com/artifact/io.github.esalbuquerquebr/d34j)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A set of classes to assist in implementing projects using Domain-Driven Design (DDD) in Java 25.

## Installation

```xml
<dependency>
    <groupId>io.github.esalbuquerquebr</groupId>
    <artifactId>d34j</artifactId>
    <version>0.1.0</version>
</dependency>
```

## Development

### Prerequisites

- JDK 25+
- [Cocogitto](https://docs.cocogitto.io/) (for version bumping and changelog)

```bash
brew install cocogitto
```

### Setup

Clone the repository and configure git hooks:

```bash
git clone https://github.com/esalbuquerquebr/d34j.git
cd d34j
git config core.hooksPath .githooks
chmod +x .githooks/*
```

### Build

```bash
./mvnw compile
```

### Format

Check formatting:

```bash
./mvnw spotless:check
```

Auto-fix formatting:

```bash
./mvnw spotless:apply
```

### Commit Convention

This project follows [Conventional Commits](https://www.conventionalcommits.org/). The git hook will reject non-conforming messages.

```
feat: add Entity base class
fix(value-object): correct equals implementation
feat!: remove deprecated API
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`

## Release

### Version Bump

Cocogitto analyzes commit history and determines the next semantic version automatically:

```bash
cog bump --auto
```

This will:
1. Determine the next version from commit history (feat → minor, fix → patch, breaking → major)
2. Update `pom.xml` with the new version
3. Generate/update `CHANGELOG.md`
4. Create a git tag (`v<version>`)
5. Push the commit and tag

The tag push triggers the CD workflow, which publishes to Maven Central.

### Manual Bump

```bash
cog bump --major   # 0.1.0 → 1.0.0
cog bump --minor   # 0.1.0 → 0.2.0
cog bump --patch   # 0.1.0 → 0.1.1
```

### GitHub Secrets (required for CD)

| Secret | Description |
|--------|-------------|
| `GPG_PRIVATE_KEY` | ASCII-armored GPG private key (`gpg --armor --export-secret-keys KEY_ID`) |
| `GPG_PASSPHRASE` | Passphrase for the GPG key |
| `CENTRAL_USERNAME` | Sonatype Central Portal user token username |
| `CENTRAL_TOKEN` | Sonatype Central Portal user token password |

Generate Central Portal tokens at https://central.sonatype.com → View Account → Generate User Token.

## License

[MIT](LICENSE)