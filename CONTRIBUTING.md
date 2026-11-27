# Contributing to The Protobuf Project

Thanks for helping. This guide applies to every repository in the
[the-protobuf-project](https://github.com/the-protobuf-project) organisation. A
repository with its own `CONTRIBUTING.md` adds to it: build commands, layout,
and release steps live there, and win where the two disagree.

New here? The [website](https://the-protobuf-project.org) explains how the pieces fit, the
[ecosystem](https://the-protobuf-project.org/ecosystem) lists every project with its docs, and the
[editor](https://the-protobuf-project.org/editor) shows what each plugin generates from one schema.

## Ways to help

You don't need to write code to contribute.

| You want to… | Do this |
| --- | --- |
| Report a bug | Open an issue with the **Bug report** form, including a minimal `.proto` that reproduces it |
| Ask for a feature | Open an issue with the **Feature request** form, describing the problem before the solution |
| Ask a question | See [SUPPORT.md](SUPPORT.md) for where questions get answered fastest |
| Fix docs or a typo | Open a pull request straight away; no issue needed |
| Fix a bug or add a feature | Comment on the issue first so work isn't duplicated, then open a pull request |
| Report a vulnerability | **Never in public.** Follow [SECURITY.md](SECURITY.md) |
| Write about it | Blog posts and talks are welcome; tell us and we'll link them |

Issues labelled `good first issue` are scoped for a first contribution, and
`help wanted` marks work maintainers would welcome help with.

## How the project fits together

Most repositories are one of four kinds, and knowing which one you are in tells
you where a change belongs:

- **Plugins** (`protoc-gen-*`) read `.proto` files and generate code. A
  change to generated output is a change to a plugin.
- **Runtimes** (`runtime-go`, `runtime-rs`, `runtime-ts`) are the libraries
  that generated code calls. Behaviour shared by every plugin lives here.
- **Foundations** such as `protokit` and `resourcename` are what plugins
  are built on.
- **Tooling** such as the linter action, the VS Code extension, and the
  Homebrew tap gets the plugins onto your machine and into CI.

If a fix seems to need changes in several repositories, say so in the issue;
we'll help split it into pull requests that can land in order.

## Schemas follow Google's AIPs

Every API in this project is designed against Google's
[API Improvement Proposals](https://google.aip.dev) and checked with
[api-linter](https://linter.aip.dev). In any `.proto` you add or change:

- Fix lint findings at the source rather than disabling rules.
- Use AIP resource names and standard methods (`Get`, `List`, `Create`,
  `Update`, `Delete`) unless the AIPs give a reason not to.
- Add new fields with new field numbers. Never renumber or reuse one; it breaks
  the wire format for every existing user.

## Making a change

1. **Fork and branch.** Work on a topic branch in your fork, not on `main`.
2. **Keep it focused.** One logical change per pull request. Unrelated
   cleanups go in their own.
3. **Test it.** Add or update tests that fail without your change. For a plugin,
   that usually means a golden file: regenerate it and commit the new output.
4. **Run the checks locally.** Each repository's README or `CONTRIBUTING.md`
   lists its lint, test, and build commands. CI runs the same ones.
5. **Document it.** Behaviour users can see belongs in the README or docs in the
   same pull request.
6. **Open the pull request.** The template asks what changed and why. Link the
   issue it closes.

### Commit messages

We use [Conventional Commits](https://www.conventionalcommits.org) so changelogs
and release notes can be generated:

```text
feat(store): generate soft-delete filters for List
fix(mcp): escape tool names that collide with reserved words
docs: explain the resource-name template syntax
```

Common types are `feat`, `fix`, `docs`, `refactor`, `test`, `build`,
`ci`, and `chore`. Mark a breaking change with `!` (`feat!: …`) and
describe it in the body.

### Code style

- Let the formatter decide: `gofmt`/`goimports`, `rustfmt`, Biome, or whatever
  the repository configures. Don't hand-format.
- Keep files small and single-purpose. Split a module before it becomes hard to
  read in one screen.
- Generated files carry a `Code generated … DO NOT EDIT.` header. Change the
  generator, not its output.
- Comment *why*, not *what*: the code already says what it does.

## Review

- A maintainer aims to give a first response within a week. If a pull request
  has been quiet longer, a polite ping on it is welcome.
- CI must pass before review. If it fails for reasons unrelated to your change,
  say so in the pull request.
- Reviews are about the change, never the person. Expect questions; they are how
  we keep the generated code predictable for everyone downstream.
- Maintainers squash-merge, so your pull request title becomes the commit
  message. Make it a good Conventional Commit.

## Licensing

Unless a repository says otherwise, The Protobuf Project is licensed under
[Apache 2.0](https://the-protobuf-project.org/license). By submitting a contribution you agree it is
licensed under the same terms as the repository it is made to.

## Recognition

Everyone who lands a contribution is credited on the
[contributors page](https://the-protobuf-project.org/contributors), which is updated from GitHub
automatically.

## Conduct

Everyone taking part is expected to follow the
[Code of Conduct](CODE_OF_CONDUCT.md).
