# wordpress-engineering
A Guide and Collection of notes in general targeting ECMAScript Developers
So Wordpress Plugins can be seen as express like Midelware. they get called with request parameters.


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
- https://blog.kulturbanause.de/2020/01/wordpress-block-editor-gutenberg-fuer-custom-post-types-aktivieren/
- https://developer.wordpress.org/reference/functions/wp_insert_post/

## How to Extend Wordpress
You should almost always write at last a plugin or use a plugin framework like @stealify/wordpress
then you should use the hooks to define your behavior. and at last create programatical posts with 
custom post types to store data and retrive it later via wp-query loops inside your plugin. To layout that 
data you should use gutenberg blocks parsed by your plugin again that inserts the data.

This little example should get you up and running when you need to do admin or user permission based stuff.
```php
function hf_Function(){
    $user_ID = get_current_user_id(); 

    if ($user_ID == 0) {
        // The user ID is 0, therefore the current user is not logged in
        return; // escape this function, without making any changes
    }
    // Run your cache requests here or wp loops anything
    // Run your SQL queries here (using WordPress DB class)
    global $wpdb;
    // $wpdb->query($sql);
}
add_action('init', 'hf_Function');
```


## Security
You should regular match your access logs for security problems and ban ips.
