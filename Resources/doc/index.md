# APY DataGrid Bundle

APYDataGridBundle is a Symfony bundle for create grids for list your Entity (ORM), Document (ODM) and Vector (Array) sources. [APYDataGridBundle](https://github.com/APY/APYDataGridBundle) was initiated by **Stanislav Turza (Sorien)** and inspired by **Zfdatagrid and Magento Grid**.

> IMPORTANT NOTICE : this is a fork repository of [APYDataGridBundle](https://github.com/APY/APYDataGridBundle). But the current version of [APYDataGridBundle](https://github.com/APY/APYDataGridBundle) is not compatible with Symfony 3+ framework. So, I fork this repository for make a APYDataGrid bundle compatible with Symfony3+. If you want to use it for Symfony2, please use the original repository [APYDataGridBundle](https://github.com/APY/APYDataGridBundle).

> IMPORTANT NOTICE: This bundle is still under development. Any changes will be done without prior notice to consumers of this package. Of course this code will become stable at a certain point, but for now, use at your own risk.

> You can see [CHANGELOG](CHANGELOG.md) and [UPGRADE 2.0](UPGRADE-2.0.md).

## Prerequisites

This version of the bundle requires Symfony 3.0+.

### Translations

If you wish to use default texts provided in this bundle, you have to make sure you have translator enabled in your config.

```yaml
# app/config/config.yml
framework:
    translator: ~
```

For more information about translations, check [Symfony documentation](https://symfony.com/doc/current/book/translation.html).

## Installation

### Step 1 : Download APYDataGridBundle using composer

For this forked version of APYDataGridBundle, update your project's composer.json file like the following :

```json
{
	"require": {
        "artscorestudio/APYDataGridBundle": "dev-master"
	},
	"repositories" : [{
        "type": "package",
        "package": {
            "name": "artscorestudio/APYDataGridBundle",
            "version": "dev-master",
            "dist" : {
				"url" : "https://github.com/artscorestudio/APYDataGridBundle/archive/master.zip",
				"type" : "zip"
			},
			"source" : {
				"url" : "https://github.com/artscorestudio/APYDataGridBundle.git",
				"type" : "git",
				"reference" : "dev-master"
			},
			"autoload": {
			    "psr-4": { "APY\\DataGridBundle\\": "" }
			}
        }
    }]
}
```

And run composer update command :

```bash
$ composer update
```

Composer will install the bundle to your project's *vendor/artscorestudio/APYDataGridBundle* directory.

### Step 2 : Enable the bundle

Enable the bundle in the kernel :

```php
// app/AppKernel.php

public function registerBundles()
{
	$bundles = array(
		// ...
		new APY\DataGridBundle\APYDataGridBundle(),
		// ...
	);
}
```

### Step 3 : Quick start with APYDataGridBundle

#### Create simple grid with an ORM source in your controller

```php
<?php
namespace MyProject\MyBundle\Controller;

use APY\DataGridBundle\Grid\Source\Entity;

class DefaultController extends Controller
{
	public function myGridAction()
	{
		// Creates a simple grid based on your entity (ORM)
		$source = new Entity('MyProjectMyBundle:MyEntity');
		
		// Get a Grid instance
		$grid = $this->get('grid');
		
		// Attach the source to the grid
		$grid->setSource($source);
		
		// Return the response of the grid to the template
		return $grid->getGridResponse('MyProjectMyBundle:myGrid.html.twig');
	}
}
```

#### Create simple configuration of the grid in the entity

```php
<?php
namespace MyProject\MyBundle\Entity

use Doctrine\ORM\Mapping as ORM;
use APY\DataGridBundle\Grid\Mapping as GRID;

/**
 * @GRID\Source(columns="id, my_datetime")
 */
class MyEntity
{
    /*
     * @ORM\Column(type="integer")
     */
    protected $id;

    /*
     * @ORM\Column(type="datetime")
     */
    protected $my_datetime;
}
```

#### Display the grid in a Twig template

```twig
<!-- MyProject\MyBundle\Resources\views\myGrid.html.twig -->
{{ grid(grid) }}
```

> Don't forget to clean your cache !

### Next Steps

Now you have completed the basic installation and configuration of the APYDataGridBundle, you are ready to learn about more advanced features and usages of the bundle.

The following documents are available :

* [Getting Started With APYDataGridBundle](getting_started.md)
* [Setting the Grid Source](source/index.md)
* [Setting the Grid template](template/index.md)
* [Columns Configuration with Annotations](columns_configuration/index.md)
* [Grid Configuration with PHP](grid_configuration)
* [Export](export/index.md)
* [APYDataGridBundle Configuration Reference](configuration.md)