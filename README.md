# Useful functions PHP (at least for me)
List of all functions for PHP.

```php
/**
* Route: Get URI Segment
* @author Ricardo (sawir.ricardo@gmail.com)
* @param int $int_pos default 0
* @return string
*/
function route_get_uri(int $int_pos=0):string {
    $arr_uri = explode("/", parse_url(ltrim($_SERVER['REQUEST_URI'], '/'), PHP_URL_PATH));
    if (array_key_exists($int_pos, $arr_uri)) {
        return "/" . $arr_uri[$int_pos];
    }
    return "/404";
}
```

Token for CSRF in PHP
https://stackoverflow.com/a/31683058/9478774
```php
/**
* Initialize token
* @link https://stackoverflow.com/a/31683058/9478774
* @return void
*/
function token_init():void
{
if (empty($_SESSION['token'])) {
    $_SESSION['token'] = bin2hex(random_bytes(32));
}
}
```

```php
/**
* Get Token CSRF
* @link https://stackoverflow.com/a/31683058/9478774
* @param string $str_form_name
* @return string
*/
function token_get_csrf(string $str_form_name="form"):string
{
return hash_hmac('sha256', $str_form_name, $_SESSION['token']);
}
```

```php
/**
* Validate token CSRF
* @link https://stackoverflow.com/a/31683058/9478774
* @param string $str_form_name
* @param string $str_token
* @return bool
*/
function token_validate_csrf(string $str_token,string $str_form_name="form"):bool
{
return hash_equals(token_get_csrf($str_form_name),$str_token);
}
```

Route get query params
```php
/**
* Route Get Query Params
* @return array
*/
function route_get_query_params(): array
{
    $arr_res = [];
    parse_str(parse_url($_SERVER['REQUEST_URI'], PHP_URL_QUERY), $arr_res);
    return $arr_res;
}
```
