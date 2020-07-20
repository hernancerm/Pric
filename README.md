# 👨🏻‍💻 Pric: Print Code

The goal of this tool is to provide an easy and fast way to produce a PDF out of a set of code files.

## Usage

Given the following project, we can generate a PDF out of the Java files.

```
.
`-- src
    |-- META-INF
    |   `-- MANIFEST.MF
    `-- hercerm
        `-- iindices
            |-- app
            |   |-- ApplicationStarter.java
            |   `-- WordSearcherApplication.java
            |-- core
            |   |-- FileContentCleanser.java
            |   |-- IIValue.java
            |   |-- IIndexGenerator.java
            |   |-- REPL.java
            |   |-- REPLCommands.java
            |   |-- TXTCleanser.java
            |   `-- WordSearcher.java
            `-- util
                |-- FileDownloader.java
                |-- PathsAccessor.java
                `-- Serializer.java

```

To create the PDF, simply run:

```bash
pric output_file.pdf -re java
```

Which produces `output_file.pdf`, with a cover page, syntax highlighted code listings and a table of contents shown by the PDF reader:

<p align="center">
    <img width=720px src="images/non_compact_demo.png">
</p>

## Options

```
$ pric -h

Print multiple source code files to a single PDF file.

pric <file> (-e <ext>[,<ext>...] | -f <regex>[:<regex>...]) [OPTIONS]

Parameters:
      file                Filename of the PDF, must end in '.pdf'.

Options:
  -a, --author=<author>   Author of the document.
  -c, --compact           Produce a PDF with less pages.
  -e, --extensions=<ext>[,<ext>...]
                          Extensions of the files to be printed.
  -f, --files=<regex>[:<regex>...]
                          Match filenames by regex.
  -h, --help              Show this help message and exit.
  -k, --keep-asciidoc     Preserve AsciiDoc file after PDF generation.
  -p, --paths=<path>[?<path>...]
                          Absolute or relative paths to directories to search
                            for files (default is current directory)
  -r, --recursive         Recurse sub-directories.
  -s, --silent            Do not show log messages.
  -t, --title=<title>     Title of the document. If omitted, filename is used.
  -V, --version           Print version information and exit.

Exit codes:
  0    Successful PDF generation.
  1    No PDF was generated.

Examples:
Print to out.pdf all Java and XML files on the current dir and its sub-dirs.
pric out.pdf -re java,xml

Print to out.pdf all Markdown files and the LICENSE file found on the current
directory.
pric out.pdf -f 'LICENSE:.*[.]md'
```

- By default, the PDF generated has one file per page. If you are dealing with many small files, this might not be ideal. The `--compact` option generates a PDF with no cover page, no ToC, and attempts to place more files per page.
- If you would like to further customize the PDF, for example by adding a paragraph or some other information, you can use `--keep-asciidoc` to preserve the AsciiDoc file and manually edit it as you will. Then it is simple to generate your PDF by using [`asciidoctor-pdf`](https://github.com/asciidoctor/asciidoctor-pdf#install-the-published-gem).

## Requirements

- Groovy 3
- Java 8

## Installation

### Linux

Download **[Pric](./pric)** and provide execution permission:

```
chmod +x pric
```

To have the script globally available, copy it to `/usr/local/bin`.

### Windows

1. Make sure you have a shell which supports Bash, e.g. [Git Bash](https://gitforwindows.org/).
2. Download **[Pric](./pric)** and you are done.
3. (Optional but recommended) Make the script globally available by configuring your `PATH` environment variable.
