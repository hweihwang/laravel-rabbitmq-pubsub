# Laravel PubSub Library
Laravel pub/sub library allows you to publish and consume and process rabbit events.

# Installation
```bash
composer require chocofamilyme/laravel-pubsub
```

# Publishing the configuration (optional)
```bash
php artisan vendor:publish --provider="Chocofamilyme\LaravelPubSub\Providers\PubSubServiceProvider"
```

# Configuration
## AMQP
AMQP configuration file is located under config/queue.php and contains configuration for RabbitMQ.

## PubSub
PubSub configuration file is located under config/pubsub.php and contains configuration for EventRouting.
```php
<?php

return [
    /*
    |--------------------------------------------------------------------------
    | Listen for events
    |--------------------------------------------------------------------------
    |
    | Define event name and it's listeners. Please notice that one event name may have multiple listeners
    |
    | Example:
    |
    | 'user.notified' => [
    |     NotifyAboutDeviceChangeListener::class,
    | ],
    |
    */
    'listen' => [
    ]
];
```

## Usage
### Single event
```bash
php artisan event:listen gateway.user.authenticated --job=common
```
Will listen to single event "gateway.user.authenticated" in default exchange and queue name

### Wildcard event
```bash
php artisan event:listen gateway.user.# --exchange=gateway --queue=guardqueue --job=common
```
Will listen to all "gateway.user.*" events in exchange gateway and with queue name "guardqueue"

### Laravel event
```bash
php artisan event:listen
```


### Base publish message

```php
 Amqp::publish('route.test', ['bodyKey' => 'bodyValue'], [
        'exchange' => [
            'name' => 'test',
            'type' => 'topic',
        ],
        'headers' => [
            'application_headers' => [
                'headerKey' => 'headerValue'
            ],
            'message_id' => 'uuid4',
        ],
    ]
);
```
