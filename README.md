# Unleash Proxy Client for the browser (js)

This is a client that your can use in the browser together with the 
unleash-proxy, available for unleash-hosted customers. 

This client expect `fetch` to be available. If you have to support older
browsers you should probably use the [fetch polyfill](https://github.com/github/fetch). 


## How to use the client as a module.


**Step 1: Install**
```js
npm install unleash-proxy-client --save
```

**Step 2: Initialize**
```js
import { UnleashClient } from 'unleash-proxy-client';

const unleash = new UnleashClient({
    url: 'https://eu.unleash-hosted.com/hosted/api',
    clientKey: 'your-proxy-key'
});

// Used to set the context fields, shared with the Unleash Proxy
unleash.updateContext({userId: '1233'});

// Start the background polling
unleash.start();
```

**Step 3: Check if feature toggle is enabled**
```js
unleash.isEnabled('proxy.demo');
```


**Step 4: Get toggle variant**
```js
const variant = unleash.getVariant('proxy.demo');
if(variant.name === 'blue') {
 // somehting with variant blue...
}
```

## How to use the client via CDN.

```html
<html>
<head>
    <script src="https://unpkg.com/unleash-proxy-client@latest/build/main.min.js" type="text/javascript"></script>

    <script type="text/javascript">
        var config = {url: 'https://eu.unleash-hosted.com/hosted/api', clientKey: 'some-proxy-key'};
        var context = {userId: '1233'};
        var client = new unleash.UnleashClient(config, context);
        client.start();

        setTimeout(() => {
            console.log(client.isEnabled('demo.toggle'));
        }, 1000);
    </script>
</head>
</html>
```