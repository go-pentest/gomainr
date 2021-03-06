# Gomainr


Terminal cli app that checks the availability of domains for different configurations of keywords.

![Demo](https://raw.githubusercontent.com/MichaelThessel/gomainr/master/assets/demo.gif)

## Installation

You need to have [Go](https://golang.org/) installed.

```
# go get github.com/MichaelThessel/gomainr
# gomainr
```

## Usage

The main purpose of this tool is to find available domains for different keywords. I.e.:

* Keywords 1: foo bar
* Keywords 2: alice bob
* TLDs: com net

Will search for:

* fooalice.com
* fooalice.net
* baralice.com
* baralice.net
* foobob.com
* foobob.net
* barbob.com
* barbob.net

and return the available domain names.

Keywords 2 is optional, so you can just search for various domains among different TLDs.

You can save a session to a file and load it later again. This way you can view the results again without performing a new search. In addition this allows you to modify the keywords and repeat a search without typing the keywords all over again.

**TLD Substitution**

You can enable TLD substitution which will check if the end of your domain could be replaced by a TLD. I.e.:

fishnet - fish.net

## Keyboard Shortcuts

Shortcut | Action
---------|-------
<kbd>CTRL</kbd>+<kbd>q</kbd> | Quit
<kbd>CTRL</kbd>+<kbd>/</kbd> | Search
<kbd>UP</kbd>, <kbd>DOWN</kbd>, <kbd>TAB</kbd> | Navigate
<kbd>CTRL</kbd>+<kbd>j</kbd> | Scroll result list down
<kbd>CTRL</kbd>+<kbd>k</kbd> | Scroll result list up
<kbd>CTRL</kbd>+<kbd>r</kbd> | Toggle TLD substitution
<kbd>CTRL</kbd>+<kbd>s</kbd> | Save session
<kbd>CTRL</kbd>+<kbd>l</kbd> | Load session

## API Keys

By default gomainr will use DNS to query for available domains. This will be sufficient in most cases. Sometimes DNS servers can be configured incorrectly and this will result in incorrect results. To get more precise results gomainr supports both the [NameCheap.com](https://www.namecheap.com/support/api/intro.aspx) and [GoDaddy.com](https://developer.godaddy.com/) APIs. To do API based searches you need to obtain an API key from either service and add your credentials to the gomainr config file (make sure to disable the DNS source).

```
# $HOME/.gomainr/config
```

To be allowed to use the NameCheap API you need to fulfill certain [conditions](https://www.namecheap.com/support/knowledgebase/article.aspx/9739/63/api--faq#c). It will also take up to 48 hours for NameCheap to activate your API access (if you ask nicely in the live chat they might do it right away though :). There are no restrictions for access to the GoDaddy API. Unless you already have a bunch of domains with NameCheap it's probably easiest to get a GoDaddy key.

**Notes**

To speed up consecutive searches and to keep things light on the APIs gomainr caches API request results for 24hrs. If you want to flush the cache for some reason you can delete the contents of this directory:

```
# $HOME/.gomainr/data
```

## Thanks

This project utilizes the following 3rd party packages

* [GOCUI](https://github.com/jroimartin/gocui)
* [TOML](https://github.com/BurntSushi/toml)
* [dnsr](https://github.com/domainr/dnsr)
* [diskv](https://github.com/peterbourgon/diskv)
* [go-namecheap](https://github.com/billputer/go-namecheap)
