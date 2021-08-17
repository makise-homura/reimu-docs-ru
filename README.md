# Documentation

The actual REIMU manual is [here](reimu.md).

Build documentation is [here](reimu-BUILD.md).

Integration documentation is [here](reimu-INTEGRATION.md).

# How to build documentation

## Overview of building scheme

```
*-git.conf ───────────────┐ vars
                          ├──────► reimu.md, reimu-BUILD.md, reimu-INTEGRATION.md
                     ┌────┘
*.template.md ───────┤
                     └────┐ vars, links              pandoc                            unzip, styles             zip               mv
                          ├─────────────► *.espd.md ────────► *.espd.intermediate.odt ───────────────► workdir/ ─────► *.espd.odt ────► result-*.*/
                     ┌────┘
*-espd.conf.* ───────┤
                     └────┐ vars             zip             mv
                    unzip ├──────► workdir/ ─────► root.odm ────► result-*.*/
*-root.template.odm ──────┘

```

Build stages:
* `vars`: substitute variables defined in `.conf` files
* `links`: remove links
* `pandoc`: convert `.md` to `.odt`
* `unzip`: unzip `.odt` to directory containing `.xml` files
* `styles`: alter list styles
* `zip`: zip directory containing `.xml` files back to `.odt`
* `mv`: move resulting `.odt` and `.odm` files to output directory

Source files:
* `{reimu,build,integration}.template.md`: The source of documentation in Markdown format, including places for variable substitution
* `{reimu,build}-root.template.odm`: Template of master ODF document, including title, ToC, and changelog pages
* `{reimu,build,integration}-git.conf`: Variables for Markdown documentation
* `{reimu,build}-espd.conf.*`: Variables for ESPD ODF documentation (`*` is `306`, `308`, and `dacn` for several output configurations)

Created files:
* `reimu.md`: Markdown documentation on usage
* `reimu-BUILD.md`: Markdown documentation on build
* `reimu-INTEGRATION.md`: Markdown documentation on integration
* `result-manual.*/root.odm`: Master document of ESPD ODF documentation on usage (`*` is `306`, `308`, and `dacn`)
* `result-manual.*/reimu.espd.odt`: Slave document of ESPD ODF documentation on usage (`*` is `306`, `308`, and `dacn`)
* `result-build.*/root.odm`: Master document of ESPD ODF documentation on build (`*` is `306`, `308`, and `dacn`)
* `result-build.*/build.espd.odt`: Slave document of ESPD ODF documentation on build (`*` is `306`, `308`, and `dacn`)

## Building

Just run `./build`.

You may run `./clean` to get rid of everything created during build.

Prerequisites:
* `sed`
* `pandoc`
* `zip`, `unzip`
* `xmlstarlet`

After you created the ODF documentation, you should do the following:
* Open the master document
* Update ToC
* Export file to ODF
* Open resulting ODF
* Break links as specified [here](https://wiki.openoffice.org/wiki/Documentation/OOo3_User_Guides/Writer_Guide/Creating_one_file_from_a_master_document)
* Save resulting ODF

## Configuration files

You may edit `*-git.conf` and `*-espd.conf.*` to specify some significant variables.

Variables related to document contents:
* `DN`: ESPD decimal number of product (has sense for `*-espd.conf.*` only)
* `NAME1`: First line of full product name
* `NAME2`: Second line of full product name
* `NAMEOF`: Full product name in genitive case (has sense for `*-espd.conf.*` only)
* `DESIGNEDTO`: a literal spelling of word "designed to"

Variables related to pipeline:
* `INPUTFILE`: Input Markdown template file name
* `ROOTTEMPLATE`: Input master template file name (has sense for `*-espd.conf.*` only)
* `MARKDOWNFILE`: Markdown slave document intermediate file name (has sense for `*-espd.conf.*` only)
* `INTERMEDIATE`: OpenDocument slave document intermediate file name (has sense for `*-espd.conf.*` only)
* `OUTPUTDATAFILE`: Resulting slave document file name (has sense for `*-espd.conf.*` only)
* `OUTPUTROOTFILE`: Resulting master document file name (has sense for `*-espd.conf.*` only)
* `OUTPUTDIR`: Directory for resulting files (has sense for `*-espd.conf.*` only)
* `OUTPUTFILE`: Resulting file name (has sense for `*-git.conf.*` only)
