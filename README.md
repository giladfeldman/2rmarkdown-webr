# 2rmarkdown-webr

R packages compiled for [webR](https://docs.r-wasm.org/webr/) 0.6.0 (R 4.6,
WebAssembly), so that the 2Rmarkdown converters (SPSS, Stata, jamovi and JASP to
R Markdown) can run inside a web browser. They are not on webR's own package site,
either because they are not on CRAN or because the build there does not load in
webR 0.6.0.

Files are served free by jsDelivr, for example:

    https://cdn.jsdelivr.net/gh/giladfeldman/2rmarkdown-webr@<commit>/bin/emscripten/contrib/4.6/jsq_1.2.2.tgz

Address files by commit, not by branch, so that a given address always returns the
same bytes. `SHA256SUMS` lists every file's checksum; check it before installing.
The folder is also a regular webR package repository (`PACKAGES` index), usable as
`webr::install(pkgs, repos = "https://cdn.jsdelivr.net/gh/giladfeldman/2rmarkdown-webr@<commit>")`.

## What is here

| Package | Version | Source | License |
|---|---|---|---|
| spss2rmarkdown | 0.3.0 | [giladfeldman/spss2rmarkdown](https://github.com/giladfeldman/spss2rmarkdown) | MIT |
| stata2rmarkdown | 0.2.1 | [giladfeldman/stata2rmarkdown](https://github.com/giladfeldman/stata2rmarkdown) | MIT |
| jamovi2rmarkdown | 0.2.1 | [giladfeldman/jamovi2rmarkdown](https://github.com/giladfeldman/jamovi2rmarkdown) | MIT |
| jasp2rmarkdown | 0.3.0 | [giladfeldman/jasp2rmarkdown](https://github.com/giladfeldman/jasp2rmarkdown) | MIT |
| jsq | 1.2.2 | [jonathon-love/jsq@5d6409a](https://github.com/jonathon-love/jsq/tree/5d6409a2f28f23fcd2f09c96989543964c579dc3); source in `src/contrib` | GPL (>= 2) |
| surveymv | 0.7.1 | [raviselker/surveymv@08086bb](https://github.com/raviselker/surveymv/tree/08086bb2d1c3396495c860c444152cf6b52032e0); source in `src/contrib` | GPL (>= 2) |
| gamlj | 2.9.5 | [gamlj/gamlj@bdfa416](https://github.com/gamlj/gamlj/tree/bdfa4166ea91d5588e2000d9f740200a64cb339f); source in `src/contrib` | GPL |
| RSQLite | 3.53.3 | [CRAN](https://cran.r-project.org/package=RSQLite); source in `src/contrib` | LGPL (>= 2.1) |
| websocket | 1.2.0.9000 | Placeholder from [giladfeldman/jmv2gg](https://github.com/giladfeldman/jmv2gg), **not** the CRAN `websocket` package: it lets jmv's contingency tables load and opens no connections. Source in `src/contrib` | MIT |

The four converter binaries were built from commits that are ahead of their public
repositories; the public repositories will be brought up to date. Each binary carries
its own `DESCRIPTION` and `LICENSE`.

## How they were built

In the `ghcr.io/r-wasm/webr:v0.6.0` Docker image, with `LANG=C.UTF-8` (in the
image's default C locale non-ASCII strings such as `ε` come out as `<U+03B5>`):
`R CMD build`, then `rwasm`'s `wasm_build()` for each package.

No warranty. Problems with a converter: open an issue in that converter's repository.
