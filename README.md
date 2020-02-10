# WP Bootstrap Navwalker

A custom WordPress Nav Walker Class to fully implement the Bootstrap 4.x navigation style in a custom theme using the WordPress built in menu manager.

## Installation

Place **wp-bootstrap-navwalker.php** in your WordPress theme folder `/wp-content/themes/your-theme/`

Open your WordPress themes **functions.php** file - `/wp-content/themes/your-theme/functions.php` - and add the following code:

```php
/**
 * Register Custom Navigation Walker
 */
function register_navwalker(){
	require_once get_template_directory() . '/wp-bootstrap-navwalker.php';
}
add_action( 'after_setup_theme', 'register_navwalker' );
```

If you encounter errors with the above code use a check like this to return clean errors to help diagnose the problem.

```php
if ( ! file_exists( get_template_directory() . '/wp-bootstrap-navwalker.php' ) ) {
    // File does not exist... return an error.
    return new WP_Error( 'wp-bootstrap-navwalker-missing', __( 'It appears the wp-bootstrap-navwalker.php file may be missing.', 'wp-bootstrap-navwalker' ) );
} else {
    // File exists... require it.
    require_once get_template_directory() . '/wp-bootstrap-navwalker.php';
}
```

## Usage

Add or update any `wp_nav_menu()` functions in your theme (often found in `header.php`) to use the new walker by adding a `'walker'` item to the wp_nav_menu args array.

```php
wp_nav_menu( array(
    'theme_location'  => 'primary',
    'depth'           => 2, // 1 = no dropdowns, 2 = with dropdowns.
    'container'       => 'div',
    'container_class' => 'navbar-collapse',
    'container_id'    => 'navbarCollapse',
    'menu_class'      => 'navbar-nav',
    'fallback_cb'     => 'WP_Bootstrap_Navwalker::fallback',
    'walker'          => new WP_Bootstrap_Navwalker(),
) );
```

#### Icons

To add an Icon to your link simply enter Font Awesome class names in the links **CSS Classes** field in the Menu UI and the walker class will do the rest. IE `fa fa-arrow-left` or `fas fa-arrow-left`.
