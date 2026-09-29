# Contributing to Axion IDE

Thanks for contributing! A few rules keep the project readable and safe.

## The ELI5 rule (non-negotiable)

Every non-trivial class, service, command, and property carries an **ELI5
comment** — one or two sentences a beginner would understand — and comments are
updated in the same commit as the code they describe. See the
[full convention](https://blivodev.github.io/Axion-IDE-Docs/dev/eli5-comment-convention/).

## Ground rules

1. **Open source only.** Libraries, frameworks, tools, and code must carry a
   permissive license (MIT, Apache-2.0, BSD, MPL...). No proprietary dependencies.
2. **Tests stay 100% green.** `dotnet test` before every commit.
3. **Versioning discipline.** Every feature/fix batch bumps the version in all
   5 `.csproj` files + UI strings, and adds a `CHANGELOG.md` entry.
4. **ELI5 comments** as above.

## Dev workflow

```bash
git clone https://github.com/blivodev/Axion-IDE.git
cd Axion-IDE
dotnet build
dotnet test
dotnet run --project src/Axion.App
```

See the [Building & Debugging guide](https://blivodev.github.io/Axion-IDE-Docs/dev/building-debugging/)
for the full release checklist (publish layout, retention rule, repomix).

## PRs

- Small, focused PRs win.
- Include ELI5 comments for anything new.
- Update the docs (`Axion-IDE-Docs` repo) when behavior changes.
