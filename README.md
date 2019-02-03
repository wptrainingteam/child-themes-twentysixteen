# Child Themes Twentysixteen

## Description

In this lesson you will learn what a child theme is and when should you use one. The step-by-step walkthrough will give you an understanding of what a child theme is and how to create your own child theme.

## Objectives

At the end of this lesson, you will be able to:

*   Explain what a child theme is.
*   Summarize why you should use child themes.
*   Create a child theme including the directory (in the correction location) and file(s) required.
*   Replace "Proudly Powered by WordPress" with a copyright statement.
*   Create a new template file that is only in the child theme.

## Prerequisite Skills

You will be better equipped to work through this lesson if you have experience in and familiarity with:

*   Basic knowledge of HTML/[CSS](https://make.wordpress.org/training/handbook/theme-school/intro-to-css/)
*   Basic knowledge of [installing and activating WordPress themes](https://make.wordpress.org/training/handbook/user-lessons/choosing-and-installing-a-theme/)
*   Understanding of how folders and files are structured
*   Ability to edit files with a text editor

## Assets

*   [Twenty Sixteen theme](https://wordpress.org/themes/twentysixteen/ "Twenty Sixteen Theme")
*   [Sample screenshot png file](http://make.wordpress.org/training/files/2013/10/screenshot.png)

## Screening Questions

*   Are you familiar with installing and activating themes via the WordPress Dashboard?
*   Do you have at least a basic knowledge of HTML/CSS?
*   Do you feel comfortable using a text editor to edit code?
*   Will you have a locally or remotely hosted sandbox WordPress site to use during class?

## Teacher Notes

*   **Time Estimate:** 45 minutes
*   Performing a live demo while teaching the steps to make a child theme is crucial to having the material "click" for students.
*   It is easiest for students to work on a locally installed copy of WordPress. Set some time aside before class to assist students with installing WordPress locally if they need it. For more information on how to install WordPress locally, please visit our [Teacher Resources page](http://make.wordpress.org/training/teacher-resources/).
*   The preferred answers to the screening questions is "yes." Participants who reply "no" to all 4 questions may not be ready for this lesson.
*   Built using WordPress 4.7.3.

## Hands-on Walkthrough

### Introduction: What is a Child Theme

Welcome to child themes! Today, you are going to learn how to make a child theme for WordPress. One of the first things people want to do is modify the design of an existing WordPress theme. After a little investigation, they discover where the theme files live, then directly edit the files. After the next theme update, they are horrified to discover that the update completely erased all of their modifications. Many people have learned this lesson the hard way. How do you prevent this from happening? By using a child theme! A child theme is a theme that overrides and adds elements to another theme (the "parent" theme) without touching any of the parent theme's code. When the parent theme is updated, your changes in the child theme will be preserved.

* * *

### Why Use a Child Theme?

The #1 Rule of WordPress development is to **never directly modify WordPress files**. **This means do not edit:**

*   WordPress core files
*   Plugin files
*   Theme files

Exception: starter themes that have been intentionally created by theme builders for you to modify. **Why?**

*   *   **Updates wipe out customization changes**

If you update a modified theme, the update will overwrite all customizations. Similarly, when you update a plugin, the update will overwrite any edits you've made. Same for WordPress core files.

*   *   **Themes can get broken**

If you edit theme files directly and make a mistake that cannot be undone, you are stuck with a broken theme.

*   *   **WordPress and WordPress plugins may not work with theme hacks**

You may inadvertently remove elements that WordPress and WordPress plugins look for in a theme, so they no longer work. **So how do you safely customize a WordPress theme?** Create a **child theme** that is a "**child**" of another theme (the "parent theme").

*   The child theme overrides selected design elements and otherwise falls back to the parent.
*   The child theme can also override or add functionality to the parent theme.

* * *

### How Child Themes Work

A child theme loads first, before the parent, and only contains overrides and additions to the parent theme. [![file-flow-diagram-02](http://make.wordpress.org/training/files/2013/10/file-flow-diagram-02-1024x248.png)](http://make.wordpress.org/training/files/2013/10/file-flow-diagram-02.png)   All of your CSS, templates, images, and other files are kept in the child theme's folder while the original parent theme's files are left intact. If something breaks, you can simply delete or fix the offending file in the child theme folder.

* * *

### Creating a Child Theme

You are going to create a child theme of the default WordPress theme [Twenty Sixteen](https://wordpress.org/themes/twentysixteen/ "Twenty Sixteen Theme"). We'll name this child theme "**MyChildTheme**". A child theme only needs a few things to get up and running: a theme folder, a CSS file, and a screenshot file.

#### Step 1: A Theme Folder

Every theme for WordPress needs its own folder. Take a look at the folder structure of WordPress. You can see each installed theme's folder in `/wp-content/themes` [![](https://make.wordpress.org/training/files/2016/11/childthemes-file-path-1024x663.png)](https://make.wordpress.org/training/files/2016/11/childthemes-file-path.png) Create a folder for your child theme. The folder name should be all lowercase with no spaces. In our example the child theme's folder is called "**mychildtheme**." [![](https://make.wordpress.org/training/files/2016/11/childthemes-file-path-new-folder-1024x663.png)](https://make.wordpress.org/training/files/2016/11/childthemes-file-path-new-folder.png)

#### Step 2: A style.css File

At a minimum, your child theme needs a `style.css` file. The `style.css` file tells WordPress to load the parent theme's files after the child. Place this file inside the child theme's folder. Make sure it is in the root level of the theme folder and not inside a subfolder. The `style.css` file needs the following code at the top:

<pre> /*
 Theme Name: [Your Theme Name]
 Description: The custom theme [Your Theme Name] using the parent theme Twenty Sixteen.
 Author: [You]
 Author URI: [Your URL]
 Template: twentysixteen
 Version: 1
 */
</pre>

There are other variables you can include, but these are the most important ones you should include to identify your child theme. Here is an explanation of the different variables in `style.css`:

*   **Theme Name:** The name of the theme. This is the name that shows up in the WordPress Dashboard under Appearance > Themes.
*   **Description:** A short description for the theme. You can put anything you like here. This shows up in the WordPress Dashboard under Appearance > Themes once the theme is activated.
*   **Author:** The author of the child theme, which can be a person's name or company name.
*   **Author URI:** The URL for the author of the child theme.
*   **Template: Very important!** This is **the folder name of the parent theme**. If this variable is not correct the child theme will not work.
*   **Version:** The version of the child theme

All of these variables are optional, with the exception of `**Template:**`. If this line is not present or contains typos the child theme will not work.

### Step 3: Enqueue Parent and Child Theme Style Sheets

Your child theme needs to call the `style.css` files using a method called "enqueueing scripts." That just means that the files need to be lined up in the correct order and WordPress will help you do that. To add the calls for the parent and child theme stylesheets to your child theme, first you need to create a `functions.php` file. Place this file inside the child theme's folder. Make sure it is in the root level of the theme folder and not inside a subfolder. [tip]Note that functions.php in the child theme does not replace functions.php in the parent theme. This is where you can put hooks, actions, and filters that modify or add functionality to the parent theme, rather than replacing it.[/tip] The first line of your child theme's functions.php will be an opening PHP tag (`<?php`), after which you can enqueue your parent and child theme stylesheets. The correct method of enqueuing the parent theme stylesheet is to add a `wp_enqueue_scripts` action and use `wp_enqueue_style()` in your child theme's functions.php. The following example function will only work if your parent theme uses only one main `style.css` to hold all of the css. If your theme has more than one .css file (eg. `ie.css`, `style.css`, `main.css`) then you will have to make sure to maintain all of the parent theme dependencies.

<pre>add_action( 'wp_enqueue_scripts', 'mychildtheme_enqueue_styles' );
    function mychildtheme_enqueue_styles() {
       wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css' );
}
</pre>

This line needs to point to the parent theme’s `style.css` file. Your child theme's `style.css` file can be empty. But if it contains CSS code, as it usually will, you will need to enqueue it as well. Setting 'parent-style' as a dependency will ensure that the child theme stylesheet loads after it.

<pre>function awesome_enqueue_styles() {

    $parent_style = 'parent-style';

    wp_enqueue_style( $parent_style, get_template_directory_uri() . '/style.css' );
    wp_enqueue_style( 'child-style',
        get_stylesheet_directory_uri() . '/style.css',
        array( $parent_style )
    );
}
add_action( 'wp_enqueue_scripts', 'awesome_enqueue_styles' );
</pre>

This is the recommended way to enque the styles for your child theme. [warning]The old way of working with scripts and styles was to use @import url("../parentfolder/style.css");, and you'll still see old articles online that show that technique. But this is very inefficient, so a better way is to use the wp_enqueue_style() method covered here.[/warning]

### Step 4: A screenshot.png File

A theme's screenshot is the thumbnail image that shows up under Appearance > Themes in the WordPress Dashboard. A screenshot image is not required for a child theme, but it will look sad without one.   [![](https://make.wordpress.org/training/files/2016/11/twenty-sixteen-active-300x251.png)](https://make.wordpress.org/training/files/2016/11/twenty-sixteen-active.png) The recommended image size is 880x660\. The screenshot will only be shown as 387x290, but the larger image allows for high-resolution viewing on HiDPI displays. Create a 880px by 660px image file, name it "screenshot.png", and place it into the child theme's folder. If you don't have an image editor, download a [sample screenshot.png file](http://make.wordpress.org/training/files/2013/10/screenshot.png).

* * *

### Activate the Child Theme

You now have everything you need to use a child theme! Make sure the child theme folder containing at least `style.css` is uploaded or pushed to `/wp-content/themes` on the web server, or your computer if you are working on a local WordPress install. After you add the theme folder to `/wp-content/themes`, go to Appearance > Themes in the Dashboard. You should see your theme listed.   [![](https://make.wordpress.org/training/files/2016/11/my-child-theme-activate-1024x412.png)](https://make.wordpress.org/training/files/2016/11/my-child-theme-activate.png) Hover over your theme to reveal the "Activate" button. Click to activate your theme. Once activated, the site will not look any different on the front-end, but the child theme will be the theme in charge. You can now see your theme labeled as "active". [![](https://make.wordpress.org/training/files/2016/11/my-child-theme-active-300x242.png)](https://make.wordpress.org/training/files/2016/11/my-child-theme-active.png)  

* * *

### Child Theme Files

The files in the example child theme illustrate how a child theme's files affect the parent's files: they either override elements and add functionality to its identically named file, or completely replaces it.   [![](https://make.wordpress.org/training/files/2016/11/childtheme-lesson-file-flowA-1024x285.png)](https://make.wordpress.org/training/files/2016/11/childtheme-lesson-file-flowA.png) `style.css` in MyChildTheme overrides elements and adds to `style.css` in Twenty Sixteen, while `screenshot.png` completely replaces the copy of `screenshot.png` in Twenty Sixteen.

* * *

### Overriding the Parent Theme's CSS

The child theme's `style.css` file will override any styles in the parent theme's `style.css` file that have the same selectors. Let's say you wanted to change the size of the site title in the header. Inspecting that element reveals the CSS selector `.site-title` shows that the parent theme sets the font size at 1.75rem.   [![](https://make.wordpress.org/training/files/2016/11/twenty-sixteen-inspector-1024x443.png)](https://make.wordpress.org/training/files/2016/11/twenty-sixteen-inspector.png) In the Child Theme's `style.css` file, add the selector and the font-size you want to change the site title to:

<pre> .site-title {
    font-size: 4.75rem;
    line-height: 1.25;
}
</pre>

Now the site title is 4.75rem instead of 1.75rem. [![](https://make.wordpress.org/training/files/2016/11/childtheme-larger-site-title-1024x205.png)](https://make.wordpress.org/training/files/2016/11/childtheme-larger-site-title.png)  

* * *

### Overriding the Parent Theme's Templates

[Templates](http://codex.wordpress.org/Templates) are the files that control how your WordPress site will be displayed on the Web. Inside the `twentysixteen` folder are all of Twenty Thirteen's template files. You can create your own versions of these files in your child theme. [![](https://make.wordpress.org/training/files/2016/11/twenty-sixteen-files-1024x542.png)](https://make.wordpress.org/training/files/2016/11/twenty-sixteen-files.png) Let's say you want to replace the text "Proudly powered by WordPress" in the footer with a copyright. Here's how it looks now:   [![](https://make.wordpress.org/training/files/2016/11/twenty-sixteen-default-footer-1024x262.png)](https://make.wordpress.org/training/files/2016/11/twenty-sixteen-default-footer.png) Open `footer.php` in the `twentysixteen` folder. You can see the code that needs to be edited:

```PHP
<div class="site-info">
	<?php do_action( 'twentythirteen_credits' ); ?>
	<a href="<?php echo esc_url( __( 'http://wordpress.org/', 'twentythirteen' ) ); ?>" 
        title="<?php esc_attr_e( 'Semantic Personal Publishing Platform', 'twentythirteen' ); ?>"
        ><?php printf( __( 'Proudly powered by %s', 'twentythirteen' ), 'WordPress' ); ?></a>
 </div><!-- .site-info -->

```

Save a copy of `footer.php` into the child theme folder. Edits can safely be made to the child theme file, leaving the original copy of `footer.php` in `wp-content/themes/twentysixteen` intact. Just like our other child theme files, `wp-content/themes/mychildtheme/footer.php` will override the parent copy. To display a copyright line, replace the content above in `footer.php` in `wp-content/themes/mychildtheme` with the following code:

```PHP
<div class="site-info">
	Copyright &copy; <?php echo date('Y'); ?>
 </div><!-- .site-info -->
```

The result on the front-end of the site: [![](https://make.wordpress.org/training/files/2016/11/mycildtheme-footer-300x97.png)](https://make.wordpress.org/training/files/2016/11/mycildtheme-footer.png)

* * *

### Adding New Templates

In addition to being able to override existing templates with a child theme, you can also create new templates. Let's say you want to add a new template without a sidebar. Make a copy of `page.php` in your child theme and rename it `page-nosidebar.php`. Edit the existing code at the top:

```PHP
<?php
 /**
  * The template for displaying all pages
  *
  * This is the template that displays all pages by default.
  * Please note that this is the WordPress construct of pages and that other
  * 'pages' on your WordPress site will use a different template.
  *
  * @package WordPress
  * @subpackage Twenty_Sixteen
  * @since Twenty Sixteen 1.0
  */

 get_header(); ?>
```

To:

```PHP
<?php
 /*
 Template Name: Page with no sidebar
 */

 get_header(); ?>
```

The name of the template goes after the variable `Template Name:`. Finally, find and remove the line of code which loads the sidebar. This is called `get_sidebar();`:

```PHP
<?php get_sidebar(); // delete this entire line ?> 
<?php get_footer(); // leave this line in! ?>
```

The new template will now appear under **Page Attributes** on the Edit Page screen: ![newtemplate3](http://make.wordpress.org/training/files/2013/10/newtemplate3.png)

* * *

### Summary

Your child theme now has one file that overrides elements in its parent theme's file, two files that replace files in the parent theme, and one brand new file that does not exist in the parent theme. [![](https://make.wordpress.org/training/files/2016/11/childtheme-lesson-file-flowB.png)](https://make.wordpress.org/training/files/2016/11/childtheme-lesson-file-flowB.png) When you update the parent theme with a new version, none of these child theme files will be modified. Child themes are a safe and powerful way to override and add elements to an existing theme. Now that you know how to make one, go forth and make some awesome looking sites!

## Exercises

**Create a child theme of Twenty Sixteen**

*   What folders and files did you need to create?
*   Did your theme show up under Appearance > Themes in the Dashboard? If not, what steps did you take to troubleshoot?

**Change all the links in your theme to red, active links to green, and visited links to orange**

*   What file did you need to edit to do accomplish this?
*   What selectors did you apply the new color styles to?
*   How did you determine the selectors to use?

**Change the "Proudly powered by WordPress" message in the site footer**

*   What file did you need to create?
*   What steps did you take to create the file and change the message?

**Make a new template for the home page with no sidebar.**

*   What file did you create?
*   What steps did you take to create the file?
*   What code did you add to make it a new template?
*   How did you remove the sidebar?
*   How did you assign the new template to the home page of your site?

## Quiz

**When developing for WordPress, what files should you never edit?**

1.  Core WordPress files
2.  Plugin files
3.  Theme files
4.  All of the above

**Answer:** 4\. All of the above

* * *

**What file _must_ you create to make a child theme, in addition to the child theme folder?**

1.  functions.php
2.  index.html
3.  style.css
4.  readme.html
5.  license.txt

**Answer:** 3\. style.css

* * *

**What items do you have to include in the style.css file of your child theme in order for it to work properly?**

1.  `Theme Name: [Name] and Template: [parentfolder]`
2.  `Theme Name: [Name] and Version: [#]`
3.  `Description: [Theme description] and wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css' );`
4.  `Template: [parentfolder] and wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css' );`
5.  `Theme Name: [Name] and wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css' );`

**Answer:** 4\. `Template: [parentfolder] and wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css' );`

* * *

**How do you get a picture of your theme to show up under Appearance > Themes in the Dashboard?**

1.  Upload screenshot.png to the child theme folder
2.  Upload screenshot.png to the the parent theme folder
3.  Upload screenshot.png to the /images folder of /wp-admin/
4.  Upload screenshot.png to the /images folder in /wp-content/

**Answer:** 1\. Upload screenshot.png to the child theme folder

## Additional Resources

[Child Themes](https://codex.wordpress.org/Child_Themes) in the WordPress Codex
