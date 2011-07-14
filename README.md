# Menu Library

The Menu library is used to create hierchical html structures ideal for menu structures. It is adapted from the [menu class](http://www.getfuelcms.com/user_guide/libraries/menu) found in [FUEL CMS](http://www.getfuelcms.com/) but redistributed here according to [the license](http://www.apache.org/licenses/LICENSE-2.0).

## Documentation

This library is capable of outputting standard collapsable menus with helper classes for drop-down or vertical navigation, as well as breadcrumbs and page titles. More complete documentation can be found [in the FUEL CMS user guide](http://www.getfuelcms.com/user_guide/libraries/menu), but here is a brief overview.

### Usage

To create a menu, you must populate an array with the menu items. Then you can output structured HTML suitable for standard navigation by calling the render method. Here's an example:

	$this->load->spark('menu/0.0.1');
	$nav = array();
	$nav['about'] = 'About';
	$nav['about/history'] = array('label' => 'History', 'parent_id' => 'about');
	$nav['about/contact'] = array('label' => 'Contact', 'parent_id' => 'about');
	 
	$nav['products'] = 'Products';
	$nav['products/X3000'] = array('label' => 'X3000', 'parent_id' => 'products');
	 
	$active = 'about/history';
	$menu = $this->menu->render($nav, $active, NULL, 'basic');
	 
	echo $menu;
	/* echoed output looks something like this
	<ul>
		<li class="first active"><a href="/about" title="About">About</a>
			<ul>
				<li class="first"><a href="/about/history" title="History">History</a></li>
				<li class="last active"><a href="/about/contact" title="Contact">Contact</a></li>
			</ul>
		</li>
		<li class="last"><a href="/products" title="Products">Products</a></li>
	</ul>
	*/


### The Menu Array Structure

The menu array can hav the following key/value pairs:

* id - the id value of the menu item. If none is specified, then the array key value will be used
* parent_id - the parent's id value that the menu item should reside under. Top level (also called root items), should have a root value of NULL or 0 depending on what is specified for the root_value
* label - the text label to display for the menu item
* location - the link location of the menu item. If none is specified, the array key value will be used
* attributes - additional HTML link attributes (e.g. target="_blank") to assign to the menu item
* hidden - whether to display the menu item or not.
* active - a regular expression that determines whether it should be given active status. If none is specified, it will be the same as the location value (e.g. about/history$|about/contact$). You can also use the :children active magic selector, which will highlight a menu item if it or any of it's sub pages are active. For example, if you have a news page, it allows you to easily highlight the news in the menu for all URI locations of news and news/:children (translates to news$|news/.+ in regular expression).


## Credits
- Original developer: David McReynolds @ Daylight Studio
- Repackaged by: Barnabas Kendall (barnabas@bkendall.biz)