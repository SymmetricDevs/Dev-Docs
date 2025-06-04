# SUSY Dev Docs

To develop locally, install [Rust](https://www.rust-lang.org/tools/install), and then:

```sh
git clone https://github.com/SymmetricDevs/Dev-Docs.git
cd Dev-Docs
cargo install mdbook mdbook-mermaid  mdbook-admonish mdbook-linkcheck mdbook-emojicodes
mdbook serve
```

Or if you're a freak there's the nix flake ;)

For most PR's however its probably not necessary to actually install mdbook and check because, its like, markdown.
