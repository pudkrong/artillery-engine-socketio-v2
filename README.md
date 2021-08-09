# artillery-engine-socketio-v2
Socket.IO v2 engine for Artillery

## Disclaimer
The latest artillery is using socket.io-client version 4.x which does not compatible with socket.io version 2.x. The detail is [here](https://socket.io/docs/v3/client-installation/index.html).

### Acknowledge
I also tweak the code to make `acknowledge` to take timeout into account the same as `response` because I have implemented RPC using socket.io.

### Report
#### Timeout
The original library, the timeout report is accumulated value which might not give us more detail in which channel is slow. So, I have extended the error message by adding channel into the error message. So, the repoert will have its own section.

#### Does not match
When the result does not match, we just get error like `Failed match` which sometimes it does not give us the context why it does not match. So, I put the handle to capture the error code. So, the report will contain more context why it does not match

## Install & Configure
Install with npm

```
npm install -D artillery-engine-socketio-v2
```

Enable the `socketio-v2` engine by listing it in `config.engines`. Ex:

```yml
config:
  target: "http://localhost:3000"
  phases:
    - duration: 30
      arrivalRate: 5
  engines:
   socketio-v2: {}
```

In each scenario you must list the engine `socketio-v2` as well. Ex:
```yml
scenarios:
  - name: My first scenario
    engine: socketio-v2
    flow:
      - emit:
          channel: "echo"
```