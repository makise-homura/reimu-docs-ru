# Documentation

The actual documentation is [here](reimu.md)

# How to build documentation

## Overview of building scheme

```
git.conf ─────────────────┐ vars
                          ├──────► reimu.md
                     ┌────┘
reimu.template.md ───┤
                     └────┐ vars, links                  pandoc                                unzip, styles                                 zip
                          ├─────────────► reimu.espd.md ────────► reimu.espd.intermediate.odt ───────────────► reimu.espd.intermediate.data ─────► reimu.espd.odt
                     ┌────┘
espd.conf ───────────┤
                     └────┐ vars                       zip
                    unzip ├──────► root.template.data ─────► root.odm
root.template.odm ────────┘

```

Build stages:
* `vars`: substitute variables defined in `.conf` files
* `links`: remove links
* `pandoc`: convert `.md` to `.odt`
* `unzip`: unzip `.odt` to directory containing `.xml` files
* `styles`: alter list styles
* `zip`: zip directory containing `.xml` files back to `.odt`

Source files:
* `reimu.template.md`: The source of documentation in Markdown format, including places for variable substitution
* `root.template.odm`: Template of master ODF document, including title, ToC, and changelog pages
* `git.conf`: Variables for Markdown documentation
* `espd.conf`: Variables for ESPD ODF documentation

Created files:
* `reimu.md`: Markdown documentation
* `root.odm`: Master document of ESPD ODF documentation
* `reimu.espd.odt`: Slave document of ESPD ODF documentation

## Building

Just run `./build`.

You may run `./clean` to get rid of everything created during build.

Prerequisites:
* sed
* pandoc
* zip, unzip
* xmlstarlet

After you created the ODF documentation, you should do the following:
* Open the master document
* Update ToC
* Export file to ODF
* Open resulting ODF
* Break links as specified [here](https://wiki.openoffice.org/wiki/Documentation/OOo3_User_Guides/Writer_Guide/Creating_one_file_from_a_master_document)
* Save resulting ODF

## Configuration files

You may edit `git.conf` and `espd.conf` to specify some significant variables:
* `DN`: ESPD decimal number of product (has sense for `espd.conf` only)
* `NAME1`: First line of full product name
* `NAME2`: Second line of full product name
* `DESIGNEDTO`: a literal spelling of word "designed to"
