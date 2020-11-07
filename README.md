# useful-functions-php
List of all functions for PHP.

```php
function route_get_uri(string $int_pos):string {
    $arr_uri = explode("/", parse_url(ltrim($_SERVER['REQUEST_URI'], '/'), PHP_URL_PATH));
    if (array_key_exists($int_pos, $arr_uri)) {
        return "/" . $arr_uri[$int_pos];
    }
    return "/404";
}
```
