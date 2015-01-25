# Robo Drush Extension

Extension to execute Drush commands in [Robo](https://github.com/Codegyre/Robo).

[![Build Status](https://travis-ci.org/boedah/robo-drush.svg?branch=master)](https://travis-ci.org/boedah/robo-drush) [![Latest Stable Version](https://poser.pugx.org/boedah/robo-drush/v/stable.png)](https://packagist.org/packages/boedah/robo-drush) [![Total Downloads](https://poser.pugx.org/boedah/robo-drush/downloads.png)](https://packagist.org/packages/boedah/robo-drush) [![Latest Unstable Version](https://poser.pugx.org/boedah/robo-drush/v/unstable.png)](https://packagist.org/packages/boedah/robo-drush) [![License](https://poser.pugx.org/boedah/robo-drush/license.png)](https://packagist.org/packages/boedah/robo-drush)

Runs Drush commands in stack. You can define global options for all commands (like Drupal root and uri).

The option -y is always set, as it makes sense in a task runner.

## Table of contents
- [Installation](#installation)
- [Usage](#usage)
- [Examples](#examples)

## Installation

Add `"boedah/robo-drush": "~1.0"` to your composer.json:

```json
    {
        "require-dev": {
            "boedah/robo-drush": "~1.0"
        }
    }
```

Execute `composer update`.

## Usage

Use the `Drush` trait in your RoboFile:

```php
class RoboFile extends \Robo\Tasks
{
    use \Boedah\Robo\Task\Drush;

    //...
}
```

## Examples

### Site update

This executes pending database updates and reverts all features (from code to database):

```php
$this->taskDrushStack()
    ->drupalRootDirectory('/var/www/html/some-site')
    ->uri('sub.example.com')
    ->maintenanceOn()
    ->updateDb()
    ->revertAllFeatures()
    ->maintenanceOff()
    ->run();
```

### Site install

```php
$this->taskDrushStack()
  ->siteName('Site Name')
  ->siteMail('site-mail@example.com')
  ->locale('de')
  ->accountMail('mail@example.com')
  ->accountName('admin')
  ->accountPass('pw')
  ->dbPrefix('drupal_')
  ->sqliteDbUrl('sites/default/.ht.sqlite')
  ->disableUpdateStatusModule()
  ->siteInstall('minimal')
  ->run();
```
