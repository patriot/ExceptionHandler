ExceptionHandler
================

A PHP Exception Handler to Post Exceptions to a Slack Channel

You will need to Create an Incoming Webhook for your Channel.

You needs to configure this Class before you can use it:

* `\ExceptionHandler::setToken('<your_integration_token>');`
* `\ExceptionHandler::setUsername('<your_subdomain>');`
* `\ExceptionHandler::setWebhookUser('<posting_as_username>');`
* `\ExceptionHandler::setWebhookChannel('<posting_to_channel>');`
* `\ExceptionHandler::setIcon('<your_icon>');`
* `\ExceptionHandler::setEnv('production');`
* `\ExceptionHandler::setHostname('tiberius');`
* `\ExceptionHandler::setVersion('1.0.0');`

And finally set the Exception Handler:

* `set_exception_handler(array('\ExceptionHandler', 'handleException'));`

You will start to get Messages like these in your Channel:

> chrisbookair.local/2.0.79@development: uncaught Exception in file /Users/christian/Code/PhpstormProjects/api-v2/app/Classes/Util/GeneralUtility.php on line 519 (Code: 8): Memcache::connect(): Server 127.0.0.1 (tcp 11211) failed with: Connection refused (61)

ExceptionHandler will quit your current Applications run and returns a `json_encode()`d Message

```json
{
  status: 500
  message: "Okay, Houston, we've had a problem here. -- Don't panic. The Team has been notified."
}
```

By default this ExceptionHandler will care about uncaught Exceptions. If you want to send Slack Messages for Exceptions you handled you can use this like `\ExceptionHandler::handleException($exception, true);` to get notified. ExceptionHandler will not `die()` in this case.
