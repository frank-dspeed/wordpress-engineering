# wordpress-engineering
A Guide and Collection of notes


## Great Pages that i need to adapt and Condense a bit

- https://jonchristopher.us/blog/handlebars-wordpress-template-parts/
- https://developer.wordpress.org/reference/functions/get_template_part/
- https://developer.wordpress.org/themes/template-files-section/custom-post-type-template-files/
- https://awhitepixel.com/blog/wordpress-gutenberg-access-parse-blocks-with-php/
- https://wordpress.stackexchange.com/questions/255804/how-can-i-load-a-page-template-from-a-plugin
- https://www.ibenic.com/include-or-override-wordpress-templates/
```php
 define( 'MY_PLUGIN_DIR', plugin_dir_path( __FILE __ ) );
define( 'MY_PLUGIN_TEMPLATE_DIR', MY_PLUGIN_DIR . '/templates/' );

add_filter( 'template_include', 'ibenic_include_from_plugin', 99 );

function ibenic_include_from_plugin( $template ) {

    $new_template = '';

    $provided_template_array = explode( '/', $template );

    // This will give us archive.php
    $new_template = end( $provided_template_array );

    // Define single and archive template for custom post type 'portfolio'
    if( is_singular('portfolio') ) {
        $new_template = 'single-portfolio.php';
    }

    if( is_post_type_archive( 'portfolio' ) ) {
        $new_template = 'archive-portfolio.php';
    }

    $plugin_template = MY_PLUGIN_TEMPLATE_DIR . $new_template;

    if( file_exists( $plugin_template ) ) {
    return $plugin_template;
    }

    return $template;
}
 ```
- https://wordpress.stackexchange.com/questions/13378/add-custom-template-page-programmatically
- https://jasonyingling.me/use-page-custom-post-type-archive-url-rewrites/
