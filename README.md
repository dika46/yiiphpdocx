yii-PHPDOCX
===========

Fork
----
This is modified community version of phpdocx, you can download community version from here http://www.phpdocx.com/download
When I init this repo, the current version was 3.0 (as per March 1, 2014)

Integrating with YII Framework
------------------------------
Assumse that you have php5, apache2.2.x and all requirements that phpdocx needed.
YII Version 1.1.14 (I am using 1.1.15-dev straight clone from github)

+ Clone or extract this repo to:

        /protected/vendors/phpdocx
        
+ The structure of directory should be

        /protected/vendors/phpdocx/classes etc...
        
+ Add this line to: /protected/config/main.php

        'import' => array(
		....
		'application.vendors.phpdocx.classes.*', 
		'application.vendors.phpdocx.lib.log4php.*',
		'application.vendors.phpdocx.lib.log4php.appenders.*',
		'application.vendors.phpdocx.lib.log4php.configurators.*',
		'application.vendors.phpdocx.lib.log4php.filters.*',
		'application.vendors.phpdocx.lib.log4php.helpers.*',
		'application.vendors.phpdocx.lib.log4php.layouts.*',
		'application.vendors.phpdocx.lib.log4php.pattern.*',
		'application.vendors.phpdocx.lib.log4php.renderers.*',
		... 
		);

        
+ Create simple code to generate docx


        public function actionDocx1() {  
	        spl_autoload_unregister(array('YiiBase', 'autoload'));
	        Yii::import('application.vendors.phpdocx.*'); 
	        Yii::$enableIncludePath = false;
	        
	        require_once('lib/log4php/Logger.php');  
	        require_once('classes/CreateDocx.php');
	
		// the filename will be saved in
		// public_html/contents/documents 
		// make sure this directory has writeable permission by webserver.
	        $filename_target = YiiBase::getPathOfAlias('webroot') . '/contents/documents/' . 'isiaja1';
	
	        $docx = new CreateDocx();
	        $text = 'Ini sekedar tulisan.'; 
	
	        $docx->addText($text);
	        $docx->createDocx($filename_target);
	        spl_autoload_register(array('YiiBase', 'autoload'));
	        }


Notes
-----
+ From this thread (http://www.phpdocx.com/forums/issues/how-integrate-phpdocx-yii-framework), phpdocx having an issue with Yii AutoLoad, so spl_autoload_unregister at first is the solution for this issue.
+ Also, adding "Yii:$enableIncludePath = false;" is required (see here for more info: http://www.yiiframework.com/doc/api/1.1/YiiBase#enableIncludePath-detail).
+ The documents named 'isiaja1.docx' will be available at /public_html/contents/documents or depends on your configuration.
+ pdf components is NOT included.

Credits
-------
+ Original by 2mdc.com (awesome works)
+ Modified by @dika46 - @agungsijawir

License
-------
GNU GPL v3
