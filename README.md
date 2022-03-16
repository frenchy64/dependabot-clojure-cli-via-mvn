# Leiningen Dependabot support via Maven

This repository demonstrates how you use dependabot's to (mostly) help
manage Leiningen project dependencies. The basic idea is to use `lein pom`
to generate a `pom.xml` for dependabot to inspect.

The downside is that the PR's sent by dependabot are not immediately mergable.
To compensate, this setup will make GitHub Actions fail in dependabot's PRs until you fix them yourself.

## Usage

Assuming you have a Leiningen project ready to go, adding dependabot support is a matter of
copying some files and code from this repo.

1. Copy `.github/dependabot.yml` to your repo. Notice that we've configured the `dependabot` as a Maven repository.
2. Copy `script/sync-dependabot` and `script/check-dependabot` to your repo.
3. Call `./script/sync-dependabot` in your repository root. Commit the generated `dependabot/pom.xml`.
4. Add a call to `./script/check-dependabot` in your CI build. It will fail if `dependabot/pom.xml` is out of date.
   - see `.github/workflows/build.yml` for an example
5. Commit and push.
