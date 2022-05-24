### Wordpress Developer Notes

### Theme Bootstrapping

#### Basic Template Files

- index.php
- style.css
- functions.php
- page.php
- single.php
- archive.php
- search.php
- searchform.php
- 404.php
- header.php
- footer.php
- sidebar.php

#### Basic *style.css* code

```markdown

/*
Theme Name: 
Theme URI: 
Author: Dipto Nath
Author URI:  https://diptonath.com
Description: 
Version: 1.0
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: 
*/

```

#### Basic *functions.php* after_setup_theme code

```markdown

function textdomain_theme_setup(){
    load_theme_textdomain("philosophy");
    add_theme_support("title-tags");
    add_theme_support( 'post-thumbnails' );
    add_theme_support( 'html5', array(
        'search-form', 'comment-form', 'comment-list', 'gallery', 'caption'
    ) );
    add_theme_support( 'post-formats', array(
        'image', 'video', 'quote', 'link', 'gallery', 'audio'
    ) );
    add_editor_style('/assets/css/editor-style.css');
}
add_action("after_setup_theme", "textdomain_theme_setup");

```

#### Basic `functions.php` wp_enqueue_script code

```markdown

function textdomain_theme_enqueue_scripts(){
    // Enqueue my styles.
    wp_enqueue_style('main-css', get_template_directory_uri().'/assets/css/main.css',null,'1.0');
    wp_enqueue_style( 'philosophy-css', get_stylesheet_uri() );
     
    // Enqueue my scripts.
    wp_enqueue_script('modernizr-js', get_template_directory_uri().'/assets/js/modernizr.js',null,'1.0'); 
    // If dependent on jquery
    wp_enqueue_script('main-js', get_template_directory_uri().'/assets/js/main.js',array("jquery"),'1.0',true);  
}
add_action( 'wp_enqueue_scripts', 'textdomain_theme_enqueue_scripts' );

```

- ***<?php wp_head(); ?>*** loads all style sheets and script on the heads
- ***<?php wp_footer(); ?>*** loads all style sheets and script on the footer

Loading image files during theme bootstrapping

```markdown

<img src="<?php echo get_template_directory_uri();?>/assets/images/thumbs/masonry/gallery/gallery-1-400.jpg" alt="">

```

Template file call

```markdown

<?php get_template_part("template-parts/common/navigation");?>

```

### Menu

[Register nav menu](https://developer.wordpress.org/reference/functions/register_nav_menus/) using this code with your desired name and id on the `function.php` file **after_setup_theme** hook

```markdown

register_nav_menus( array(
'menu_id' => __('Menu Name','textdomain'),
) );

```

Displays a [navigation menu](https://developer.wordpress.org/reference/functions/wp_nav_menu/)

```markdown

wp_nav_menu( array(
    'theme_location' => 'menu_id',
    'menu_id'        => 'menu_id',
    'menu_class'     => 'header__nav'
) );

```

You can check [this 6 number answer](https://stackoverflow.com/questions/26180688/how-to-add-class-to-link-in-wp-nav-menu) for adding **li class** and **a class**
Also, You can check [this 5 number answer](https://stackoverflow.com/questions/26180688/how-to-add-class-to-link-in-wp-nav-menu) for adding **active class**

### All About Post  

Display Posts [loop](https://developer.wordpress.org/themes/basics/the-loop/)

```markdown

<?php
    while(have_posts()){
        the_post();
            // Display post content
    }
?>

```

### Pagination

Creating [*Pagination*](https://developer.wordpress.org/themes/functionality/pagination/) using function same as html design

At first, we need to create a function. Then replace the Wordpress default pagination design class with your HTML markup design class

Pagination function code

```markdown

function the_textdomain_pagination(){
    global $wp_query;
    $links = paginate_links(array(
        'current' => max(1,get_query_var('paged')),
        'total'   => $wp_query->max_num_pages,
        'type'    => 'list',
        'mid_size'=> 3
    ));
    //Replacing Design
    $links  = str_replace("page-numbers","pgn__num",$links);
    echo $links;
}

```

Display function on the pagination page

```markdown

<?php the_textdomain_pagination();?>

```

### Comments

### Page Templates

[Pages templates](https://developer.wordpress.org/themes/template-files-section/page-template-files/) comment Code

```markdown

<?php /* Template Name: Example Template */ ?>

```

### Widgets Registered

For example, used with registering sidebars:

```markdown

function mytheme_widgets_init() {
    register_sidebar( array(
        'name'          => __( 'Single Post Widgets', 'textdomain' ),
        'id'            => 'mytheme-single-post-widgets',
        'description'   => __( 'Widgets in this area will be shown under your single posts, before comments.', 'textdomain' ),
        'before_widget' => '',
        'after_widget'  => '',
        'before_title'  => '',
        'after_title'   => '',
    ) );
}
add_action( 'widgets_init', 'mytheme_widgets_init' );

```

Display sidebars

```markdown

<?php
  if(is_active_sidebar("mytheme-single-post-widgets")){
    dynamic_sidebar("mytheme-single-post-widgets");
  }
?>

```
