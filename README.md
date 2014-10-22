nQuery-CSV-Importer
===================

This is a (very basic) Tcl based object oriented CSV cypher script generator for neo4j.

After much frustration learning to write cypher scripts for the purposes of importing CSV files into neo4j, this library was written to quickly define import properties and have a cypher script generated (and optionally executed) to import data from a CSV file into neo4j.

The current implementaiton is BASIC - it has a few nice tricks built into it, but fundamentally, it is intended for first time creation / imports of CSV data into neo4j.  Other capabilties will be added in the future (e.g. updating and relationship creation).

# Why TCL?!

- easy to learn
- easy to use
- typeless scripting
- object oriented
- it works
- it is standard install on OSX and Linux
- it is what I know the best.. :)

# Minimum Requirements
- neo4j 2.1.4 (or later)
- Tcl 8.5 - Typically Installed on OSX and Linux
- Windows Users --> [Download ActiveState - Community Version](http://www.activestate.com/activetcl/downloads)

## Required Packages
- snit

## Required Tools
- Text Editor
- your csv file(s)

# Getting Started
A Tcl Script is nothing more than a text file.  So any text editor will work, but it is recommended that you use something with syntax highlighting and code checking (e.g. Komodo is a good choice from ActiveState, or download hint files for your favorite editor if they are available).

## Global Definitions
Start by defining your neo4j installation directory as a global variable:

`set ::neo4j_dir "<path>/neo4j-community-2.1.5"`

## Load Package(s) and Source Required Files
```Tcl
package require snit
source nQuery_importDataMapObj.tcl
```

## Simple Import Example
```Tcl
set ::dataDir "<path>/data"

puts "processing: Drink Size"
csvMapObj sizeObj
sizeObj configure -datadir       $::dataDir
sizeObj configure -srcfile       PEACH_HOT.csv
sizeObj configure -delimeter     ","
sizeObj configure -outfile       temp_Size.cql
sizeObj configure -outdir        cypher
sizeObj configure -nodelabel     size
sizeObj configure -unique        name

sizeObj addMap Size name

sizeObj writeCreateNodesCypherFile
sizeObj executeCypherFile
puts "DONE!"
exit
```




