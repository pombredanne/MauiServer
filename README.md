# Maui Server: A topic indexing server based on Maui

This is work in progress on Maui Server, an HTTP wrapper around the [Maui Topic Indexer](https://github.com/zelandiya/maui).

Maui Server provides a topic indexing service. It automatically determines the main topics of a text, with candidate topics coming from a [SKOS](http://www.w3.org/2004/02/skos/) vocabulary. It requires training data--documents with previously assigned topics--to work. Maui Server is a Java web application an provides RESTful, JSON-based APIs.

## Status

This is pre-release work in progress.

## Configuring the data directory

Maui Server needs a **data directory** on the file system where it keeps its data. This directory is established in the following way:

1. If the Java **system property** `MauiServer.dataDir` is set, use its value. (This can be set on the Java command line via `-DMauiServer.dataDir=...`)
2. Otherwise, if the OS **environment variable** `MAUI_SERVER_DATA_DIR` is set, use its value. (How to set this depends on the operating system.)
3. Otherwise, use a subdirectory `data` in the **current directory**, from where Maui Server was started.

The directory must already exist, otherwise initialisation will fail.

## Building and Running

The project uses Maven for building.

- `mvn package` creates a war file in the `/target` directory, for deployment with a servlet container such as Tomcat or Jetty.
- `mvn jetty:run` runs Maui Server directly, using Jetty. The server will start up at http://localhost:8080/ . This can be convenient for testing.

The API root is at `/`. A small demo app is at `/app/` (requires tagger creation and training through the API).

## Configuring the default language

By default, Maui Server assumes that vocabulary and content are in English. The global language can be set using the Java **system property** `MauiServer.defaultLang`, or the OS **environment variable** `MAUI_SERVER_DEFAULT_LANG`. Supported values are `en`, (English), `fr` (French), `es` (Spanish) and `de` (German). The default language can be overridden on a per-tagger basis using the `lang` key in the configuration.

## License

This project is licensed under the terms of the [GNU GPL v3](http://www.gnu.org/licenses/gpl.html).
