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
 
 get Status CodeMessage
 
 <pre> 
 100 => 'Continue',
            101 => 'Switching Protocols',
            200 => 'OK',
            201 => 'Created',
            202 => 'Accepted',
            203 => 'Non-Authoritative Information',
            204 => 'No Content',
            205 => 'Reset Content',
            206 => 'Partial Content',
            300 => 'Multiple Choices',
            301 => 'Moved Permanently',
            302 => 'Found',
            303 => 'See Other',
            304 => 'Not Modified',
            305 => 'Use Proxy',
            306 => '(Unused)',
            307 => 'Temporary Redirect',
            400 => 'Bad Request',
            401 => 'Unauthorized',
            402 => 'Payment Required',
            403 => 'Forbidden',
            404 => 'Not Found',
            405 => 'Method Not Allowed',
            406 => 'Not Acceptable',
            407 => 'Proxy Authentication Required',
            408 => 'Request Timeout',
            409 => 'Conflict',
            410 => 'Gone',
            411 => 'Length Required',
            412 => 'Precondition Failed',
            413 => 'Request Entity Too Large',
            414 => 'Request-URI Too Long',
            415 => 'Unsupported Media Type',
            416 => 'Requested Range Not Satisfiable',
            417 => 'Expectation Failed',
            500 => 'Internal Server Error',
            501 => 'Not Implemented',
            502 => 'Bad Gateway',
            503 => 'Service Unavailable',
            504 => 'Gateway Timeout',
            505 => 'HTTP Version Not Supported'
 </pre>
