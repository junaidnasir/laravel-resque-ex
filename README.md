## Laravel Resque

This package allows you to connect to Resque when using `Queue`.

fixes some problems of deedod's [laravel-resque-ex](https://github.com/deedod/laravel-resque-ex). (Resque queue was overwriting other queues)

This fork fixes the problem of queues overwriting (all queues are overwrited when using resque service providor.

## Requirements
- PHP 5.4+

## Installation

Add the following to your project's `composer.json`:

    "require": {
    	"junaidnasir/laravel-resque-ex": "^1.0"
    }

Now you need to run the following to install the package:

	composer update

Next you need to add the following service provider to your `app/config/app.php`:

    'Resque\ServiceProviders\ResqueServiceProvider'

Now you need to add the following to your `/app/config/queue.php` "connections" section:

    "resque" => [
    	"driver" => "resque"
    ]

If you wish to use this driver as your default Queue driver you will need to set the following as your "default" drive in `app/config/queue.php`:

    "default" => "resque",


## Usage

If you choose to not use this driver as your default Queue driver you can call a Queue method on demand by doing:

    Queue::connection('resque')->push('JobName', ['name' => 'Andrew']);

### Enqueing a Job

	Queue::push('JobName', ['name' => 'Andrew']);

### Tracking a Job

	$token = Queue::push('JobName', ['name' => 'Andrew'], true);
	$status = Queue::getStatus($token);

### Enqueing a Future Job

	$when = time() + 3600; // 1 hour from now
	Queue::later($when, 'JobName', ['name' => 'Andrew']);

## Further Documentation

- [PHP-Resque](https://github.com/kamisama/php-resque-ex)
- [PHP-Resque-Scheduler](https://github.com/kamisama/php-resque-ex-scheduler)

## License

Laravel Resque is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).
