# node-red-flow-startpage #

Node-RED flow to run an internet search using Startpage.com and parse its findings

![Startpage Flow Screenshot](./Startpage-Flow.png)

This repository contains a simple flow which runs an internet search using [Startpage.com](https://www.startpage.com/) and parses its results.

> Just a small note: if you like this work and plan to use it, consider "starring" this repository (you will find the "Star" button on the top right of this page), so that I know which of my repositories to take most care of.

## Installation ##

This flow relies on [Axios](https://axios-http.com/) for the communication with Startpage.com.

Simply import the contents of file [Startpage-Flow.json](./Startpage-Flow.json) into your Node-RED Flow Editor and Axios will be installed as well (if necessary)

Since the flow is implemented as a "reusable flow", the [corresponding nodes](https://github.com/rozek/node-red-contrib-reusable-flows) should be installed as well - afterwards, Startpage searches may be used anywhere in any workspcae of your Node-RED server without having to copy the node which implements this function (this simplifies any updates)

## Usage ##

The Startpage flow expects up to two parameters:

* `msg.payload` - initially contains the string to search for. Later on, it will be replaced either by an error message or the parsed search results
* `msg.language` - the language Startpage should use for the search

If successfull (success is indicated by `msg.status === 200`), `msg.payload` will return an array with up to 10 search results. Each result is an object with the following properties:

* `Date` - an optional date indicating when the found document was modifed
* `URL` - the URL of the found document
* `Title` - the title of the found document
* `Description` - a short description of the found document

If `msg.status` has a different value as 200 or 204, `msg.payload` contains an error message describing the error that occurred

### Example ###

File [Startpage-Example.json](./Startpage-Example.json) contains a simple example: just import its contents into your Node-RED flow editor and configure the injection node with the desired search text and language.

![Startpage Example Screenshot](./Startpage-Example.png)

Shortly after pressing the injection button, the debug output should show up to 10 properly parsed search results.

## License ##

[MIT License](LICENSE.md)
