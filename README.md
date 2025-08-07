# SNOMED CT Database Creation and Import Tool (Swiss Edition)

This Java project creates a MySQL database and imports SNOMED CT data, including both the International Edition and the Swiss Extension (CH Edition), using the Full release format.

## Features

- Creates a MySQL database
- Creates all required tables for SNOMED CT Full release:
  - `full_concept`
  - `full_description`
  - `full_relationship`
  - `full_refset_Simple`
  - `full_refset_ExtendedMap`
  - `full_refset_Language`
  - `full_refset_ModuleDependency`
- Imports SNOMED CT International Edition Full release files
- Imports Swiss Extension Full release files (German, French, Italian, English)
- Adds indexes to improve query performance

## Requirements

- Java 8 or higher
- MySQL 8.x
- MySQL Connector/J (JDBC driver)
- SNOMED CT Full release files:
  - **International Edition**
  - **Swiss Extension**

## Configuration

### 1. Update paths and release identifiers

Open `CreateDatabaseAndImportData.java` and set the following variables to match your environment:

```java
static String ReleaseFilePath = "PATH_TO_YOUR_INTERNATIONAL_EDITION";
static String ReleaseFilePathCH = "PATH_TO_YOUR_SWISS_EXTENSION";
static String ReleaseDate = "20250101"; // International Edition release date
static String ReleaseDateCH = "CH1000195_20241207"; // Swiss Extension release identifier

### 2. Database credentials

Set your local MySQL credentials and connection parameters:
```bash
String dbUser = "root";
String dbPassword = "";
String dbURL = "jdbc:mysql://localhost/";
```

Make sure `allowLoadLocalInfile=true` and `allowMultiQueries=true` are enabled in your connection string.

### 3. File structure expected

The tool expects SNOMED CT files to follow the official Full release folder structure, e.g.:
```bash
International Edition/
└── Full/
    └── Terminology/
        ├── sct2_Concept_Full_INT_20250101.txt
        ├── sct2_Description_Full-en_INT_20250101.txt
        └── sct2_Relationship_Full_INT_20250101.txt
    └── Refset/
        └── Language/
            └── der2_cRefset_LanguageFull-en_INT_20250101.txt

Swiss Extension/
└── Full/
    └── Terminology/
        ├── sct2_Concept_Full_CH1000195_20241207.txt
        ├── sct2_Description_Full-de-ch_CH1000195_20241207.txt
        ├── sct2_Description_Full-fr-ch_CH1000195_20241207.txt
        ├── sct2_Description_Full-it-ch_CH1000195_20241207.txt
        ├── sct2_Description_Full-en_CH1000195_20241207.txt
        └── sct2_Relationship_Full_CH1000195_20241207.txt
    └── Refset/
        └── Language/
            ├── der2_cRefset_LanguageFull-de-ch_CH1000195_20241207.txt
            ├── der2_cRefset_LanguageFull-fr-ch_CH1000195_20241207.txt
            ├── der2_cRefset_LanguageFull-it-ch_CH1000195_20241207.txt
            └── der2_cRefset_LanguageFull-en_CH1000195_20241207.txt
```
Note: Some optional imports (e.g., simple refsets, extended maps) are commented out in the code and can be enabled as needed.
