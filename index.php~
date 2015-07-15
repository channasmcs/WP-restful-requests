<?php
/**
 * @package Hello_Dolly
 * @version 1.6
 */
/*
Plugin Name: WP-restful-requests
Plugin URI: http://wordpress.org/plugins/WP-JSON/
Description: This is simple plugin to List Post as JSON .you can get all post & pages get by post id ,post type,post category, post status.sending a post request with json data that contains a list.ontentType to 'application/json' and use the JSON
Author:  channa senevirathna bandara
Version: 1.0
Author URI: http://channasmcs.blogspot.com/

*/
/*

GET all post
http://SITE_NAME/?wp-api=all
=================================================

GET all post related by post type
http://SITE_NAME/?wp-api/post_type=post_type

EX :
http://SITE_NAME/?wp-api/post_type=page

=================================================

GET all post related by post status
http://SITE_NAME/?wp-api/post_type=post_status

EX :
http://SITE_NAME/?wp-api/post_status=auto-draft

=================================================

GET all post related by  post id
http://SITE_NAME/?wp-api/post_type=post_id

EX :
http://SITE_NAME/?wp-api/post_id=12

=================================================

GET all post related by  category id
http://SITE_NAME/?wp-api/category_id=category_id

EX :
http://SITE_NAME/?wp-api/category_id=3

=================================================

all data send as JSON format
 *
 */

function restful_requests_activate()
    {
        restful_requests_rules();
        flush_rewrite_rules();
    }

function restful_requests_deactivate()
    {
        flush_rewrite_rules();
    }


function restful_requests_rules()
    {
 //    add_rewrite_rule('products/?([^/]*)', 'index.php?pagename=products&product_id=$matches[1]', 'top');
//      json all post
        add_rewrite_rule( 'WP-api/?', 'index.php?wp-api=all', 'top' );

 //    jSOn url for post
        add_rewrite_rule( 'WP-api/?', 'index.php?wp-api/post_type=null', 'top' );
        add_rewrite_rule( 'WP-api/?', 'index.php?wp-api/post_status=null', 'top' );
        add_rewrite_rule( 'WP-api/?', 'index.php?wp-api/post_id=null', 'top' );

//      category
        add_rewrite_rule( 'WP-api/?', 'index.php?wp-api/category_id=null', 'top' );

//      page
        add_rewrite_rule( 'WP-api/?', 'index.php?wp-api/page=all', 'top' );
// post comment
        add_rewrite_rule( 'WP-api/?', 'index.php?wp-api/post_comment=null', 'top' );

// post author
    add_rewrite_rule( 'WP-api/?', 'index.php?wp-api/author_id=null', 'top' );

    }

function restful_requests_query_vars($restful_vars)
    {

    $restful_vars[] = 'wp-api';
    $restful_vars[] = 'wp-api/post_id';
    $restful_vars[] = 'wp-api/post_type';
    $restful_vars[] = 'wp-api/post_status';
    $restful_vars[] = 'wp-api/category_id';
    $restful_vars[] = 'wp-api/page';
    $restful_vars[] = 'wp-api/post_comment';
    $restful_vars[] = 'wp-api/author_id';
        return $restful_vars;
 }


function action_parse_request( &$wp ) {


    $output = array();
    foreach( $wp->query_vars as $key=> $post )
    {    // Pluck the id and title attributes
        $output[] = $post;
    }


    if ($wp->query_vars['wp-api']=='all') //get post detail
    {

        echo _sendResponse(200,null,'all',null,null,'application/json');

    }

    elseif($key=='wp-api/post_id') //get post id detail

    {

        $id =$wp->query_vars['wp-api/post_id'];

        if(!empty($id))
        {
            echo _sendResponse(200,null,'post_id',null,$id,'application/json');
        }
        else
        {
            echo _getStatusCodeMessage(404);
        }

    }
    elseif($key=='wp-api/post_type')//get type detail

    {
        $id =$wp->query_vars['wp-api/post_type'];

        echo($id);

        if(!empty($id))
        {
            echo _sendResponse(200,null,'post_type',null,$id,'application/json');
        }
        else
        {
//            echo _sendResponse(404,sprintf('Mode <b>create</b> is not implemented for model <b>%s</b>'));
            echo sprintf('Mode <b>create</b> is not implemented for model <b>%s</b>');
        };

    }
    elseif($key=='wp-api/post_status') //get status detail

        {
            $id =$wp->query_vars['wp-api/post_status'];
    //                    echo($id);
            echo _sendResponse(200,null,'post_status',null,$id,'application/json');

        }
    elseif($key=='wp-api/category_id') //get category  detail

        {
            $id =$wp->query_vars['wp-api/category_id'];

            echo _sendResponse(200,null,'category_id',null,$id,'application/json');

        }
    elseif($key=='wp-api/page') //get page  detail

        {
//            exit;
            $id =$wp->query_vars['wp-api/page'];

            echo _sendResponse(200,null,'page',null,$id,'application/json');

        }
    elseif($key=='wp-api/post_comment') //get comment related with post id

        {
//            exit;
            $id =$wp->query_vars['wp-api/post_comment'];

            echo _sendResponse(200,null,'post_comment',null,$id,'application/json');

        }
    elseif($key=='wp-api/author_id') //get post  related with author id

        {
//            exit;
            $id =$wp->query_vars['wp-api/author_id'];

            echo _sendResponse(200,null,'author_id',null,$id,'application/json');

        }




//    exit;
}

function _sendResponse($status = '', $body = '',$page='',$type='',$id='', $content_type = 'text/html')
{
    global $query_string;
    global $wpdb;
    $starttime = microtime();
    $startarray = explode(" ", $starttime);
    $starttime = $startarray[1] + $startarray[0];
    $endtime = microtime();
    $endarray = explode(" ", $endtime);
    $endtime = $endarray[1] + $endarray[0];
    $totaltime = $endtime - $starttime;

    if($totaltime > 30)
        {
            echo _getStatusCodeMessage(504) .' This page loaded in '.$totaltime.' seconds ';
        }
    else
        {


            if($page=='all') // get all post
            {

                $sql='SELECT * FROM '.$wpdb->prefix.'posts WHERE post_type LIKE "post"  ORDER BY "ID" DESC ';
                $posts = $wpdb->get_results($sql);

                if(!empty($posts)) // get all post
                {
//                               data available
                    if( !empty( $posts ) )
                    {
                        $output = array();
                        foreach( $posts as $post ) {    // Pluck the id and title attributes
                            $output[] = $post;
                        }
                        echo json_encode( $output );
                    }
                    else
                    {
                        echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                    }
                }
                else
                {
                    //  data empty
                    echo _getStatusCodeMessage(404),' Mode '.$page.' = is not implemented for wordpress  <b>%s</b>' ;
                }


            }

            elseif($page=='post_id') // get all post by id
            {
                $sql='SELECT * FROM '.$wpdb->prefix.'posts WHERE ID = "'.$id.'"  ORDER BY "ID" DESC ';
                $posts = $wpdb->get_results($sql);

                if(!empty($posts))
                {

                    echo json_encode( $posts );
                }
                else
                {
                    //  data empty
                    echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                }
//                echo _getStatusCodeMessage(404);
            }

            elseif($page=='post_type') // get all post by type
            {

                $sql='SELECT * FROM '.$wpdb->prefix.'posts WHERE  post_type LIKE "'.$id.'" AND  post_status LIKE "publish"  ORDER BY "ID" DESC ';
                $posts = $wpdb->get_results($sql);




                if(!empty($posts))
                {

                    if( !empty( $posts ) )
                    {
                        $output = array();
                        foreach( $posts as $post ) {    // Pluck the id and title attributes
                            $output[] = $post;
                        }
                        echo json_encode( $output );
                    }
                    else
                    {
                        echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                    }
                }
                else
                {
                    //  data empty

                    echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;

                }

            }
            elseif($page=='post_status') // get all post status  by type
            {
                $sql='SELECT * FROM '.$wpdb->prefix.'posts WHERE  post_status LIKE "'.$id.'" AND  post_type LIKE "post"  ORDER BY "ID" DESC ';
                $posts = $wpdb->get_results($sql);


                if(!empty($posts))
                {

                    if( !empty( $posts ) )
                    {
                        $output = array();
                        foreach( $posts as $post ) {    // Pluck the id and title attributes
                            $output[] = $post;
                        }
                        echo json_encode( $output );
                    }
                    else
                    {
                        echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                    }
                }
                else
                {
                    //  data empty
                    echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                }

            }
            elseif($page=='category_id') // get all category base post  by type
            {

                $args = array(
                    'cat'         => $id,
                    'post_type'  => 'post',
                );
                $query = new WP_Query( $args ); // $query is the WP_Query Object
                $posts = $query->get_posts();   // $posts contains the post objects

//           echo'<pre>'.print_r($posts,1).'</pre>';
                ;
//        exit;

                if(!empty($posts))
                {

                    if( !empty( $posts ) )
                    {
                        $output = array();
                        foreach( $posts as $post ) {    // Pluck the id and title attributes
                            $output[] = $post;
                        }
                        echo json_encode( $output );
                    }
                    else
                    {
                        echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                    }
                }
                else
                {
                    //  data empty
                    echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                }

            }
            elseif($page=='page') // get all category base post  by type
            {

                if($id =='all')
                {
                    $sql='SELECT * FROM '.$wpdb->prefix.'posts WHERE   post_type LIKE "page"  ORDER BY "ID" DESC ';
                    $posts = $wpdb->get_results($sql);

                    if( !empty( $posts ) )
                    {
                        $output = array();
                        foreach( $posts as $post ) {    // Pluck the id and title attributes
                            $output[] = $post;
                        }
                        echo json_encode( $output );
                    }
                    else
                    {
                        echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                    }

                }
                else
                {

                    $sql='SELECT * FROM '.$wpdb->prefix.'posts WHERE ID="'.$id.'"  AND post_type LIKE "page"  ORDER BY "ID" DESC ';
                    $posts = $wpdb->get_results($sql);

                    if( !empty( $posts ) )
                    {
                        $output = array();
                        foreach( $posts as $post ) {    // Pluck the id and title attributes
                            $output[] = $post;
                        }
                        echo json_encode( $output );
                    }
                    else
                    {
                        echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                    }

                }



            }
            elseif($page=='post_comment') // get all comment  base post  id
            {

                $sql='SELECT p.* FROM  '.$wpdb->prefix.'comments c JOIN '.$wpdb->prefix.'posts p ON c.comment_post_ID =p.ID WHERE p.ID="'.$id.'" ';
                $posts = $wpdb->get_results($sql);
                if( !empty( $posts ) )
                {
                    $output = array();
                    foreach( $posts as $post ) {    // Pluck the id and title attributes
                        $output[] = $post;
                    }
                    echo json_encode( $output );
                }
                else
                {
                    echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                }


            }
           elseif($page=='author_id') // get all comment  base post  id
            {

                echo('hello');
                $sql='SELECT * FROM '.$wpdb->prefix.'posts WHERE post_author="'.$id.'"  AND post_type LIKE "page"  ORDER BY "ID" DESC ';  $posts = $wpdb->get_results($sql);
                if( !empty( $posts ) )
                {
                    $output = array();
                    foreach( $posts as $post ) {    // Pluck the id and title attributes
                        $output[] = $post;
                    }
                    echo json_encode( $output );
                }
                else
                {
                    echo _getStatusCodeMessage(404),' Mode '.$page.' = <b>'.$id.'</b> is not implemented for wordpress  <b>%s</b>' ;
                }


            }



        }




    exit;
}


function _getStatusCodeMessage($status)
{
    // these could be stored in a .ini file and loaded
    // via parse_ini_file()... however, this will suffice
    // for an example
    $codes = Array(
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
    );
    return (isset($codes[$status])) ? $codes[$status] : '';

}
//register activation function
register_activation_hook(__FILE__, 'restful_requests_activate');
//register deactivation function
register_deactivation_hook(__FILE__, 'restful_requests_deactivate');
//add rewrite rules in case another plugin flushes rules
add_action('init', 'restful_requests_rules');
//add plugin query vars  to wordpress
add_filter('query_vars', 'restful_requests_query_vars');
//register plugin custom pages display
add_filter('template_redirect', 'restful_requests_display');
add_action( 'parse_request', 'action_parse_request');







?>
