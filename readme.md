# WordPress Plugin Check

Check if a WordPress plugin is compatible with the current environment. If not, it will automatically deactivate the plugin and show a message to the user letting them know what they can do about it.

__Note:__ Only supports checking PHP 5.2+.

## Installation

```bash
composer require wp-forge/wp-plugin-check
```

## Usage

This is how the code should be used:

```php
<?php

// Plugin headers go here...

require dirname( __FILE__ ) . '/vendor/autoload.php';

// Check plugin requirements
global $pagenow;
if ( 'plugins.php' === $pagenow ) {
	$plugin_check = new WP_Forge_Plugin_Check( __FILE__ );

	$plugin_check->min_php_version    = '5.6';
	$plugin_check->min_wp_version     = '5.0';
	$plugin_check->req_php_extensions = array( 'json', 'SimpleXML' );
	
	$plugin_check->check_plugin_requirements();
}

require dirname( __FILE__ ) . '/includes/bootstrap.php';
```

Alter the WordPress version, PHP version, and required PHP extensions as needed.

__Important:__ _Don't load any other code in your main plugin file!_ PHP parses all code in a file before running it, so incompatible PHP code added after this check will negate the ability to properly perform compatibility checks. 

