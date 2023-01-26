This repository contains the source files for generating the REPLACEME website. REPLACEME is ADD DESCRIPTION HERE. 

The REPLACEME software distribution is licensed under the REPLACEME License.

The REPLACEME website and its documentation are maintained by [Network Time Foundation](https://www.nwtime.org/) and YOURNAME.

The website and its documentation are a work in progress and rely on the contributions of many individuals. If you are interested in helping us to improve or translate the documentation, refer to the instructions in this README. 

The files in this repository are freely available for sharing and redistribution under the terms of the [Creative Commons Attribution License](https://creativecommons.org/licenses/by/4.0/). This means that you have permission to copy, distribute, translate, and adapt the work as long as you attribute [Network Time Foundation](https://www.nwtime.org/) as the original source.

## Requirements

In order to render the Markdown into HTML using Hugo (recommended), the following software needs to be installed:

* [Hugo (Extended version)](https://github.com/gohugoio/hugo/releases)
* [Node.js](https://nodejs.org/en/download/)

Add the following Node packages:

```
npm install -D autoprefixer
npm install -D postcss-cli
npm install -D postcss
```

Grab the REPLACEME repository:

```
git clone https://bitbucket.nwtime.org/scm/websites/REPLACEME.git

```

## Building

Once you've installed the requirements, start Hugo from the `REPLACEME` directory:

```
hugo server
```

This message indicates success and you can view the REPLACEME website by opening the specified URL in a web browser:

```
Web Server is available at //localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

If you instead get this error:

```
Error: Error building site: TOCSS: failed to transform "scss/main.scss" (text/x-scss): resource "scss/scss/main.scss_9fadf33d895a46083cdd64396b57ef68" not found in file cache
```

you have not installed the extended version of Hugo.

## Editing

If Hugo is running as you save edits to an REPLACEME file, it should automatically display the changes--occasionally you will need to refresh your browser to see the changes.

To issue a git pull request for your edits, use the instructions at
https://help.github.com/articles/using-pull-requests.
