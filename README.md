# Kirby – Bouncer

Restrict access of a user role to a specific page (and its children) in the panel.

![bouncer-screenshot](https://user-images.githubusercontent.com/14079751/76368370-4c6ccc00-6330-11ea-92d3-9ac560cf037e.jpg)

<br/>

## Overview

> This plugin is completely free and published under the MIT license. However, if you are using it in a commercial project and want to help me keep up with maintenance, please consider [making a donation of your choice](https://www.paypal.me/sylvainjule) or purchasing your license(s) through [my affiliate link](https://a.paddle.com/v2/click/1129/36369?link=1170).

- [1. Installation](#1-installation)
- [2. Setup](#2-setup)
- [3. Disclaimer](#3-disclaimer)
- [4. License](#4-disclaimer)

<br/>

## 1. Installation

Download and copy this repository to ```/site/plugins/bouncer```

Alternatively, you can install it with composer: ```composer require sylvainjule/bouncer```

<br/>

## 2. Setup

The intent of this plugin is to limit a user's ability to edit only their Account page + a page (and its children) selected in a *Pages field*.

- First, create a new user role (for example, `/site/blueprints/users/test.yml`)
- Set their permissions, and add a `pages` field:

```yaml
title: Test

permissions:
  access:
    panel: true
    site: true
    settings: false
    users: false
  # ...
  user:
    changeRole: false
    delete: false
    update: false # else a user will be able to edit the page they have access to on their profile

fields:
  canaccess:
    label: 'The user will only be able to access:'
    type: pages
    multiple: false
    options: query
    query: site.pages # or any query that suits your needs
```

- In your `site/config/config.php`, tell the plugin which `role => fieldname` associations to use:

```php
return [
    'sylvainjule.bouncer.list' => [
        'test' => 'canaccess'
    ]
];
```

<br/>

## 3. Disclaimer

- I needed this functionnality for a website and turned it into a plugin. I hope it can prove helpful, but do not intend to extend it or support more refined restriction scenarios with this plugin.
- The plugin uses Vue router's `beforeResolve` guard, currently not used by the panel (Kirby 3.3.5). This may change in the future, please look for any change in that direction before updating your websites, and please let me know if you spot an interfering update.

<br/>

## 4. License

MIT