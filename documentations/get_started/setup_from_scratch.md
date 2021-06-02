### Information required to setup connection
- Operator access to Back-Office
- API url
- API client secret
- API client id
  
### Create API user through Back-Office

1. Connect to Back-Office as operator

<a href="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/connect_bo.png" target="_blank"><img src="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/connect_bo.png" alt="connect-bo" /></a>

2. Go to user menu

<a href="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/user_menu.png" target="_blank"><img src="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/user_menu.png" alt="user_menu" style="text-align: center"/></a>

3. Create a user

<a href="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/create_user.png" target="_blank"><img src="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/create_user.png" alt="create_user" style="text-align: center"/></a>

4. Add operator role to this user

<a href="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/user_add_operator_role.png" target="_blank"><img src="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/user_add_operator_role.png" alt="user_add_operator_role" style="text-align: center"/></a>

5. Set the user password

<a href="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/user_set_password.png" target="_blank"><img src="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/user_set_password.png" alt="user_set_password" style="text-align: center"/></a>



### Test your API user through Postman

You could test your api user through Postman by clicking <a href="https://documenter.getpostman.com/view/1769019/TVYDfffr#5009ca65-5c00-486d-8e76-6f44bd9e6af5">here</a>

<a href="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/postman_login.png" target="_blank"><img src="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/postman_login.png" alt="postman_login" style="text-align: center"/></a>


### Use your access token to make your first request

The access token must be provided in each request that need authentication. It must be passed as Authorization header.
A user can belongs to several user groups (operator / seller / customer), so you also must provide the context header that is the user group id who execute the request.
If you're making the request as operator, you must set '1' for this parameters.

<a href="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/postman_first_request.png" target="_blank"><img src="https://storage.gra.cloud.ovh.net/v1/AUTH_bcd845e0b5634d6c8b2535ea00e54c53/ORIGAMIDEVELOPER/postman_first_request.png" alt="postman_login" style="text-align: center"/></a>
 


### PHP script example to setup API connection

Here is an example script on how to make request to Origami API with PHP and Guzzle

```php

<?php

use GuzzleHttp\Client;

$access_token = '';
$base_url = '';
$client_id = 2;
$client_secret = 'secret';
$user_email = 'email';
$user_password = 'password';
$context = 1;

$headers = [
    'Accept' => 'application/json',
    'Content-Type' => 'application/json',
    'context' => $context
];

$params = [
    'client_id' => 2,
    'client_secret' => $client_id,
    'grant_type' => 'password',
    'username' => $user_email,
    'password' => $user_password
];

$client = new Client();
$response = $client->request('post', '/oauth/token', ['form_params' => $params, 'headers' => $headers]);
$headers['Authorization'] = 'Bearer '.json_decode($response->getBody()->getContents())->access_token;

$response = $client->request('get', '/v1/catalog/categories/1', ['headers' => $headers]);
```

You can find endpoints list by clicking <a href="http://doc-api.origami-marketplace.com/">here</a>