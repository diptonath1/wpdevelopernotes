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

#### Basic *functions.php* wp_enqueue_script code

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

#### Loading image files during theme bootstrapping

```markdown

<img src="<?php echo get_template_directory_uri();?>/assets/images/thumbs/masonry/gallery/gallery-1-400.jpg" alt="">

```

- ***<?php wp_head(); ?>*** loads all style sheets and script on the heads
- ***<?php wp_footer(); ?>*** loads all style sheets and script on the footer


### Menu

[Register nav menu](https://developer.wordpress.org/reference/functions/register_nav_menus/) using this code with your desired name and id on the ***function.php*** file **after_setup_theme** hook

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

**Creating [*Pagination*](https://developer.wordpress.org/themes/functionality/pagination/) using function same as html design**

At first, we need to create a function. Then replace the Wordpress default pagination design class with your HTML markup design class

***Pagination function code***

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


You can use the [editor on GitHub](https://github.com/diptonath/wpdevelopernotes/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3
function activate_sitewide_plugin() {
    _deprecated_function( __FUNCTION__, '3.0.0', 'activate_plugin()' );
    return false; 
}
- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/diptonath/wpdevelopernotes/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration files.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.

### Dipto Nath

I am Dipto Nath 

### Code

Function is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown

function activate_sitewide_plugin() {
    _deprecated_function( __FUNCTION__, '3.0.0', 'activate_plugin()' );
    return false; 
}

```




