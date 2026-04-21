# Largest Contentful Paint solutions

## Beaver Builder
Visit Beaver builder's [hooks site](https://hooks.wpbeaverbuilder.com/) to verify the hooks.


### Adding fetchpriority and loading=eager to Photo Module of beaver builder
You need to add `critical` css class to the module first.

``` functions.php
/**
 * Use the module content filter to perform a safe string replacement
 */
add_filter( 'fl_builder_render_module_content', function( $content, $module ) {
    
    // 1. Check if the 'critical' class is assigned to this module
    if ( isset( $module->settings->class ) && strpos( $module->settings->class, 'critical' ) !== false ) {
        
        // 2. Add fetchpriority="high"
        // We inject it right after the opening <img tag
        $content = str_replace( '<img ', '<img fetchpriority="high" ', $content );

        // 3. Remove or swap Lazy Loading
        // PageSpeed Insights hates lazy loading on critical images. 
        // We swap 'lazy' for 'eager'.
        if ( strpos( $content, 'loading="lazy"' ) !== false ) {
            $content = str_replace( 'loading="lazy"', 'loading="eager"', $content );
        } else {
            // If no loading attribute exists, add eager explicitly
            $content = str_replace( '<img ', '<img loading="eager" ', $content );
        }
    }

    return $content;
}, 10, 2 );
```