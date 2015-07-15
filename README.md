# WP-restful-requests
version 1.0
Makes quickly adding a RESTFul API to your Wordpress site easy

 WP-restful-requests  provides full HTTP verb support (GET) for your resources, as well as the ability to offset, limit, sort, filter, etc… . You will also have the ability to read and manipulate related data with ease.
 
 WP-restful-requests has been lovingly rebuilt from the metal and is now 100% test covered! The new event based architecture allows for clean and unlimited customization.
 
 <b><i>How it works</i></b>
 
 1. Download and place the 'upload pluing ' directory in your wordpress site.
 2. active WP-restful-requests 
 
  So if you active  WP-restful-requests to the 'wordpress site' you will get the following new routes by default.

               1. [GET] http://SITE_NAME/?wp-api=all (returns all  post)
               
               2. [GET] http://SITE_NAME/?wp-api/post_type=post_type (returns all post related by post type 
                          EX :  http://SITE_NAME/?wp-api/post_type=page
                          
               3. [GET] http://SITE_NAME/?wp-api/post_type=post_status (returns all post related by post status)
                          EX :  http://SITE_NAME/?wp-api/post_status=auto-draft
                          
               4. [GET] http://SITE_NAME/?wp-api/post_type=post_id (return  all post related by  post id)
                          EX :  http://SITE_NAME/?wp-api/post_id=12
                          
               5. [GET] http://SITE_NAME/?wp-api/category_id=category_id (return  all post related by  category id)
                          EX :  http://SITE_NAME/?wp-api/category_id=3 
                          
 all data send as JSON format
