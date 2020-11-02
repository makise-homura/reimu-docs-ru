# Documentation

The actual documentation is [here](reimu.md)

# How to build documentation

Just run `./build`.

Prerequisites:
* sed
* pandoc
* zip, unzip
* xmlstarlet

Created files:
* `reimu.md`: Markdown documentation
* `root.odm`: Master document of ESPD ODF docmentation
* `reimu.espd.odt`: Slave document of ESPD ODF docmentation

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
