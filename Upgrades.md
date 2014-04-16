
## Upgrades
  
Prestashop supports modules upgrading. This article doesn't
concern with the AddOn site or automatically fetching the
new version form a remote source but instead focuses on the
core parts of a module needed to support upgrading.

## Version

Before you do anything relating to upgrading with your module
you should give it a version in your constructor:

```
    $this->version = "1.2.3";
```

Prestashop uses the `version_compare()` function in PHP and
is capable of handling at least version strings like `1.2` or
`1.2.3` so you are free to use *semantic versioning*. What is
important is you keep with numbers that adhere to the way
version_compare() works (see http://php.net/version_compare )

## Upgrade Scripts

Prestashop keeps track of the last time it installed or upgraded
your module, and when it sees a newer version it checks your
module for files that are named like this:

```
upgrades/abc-2.0.php
upgrades/database-1.2.php
upgrades/zztop-1.1.php
```

The first part (abc, database, zztop) is not terribly important,
but the second part is used in the `version_compare()` and is
important. Upgrade scripts are ran in the order based on their
version.

## Install and Upgrade Scripts

It's important to think about how people will use your module and
if they will uninstall it or install it again. When a module is installed,
even if an older version was installed sometime in the past, it will
call the normal `install()` method of your plugin and not run any
upgrade scripts. This is because it's simply installing the newest
reason without any upgrades.


## Always do something on upgrade

Writing an upgrade script for every version to do the same thing is
really lame. Luckily, Prestashop has a method on the `Module` class
called `runUpgradeModule()` that is invoked every time the module
is upgraded. Make sure to remember to return true if upgrading
went okay, or false if something bad happened:

```
public function runUpgradeModule() {
    if (!parent::runUpgradeModule()) {
        return false;
    }
    
    // Do something upon every upgrade
    return true;
}
```


