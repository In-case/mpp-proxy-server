## Usage

Unlike HTTPS or SOCKS proxies, no proxy agent is needed. Just connect to the WebSocket proxy server directly.

The connection URI will be in this format:
```
ws(s)://<hostname/ip>(:<port>)/?target=<targetURI>(&<headername>=<headervalue>…)
```

> If using a cloud application platform, copy the app's URL and replace `http://` with `ws://` or `https://` with `wss://`. Then append the target parameter with the target URI.

The `target` parameter is required to specify where the proxy should connect to. All other parameters are set as headers.

For example, to connect to Multiplayer Piano's server (which requires an origin header) via a WebSocket proxy on localhost port 8080:
```
ws://localhost:8080/?target=ws://www.multiplayerpiano.com:443&origin=http://www.multiplayerpiano.com
```

Query parameters may or may not be encoded, but querystring chars (`&` and `=`) must be encoded to escape them.

**Note:** If the `target` is missing or invalid, or if an error occurs when connecting to the remote host (such as if it responded with a 403), your connection is simply closed. Ideally, the proxy server would wait for the connection to the target to finish, before responding to the client with the same response of the target; however, I found this much too complicated to set up, so I just kept it simple.

To use with MPP in browser, paste into console:

MPP.client.stop();
MPP.client.uri = "ws://localhost:8080/?target=ws://www.multiplayerpiano.com:443&origin=http://www.multiplayerpiano.com";
MPP.client.start();
