# Kudo Laravel Dot Env
Configuration management best practices.

## Getting Started

### Prerequisites

What things you need to install the software and how to install them
This project is showing practices for laravel 4.2, so please prepare the composer.json file requirements as below:

```
"require": {
	"laravel/framework": "4.2.*",
	"vlucas/phpdotenv": "^2.4"
},
```
kindly add
 ```"vlucas/phpdotenv": "^2.4"``` 
if there is not found.

### Installing

Continue to this step, if you has installed composer to your system, kindly run this command
```
composer install
```

Composer will install all the dependencies needed, but please wait with patience.

### Configuring the Dot Env Library

Please open the ```bootstrap/start.php``` file, then find this line:
```
$env = $app->detectEnvironment(array(

	'local' => array('homestead'),

));
```

Please replace those lines with codes as the following:

```
$dotenv = new Dotenv\Dotenv(__DIR__ .'/../');
$dotenv->load();

$env = $app->detectEnvironment(
	function()
	{
		return getenv('APP_ENV');
	}
);
```

### Create a .env file

The next step is putting all environment configurations into a ```.env``` file. 

**REMEMBER**: the ```.env``` file is located on the root path, the same level as composer.json file.

The easiest way to create .env file is by copying from the .env.example file (if the .env.example is found)

```
cp .env.example .env
```

If there is none, kindly create a new .env file

```
touch .env
```

Put this lines into .env file

```
APP_ENV=local
APP_DEBUG=true

```

### Ignore the .env file
Open or Create the ```.gitignore``` file on the root path,
then add this line to the file
```
.env
``` 
This is for the practice to ignore the configuration values commited to the repository.

### Call the configurations been put in .env

In the controller or a library file, the configuration values can be easily called by using function 
```
getenv($env_key)
```

For instance, create a new function in HomeController
```
public function env()
{	
	$appenv = getenv('APP_ENV');
	echo $appenv;
}
```

To show it on the browser, create a new route in ```app/routes.php```

```
Route::get('/env', );
```

## Practice
Put database configuration in .env and call them in config
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
```

Call them in configuration file
``` app/config/database.php```

```
'mysql' => array(
			'driver'    => getenv('DB_CONNECTION'),
			'host'      => getenv('DB_HOST'),
			'database'  => getenv('DB_DATABASE'),
			'username'  => getenv('DB_USERNAME'),
			'password'  => getenv('DB_PASSWORD'),
			'charset'   => 'utf8',
			'collation' => 'utf8_unicode_ci',
			'prefix'    => '',
		),
```

## Contributing

Please kindly contact Kudo Technology Evangelist at our email: kudo-tech@kudo.co.id.



## Authors

* **Hutomo Sugianto** - [hutomo-s.github.io](http://hutomo-s.github.io)
