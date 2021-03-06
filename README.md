# ISO Harmonized North American Profile (HNAP) plugin for GeoNetwork

The Canadian GeoNetwork community is pleased share the *ISO Harmonized North American Profile (HNAP)* schema plugin. This is a bilingual extension of the *North American Profile of ISO 19115:2003 - Geographic information - Metadata* used nationally.

For details on this release see [3.6.0 Milestone](https://github.com/metadata101/iso19139.ca.HNAP/milestone/3?closed=1) release notes for details.

## Installation

### GeoNetwork version to use with this plugin

Use GeoNetwork `3.10.x`, not tested with prior versions!

The schema plugin editor makes use of a number of controls for editing structured text fields requiring newer releases of core-geonetwork.

### Deploy the profile in an existing installation

The plugin can be deployed manually in an existing GeoNetwork installation:

1. Download from [releases](https://github.com/metadata101/iso19139.ca.HNAP/releases) page.
   
   There are two files for each release, a `jar` and a `zip`.

2. Extract contents of the `schema-iso19139.ca.HNAP` zip download into `WEB-INF/data/config/schema_plugins/iso19139.ca.HNAP`.

3. Copy the `schema-iso19139.ca.HNAP` jar to geonetwork `WEB-INF/libs`

4. Restart geonetwork

There is some custom initialization code run when GeoNetwork starts up:

1. The plugin includes will check the GeoNetwork Data Directory `ThesauriDir` to see if the HNAP Thesauruses are already installed.

2. If they are not (i.e. this is the very first run of GeoNetwork with the HNAP Schema), the required thesaurus files are are copied from the `jar` into to the correct location in the Data Directory.

  See `SchemaInitializer.java` for details.

## Building

### Adding the plugin to the source code

The best approach is to add the plugin as a submodule:

1. Use [add-schema.sh](https://github.com/geonetwork/core-geonetwork/blob/3.10.x/add-schema.sh] for automatic deployment:

   ```
   ./add-schema.sh iso19139.ca.HNAP https://github.com/metadata101/iso19139.ca.HNAP 3.10.x
   ```

2. Build the application:
   
   ```
   mvn clean install -Penv-prod -DskipTests
   ```
   
3. Once the application is built, the war file contains the schema plugin:

   ```
   cd web
   mvn jetty:run -Penv-dev
   ```

### Deploy locally built profile into existing installation

1. Copy the `iso19139.ca.HNAP` folder from `schemas/iso19139.ca.HNAP/src/main/plugin` into geonetwork `WEB-INF/data/config/schema_plugins/`.

2. Copy `schema-iso19139.ca.HNAP` jar from `target` into geonetwork `WEB-INF/libs`.

3. Restart geonetwork
