# Guzaba Platform Documentation

## Overview

## Main packages

The following packages are neither GuzabaPlatform components, neither base modules used by these.
- [guzaba-platform/guzaba-platform](https://packagist.org/packages/guzaba-platform/guzaba-platform) - the [GuzabaPlatform](https://github.com/AzonMedia/guzaba-platform) itself
- [guzaba-platform/guzaba-platform-installer](https://packagist.org/packages/guzaba-platform/guzaba-platform-installer) - the [installer of GuzbaPlatform](https://github.com/AzonMedia/guzaba-platform-installer). It is always installed with GuzabaPlatform. It has its package type set to "composer-plugin"
- [guzaba-platform/guzaba-platform-docs](https://packagist.org/packages/guzaba-platform/guzaba-platform-docs) - GuzabaPlatform documentation
- [guzaba/guzaba2](https://packagist.org/packages/guzaba/guzaba2) - the [Guzaba2 Framework](https://github.com/AzonMedia/guzaba2) that powers GuzabaPlatform

## List of available components

The following GuzabaPlatform components are available as packages through [Packagist](https://packagist.org/).
The GuzabaPlatform components have their package type set to "guzaba-platform-component" in composer.json and have their GitHub repository name starting with "component".
You can use the given names with the `composer require` command. 
- [guzaba-platform/payments-integrations](https://packagist.org/packages/guzaba-platform/payments-integrations) - [Payments integrations component](https://github.com/AzonMedia/component-payments-integrations)
- [guzaba-platform/payments-integration-epaybg](https://packagist.org/packages/guzaba-platform/payments-integration-epaybg) - [Payments integration with Epay.bg component](https://github.com/AzonMedia/component-payments-integration-epaybg)
- [guzaba-platform/tags](https://packagist.org/packages/guzaba-platform/tags) - [Tags component](https://github.com/AzonMedia/component-tags)
- [guzaba-platform/catalog](https://packagist.org/packages/guzaba-platform/catalog) - [Catalog component](https://github.com/AzonMedia/component-catalog) (can be used as products catalog/store front)
- [guzaba-platform/cart](https://packagist.org/packages/guzaba-platform/cart) - [Shopping cart component](https://github.com/AzonMedia/component-cart)

## List of modules

Additiional packages that are used by GuzabaPlatform but are not GuzabaPlatform components.
These packages have their package type set to "library" repository name starting with "module".
These still can be installed individually with `composer require` but usually these will be installed as part of the components listed above.
- [guzaba-platform/cart-base](https://packagist.org/packages/guzaba-platform/cart-base) - [Shopping cart module](https://github.com/AzonMedia/module-cart-base) - contains interfaces
- [guzaba-platform/catalog-base](https://packagist.org/packages/guzaba-platform/catalog-base) - [Catalog module](https://github.com/AzonMedia/module-catalog-base) - contains interfaces
- [guzaba-platform/components-base](https://packagist.org/packages/guzaba-platform/components-base) - [Components module](https://github.com/AzonMedia/module-components-base) - interfaces needed to be implemented by every GuzabaPlatform module
- [guzaba-platform/payments-integrations-base](https://packagist.org/packages/guzaba-platform/payments-integrations-base) - [Payments Integrations module](https://github.com/AzonMedia/module-payments-integrations-base) - contains interfaces
- [guzaba-platform/tags-base](https://packagist.org/packages/guzaba-platform/tags-base) - [Tags module](https://github.com/AzonMedia/module-tags-base) - contains interfaces


## Basic Topics

- [Routing](./Routing)
- [Command Line Arguments](./cli-args)
- [Development](./Development)
