# Stripes Framework

* [Introduction](#introduction)
* [Modules](#modules)
* [Usage](#usage)
* [Migrating](#migrating)


## Introduction

Stripes framework is a collection of supporting modules for building a FOLIO user interface.  Stripes wraps underlying `stripes-*` modules, defining dependencies on versions known to work well together.  This takes the burden off app developers for selecting potentially incompatible versions of the underlying modules.


## Modules

The modules included within Stripes are:
* [stripes-components](https://github.com/folio-org/stripes-components) -- A component library for Stripes
* [stripes-connect](https://github.com/folio-org/stripes-connect) -- Manages the connection of UI components to back-end modules
* [stripes-core](https://github.com/folio-org/stripes-core) -- The core of Stripes, an opinionated and modular platform for React components consuming REST data and the UI framework for the FOLIO project
* [stripes-form](https://github.com/folio-org/stripes-form) -- A redux-form wrapper for Stripes
* [stripes-logger](https://github.com/folio-org/stripes-logger) -- Simple category-based logging for Stripes
* [stripes-smart-components](https://github.com/folio-org/stripes-smart-components) -- A suite of smart components. Each communicates with an Okapi web-service in order to provide the facilities that it renders
* [stripes-util](https://github.com/folio-org/stripes-util) -- A library of utility functions to support Stripes modules


## Usage

Include `stripes`, as well as `react`, both as peerDependencies and devDependencies in your app's package.json. The peerDependency ensures the same version of `stripes` is shared across all apps when your app is included in a FOLIO [platform](https://github.com/folio-org/stripes-sample-platform).  The devDependency enables your app to be built and run stand-alone with a version of `stripes` for development and testing.
```
  "devDependencies": {
    "@folio/stripes": "^1.0.0",
    "@folio/stripes-cli": "^1.5.0",
    "react": "^16.4.1",
  },
  "peerDependencies": {
    "@folio/stripes": "^1.0.0"
    "react": "*"
  }
```

Import your `stripes-*` dependencies, such as `stripes-components`, through the exports provided by `stripes`:
```
import {
  Select,
  TextField,
  Row,
  Col,
  Accordion,
  Headline
} from '@folio/stripes/components';
import { AddressEditList } from '@folio/stripes/smart-components';
```

Note: Beginning with version 1.6, [stripes-cli](https://github.com/folio-org/stripes-cli) generates new apps using `stripes` framework.


## Migrating

To migrate existing apps developed prior to the introduction of stripes framework, begin by adding `stripes` to your package.json as noted [above](#usage).

Next, review all `@folio/stripes-*` imports replacing hyphens as necessary:
```
- import { Button } from '@folio/stripes-components';
+ import { Button } from '@folio/stripes/components';
```

Take care to remove any path-based imports you may have in the process:
```
- import Button from '@folio/stripes-components/lib/Button';
+ import { Button } from '@folio/stripes/components';
```

Review the [stripes-components 4.x changelog](https://github.com/folio-org/stripes-components/blob/master/CHANGELOG.md#400-2018-10-02) for any breaking changes and moved components.  Update affected imports to reflect their new component locations.

Finally remove all individual `stripes-*` dependencies from your app's package.json.  Re-run your app to verify everything is working properly.
