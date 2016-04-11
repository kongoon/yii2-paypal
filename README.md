PayPal extension for the Yii2
===========

PayPal payment extension for the Yii2.

Installation
====

Add to the composer.json file following section:

```
php composer.phar require --prefer-dist kongoon/yii2-paypal "*"
```

```
"kongoon/yii2-paypal": "dev-master"
```

Add to to you Yii2 config file this part with component settings:

```php
'paypal'=> [
    'class'        => 'kongoon\yii2\paypal\Paypal',
    'clientId'     => 'you_client_id',
    'clientSecret' => 'you_client_secret',
    'isProduction' => false,
     // This is config file for the PayPal system
     'config'       => [
         'http.ConnectionTimeOut' => 30,
         'http.Retry'             => 1,
         'mode'                   => \kongoon\yii2\Paypal::MODE_SANDBOX, 	// sandbox | live 
         'log.LogEnabled'         => YII_DEBUG ? 1 : 0,
         'log.FileName'           => '@runtime/logs/paypal.log',
         'log.LogLevel'           => \kongoon\yii2\Paypal::LOG_LEVEL_FINE,	// FINE | INFO | WARN | ERROR
    ]
],
```

How Use
====

```php
private function pay() {
    Yii::$app->paypal->init();
    $apiContext = Yii::$app->paypal->getApiContext();
    
    // [..]
    
    $payment = new Payment();
    
    try {
        $payment->create($apiContext);
    } catch (Exception $ex) {
        echo PaypalError($e);
        exit(1);
    }
    $approvalUrl = $payment->getApprovalLink();
}
```