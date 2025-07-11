# clap-markdown

[![Crates.io](https://img.shields.io/crates/v/clap-markdown.svg)](https://crates.io/crates/clap-markdown)
![License](https://img.shields.io/crates/l/clap-markdown.svg)
[![Documentation](https://docs.rs/clap-markdown/badge.svg)](https://docs.rs/clap-markdown)

#### [API Documentation](https://docs.rs/clap-markdown) | [Changelog](./docs/CHANGELOG.md) | [Contributing](#contributing)

Automatically generate Markdown documentation for
[`clap`](https://crates.io/crates/clap) command-line tools.

## Examples

Generate Markdown text for a basic `clap` app:

```rust
#[derive(clap::Parser)]
struct Cli {
    #[arg()]
    name: String,
}

let markdown: String = clap_markdown::help_markdown::<Cli>();
```

**Generated Markdown Examples:**

See `clap` example programs and the corresponding Markdown generated by
`clap-markdown`:

| Program                                              | Markdown                                         |
|------------------------------------------------------|--------------------------------------------------|
| [`./complex_app.rs`](./docs/examples/complex_app.rs) | [complex-app.md](./docs/examples/complex-app.md) |

### Usage Convention: `CommandLineHelp.md`

This section describes a suggested convention for using `clap-markdown` to
generate a `CommandLineHelp.md` file, which can be committed to source control
and viewed as online documentation.

1. Add a hidden `--markdown-help` option to your `clap` application:

  ```rust
  use clap::Parser;

  #[derive(Parser)]
  struct Cli {
      #[arg(long, hide = true)]
      markdown_help: bool,
  }

  fn main() {
      let args = Cli::parse();

      // Invoked as: `$ my-app --markdown-help`
      if args.markdown_help {
          clap_markdown::print_help_markdown::<Cli>();
      }
  }
  ```

2. Invoke `--markdown-help` to generate a `CommandLineHelp.md` file:

  ```shell
  $ cargo run -- --markdown-help > docs/CommandLineHelp.md
  ```

3. Save `CommandLineHelp.md` in git, and link to it from the project's README.md
   or other relevant documentation.

> For projects that have multiple associated executables, consider using the
> command name as a suffix. For example: `CommandLineHelp-your-app.md`,
> `CommandLineHelp-other-app.md`.

> Comitting `CommandLineHelp.md` to version control makes it easy to track
> user-visible changes to the command-line interface.

#### Projects using `clap-markdown`

The following projects use `clap-markdown` to generate a `CommandLineHelp.md`
reference document:

* [`wolfram-app-discovery`](https://crates.io/crates/wolfram-app-discovery)
  — [`CommandLineHelp.md`](https://github.com/WolframResearch/wolfram-app-discovery-rs/blob/master/docs/CommandLineHelp.md)
* [`wolfram-cli`](https://github.com/ConnorGray/wolfram-cli)
  — [`CommandLineHelp.md`](https://github.com/ConnorGray/wolfram-cli/blob/main/docs/CommandLineHelp.md)

<small><i>
To request the addition of a project to this list, please file an issue.
</i></small>

## Compatibility with clap

When this crate adds support for a new MAJOR version of `clap`, the MAJOR
version number of `clap-markdown` will be changed.

**Compability History:**

| `clap-markdown` | `clap`    |
|-----------------|-----------|
| v0.0.1 – v0.1.5 | `"4.*.*"` |


## License

Licensed under either of

  * Apache License, Version 2.0
    ([LICENSE-APACHE](./LICENSE-APACHE) or <http://www.apache.org/licenses/LICENSE-2.0>)
  * MIT license
    ([LICENSE-MIT](./LICENSE-MIT) or <http://opensource.org/licenses/MIT>)

at your option.


## Contributing

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.

See [**Development.md**](./docs/Development.md) for instructions on how to
perform common development tasks.

See [*Maintenance.md*](./docs/Maintenance.md) for instructions on how to
maintain this project.
