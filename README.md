# Textplus-FCS-Documents

## Text+

* [Specification Lexical Search `lexfcs/index.adoc`](lexfcs/index.adoc) (Version 0.1)

## CLARIN

* [CLARIN Federated Content Search (CLARIN-FCS) - Core 2.0 `fcs-core-2.0/index.adoc`](fcs-core-2.0/index.adoc)
* [CLARIN Federated Content Search (CLARIN-FCS) - Core 1.0 `fcs-core-1.0/index.adoc`](fcs-core-1.0/index.adoc)
* [CLARIN Federated Content Search (CLARIN-FCS) - Data Views 1.0 `fcs-dataviews-1.0/index.adoc`](fcs-dataviews-1.0/index.adoc)
* [CLARIN Federated Content Search (CLARIN-FCS) - AAI 1.0 `fcs-aai/index.adoc`](fcs-aai/index.adoc)

## ASCIIDoc

* [`themes/`](themes/) for both CLARIN and Text+

## How to build

Please take a look at the [Github Actions workflow definitions in `.github/workflows`](.github/workflows). All the specification documents will be built automatically when their source files change. (_NOTE: not sure about changes to the theme files. May need to trigger a manual build._)

All the specification documents are structured as follows in their sub folders:
- `index.adoc` entrypoint document that bundles and includes single chapters into one
- `attachments/` (optional) with schema files or similar
- `examples/` (optional) examples (or fragments) that are included in the specification document
- `images/` (optional) for images that will be in the specification
- `themes/` links to the global [`themes/`](themes/) folder with the `textplus` and `clarin` themes

You can build the specifications documents yourself with:

```bash
# Set spec you want to build
# Based on folder names, choose one of: fcs-core-1.0, fcs-core-2.0, fcs-aai, fcs-dataviews-1.0, lexfcs
NAME=fcs-core-2.0

# Output will be in `docs/`

# Build HTML
asciidoctor -v -D docs -a data-uri --backend=html5 -o ${NAME}.html ${NAME}/index.adoc

# Build PDF
asciidoctor-pdf -v -D docs -o ${NAME}.pdf ${NAME}/index.adoc

# (optional) Copy attachments
cp -R ${NAME}/attachments docs/

# (optional) Copy examples (are already included into the documents)
cp -R ${NAME}/examples docs/
```

You can use the [`asciidoctor/docker-asciidoctor` docker image](https://github.com/asciidoctor/docker-asciidoctor/blob/main/README.adoc) for building the specifications if you don't want to install various dependencies. Note that the build artifacts belong to the `root` user.

```bash
docker run --rm -it -v $(pwd):/documents asciidoctor/docker-asciidoctor
# then run your build commands
```
