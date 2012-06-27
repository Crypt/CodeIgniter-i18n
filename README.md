CodeIgniter-i18n
================

####Internationalization (i18n) for CodeIgniter 2.1+

Based on http://codeigniter.com/wiki/CodeIgniter_2.1_internationalization_i18n/

##HMVC modular extension

By default is using HMVC modular extension.

If you want use without HMVC:

- In `core/MY_Lang.php` delete:

	`require APPPATH . "libraries/MX/Lang.php";`

	`class MY_Lang extends MX_Lang {`

and uncomment:

	//class MY_Lang extends CI_Lang {

- In `core/My_Config.php` delete:

	`require_once APPPATH . "libraries/MX/Config.php";`

	`class MY_Config extends MX_Config {`

and uncomment:

	//class MY_Config extends CI_Config {

##Route

Add these lines to `application/config/routes.php`:

	// URI like '/en/about' -> use controller 'about'
	$route['^(en|de|fr|nl)/(.+)$'] = "$2";

	// '/en', '/de', '/fr' and '/nl' URIs -> use default controller
	$route['^(en|de|fr|nl)$'] = $route['default_controller']; 

##Creating languages files

You can add placeholders inside your strings. For instance, if you like to add the "username" to a string, you can by writing this lang string:

	$lang['welcome'] = "Welcome, %s."; 

##Create Controller

	<?php
	class About extends CI_Controller {
 
		function index()
		{
			// you might want to just autoload these two helpers
			$this->load->helper('language');
			$this->load->helper('url');
 
			// load language file
			$this->lang->load('about');
 
			$this->load->view('about');
		}
	}
 
	/* End of file about.php */
	/* Location: ./application/controllers/about.php */ 

##Create View

To fetch a lang line or add an anchor:

	<p><?=lang('about.gender')?></p>

	<p><?=anchor('music','Shania Twain')?></p> 

In case you use placeholders inside your language strings, you can use them like this:

	<p><?php $username = "John Doe";
	echo lang('welcome', NULL, $username)?></p>

This should appear like:

	Welcome, John Doe.

Get the current language:

	<?php echo get_lang();?>

This should appear like:

	en

##Notes

- You might need to translate some of CodeIgniter’s language files in `system/language`. Example: if you’re using the "Form Validation" library for French pages, translate `system/language/english/form_validation_lang.php` to `application/language/french/form_validation_lang.php`.

- Links to internal pages are prefixed by the current language, but links to files are not:

	`site_url('about/my_work');
	// http://mywebsite.com/en/about/my_work`

	`site_url('css/styles.css');
	// http://mywebsite.com/css/styles.css`

- Get the current language:

	`$this->lang->lang();
	// en`

- Switch to another language:

	`anchor($this->lang->switch_uri('fr'),'Display current page in French');`