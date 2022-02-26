# cargo-clean-all

A custom cargo comand that analyses all cargo `target` directories under a given parent directory 
and allows for cleaning them, following certain criteria. The cleaning-criteria include 
`keep target dirs last modified X days ago` and `keep target dirs with size less than X`. Before 
actually doing anything, the detected projects are listed with their individual and total target 
dir sizes. The actual cleaning must be confirmed unless `--yes` is specified.

I was shocked when I realized that my rust target directories took up a total of over 50gb, so I 
developed this tool to help me clean up all the project target dirs. There is already 
[cargo-clean-recursive](https://github.com/IgaguriMK/cargo-clean-recursive) which unfortunately 
doesn't support keeping recent files in order to not slow down the projects I'm currently working on.

## Installation

Install using cargo:
```
cargo install cargo-clean-all
```

## Usage

Clean all target directories under the current working directory.
```
cargo clean-all
```

Clean all target directories under the directory `[dir]`.
```
cargo clean-all --dir [dir]
```

Keep target directories that have a size of less than `[filesize]`.
```
cargo clean-all --keep-size [filesize]
```

Keep target directories younger than `[days]` days.
```
cargo clean-all --keep-days [days]
```

Specify the number of threads to use for the recursive scan .
```
cargo clean-all --threads [number of threads]
```

# Alternatives

## [cargo-clean-recursive](https://github.com/IgaguriMK/cargo-clean-recursive)

| Feature      | `cargo-clean-all` | `cargo-clean-recursive` |
|------------------------------------------------|:---:|:---:|
| Clean projects under current dir               | yes | yes |
| Clean projects under any dir                   | yes | no  |
| Display freed up / freeable disk space         | yes | no  |
| Keep target dirs below a size threshold        | yes | no  |
| Keep target dirs with a last modified treshold | yes | no  |
| Ask before cleaning                            | yes | no |
| Clean only `release`, `debug` or `docs`        | no (not yet)  | yes |
| Speed (non scientific, cleaning my home dir)   | 15 sec | 24 sec |
