# Interceptor Methods: onLoad(), onUnLoad(), etc

The module configuration object is also treated as a [ColdBox Interceptor](http://wiki.coldbox.org/wiki/Interceptors.cfm) once it is created and configured. This means that the object itself can be registered on ALL of the framework's interception points by just creating the appropriate methods. Also, you have two special methods that you can create on the configuration object and they will come alive, much like Application.cfc event methods. These methods are:

* onLoad() : Called when the module is loaded and activated
* onUnLoad() : Called when the module is unloaded from memory

This gives you great hooks for you to do bootup and shutdown commands for this specific module. You can build a [Drupal](http://drupal.org/) or [Wordpress](http://wordpress.org/) like application very easily all built in to the developing platform.

```js
function onLoad(){
  // Register some tables in my database and activate some features
  controller.getWireBox().getInstance('MyModuleService').activate();
    log.info('Module #this.title# loaded correctly');
}

function onUnLoad(){
  // Cleanup some stuff and logit
  controller.getWireBox().getInstance('MyModuleService').shutdown();
  
  // Log we unloaded
  log.info('My module unloaded successfully!);
}
```

Also, remember that the configuration object itself is an interceptor so you can declare all of the framework's interception points in the configuration object and they will be registered as interceptors.

```js
function preProcess(event, interceptData){
  // I just intercepted ALL incoming requests to the application
  log.info('The event executed is #arguments.event.getCurrentEvent()');
}
```

This is a powerful feature, you can create an entire module based on a single CFC and just treat it as an interceptor. So get your brain into gear and let the gas run, you are going for a ride baby!
