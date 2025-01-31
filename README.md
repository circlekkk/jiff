1.git上拉代码
2.电脑上安装npm和node.js,命令如下：
sudo yum update
sudo yum install epel-release
sudo yum install nodejs
node -v
sudo yum install npm
npm -v
sudo npm install -g npm
3.安装 libsodium-wrappers和socket.io
安装
npm install libsodium-wrappers socket.io
验证
npm list libsodium-wrappers socket.io

# JIFF

[![CircleCI Build Status](https://circleci.com/gh/multiparty/jiff.svg?style=shield)](https://app.circleci.com/pipelines/github/multiparty/jiff)

JIFF is a JavaScript library for building applications that rely on secure multi-party computation. JIFF is built to be highly flexible with a focus on usability, with the ability to be run in the browser, on mobile phones, or via Node.js. JIFF is designed so that developers need not be familiar with MPC techniques or know the details of cryptographic protocols in order to build secure applications.

## Requirements

### Server

Running the server requires [Node](https://nodejs.org/en/) and [npm](https://www.npmjs.com/).

### Client

For browsers, we provide a bundle including the base client side library and its dependencies ([libsodium-wrappers](https://www.npmjs.com/package/libsodium-wrappers) and socket.io). Extensions have to be imported separately.

For node.js clients, npm install should install all the required dependencies.

You can use browserify or similar tools to require JIFF via npm and bundle it with your browser-side JS.

## Installation

Add JIFF as a dependency to your project:
```shell
npm install jiff-mpc
```

### Node.js

After installing JIFF via npm, you can require the server module in your server
code using:
```javascript
const { JIFFServer } = require('jiff-mpc');

// create the JIFF server.
const jiffServer = new JIFFServer(http, options);

// listen for connections.
http.listen(port, cb);
```

[//]: # (首先，您使用require语句从jiff-mpc包中引入了JIFFServer类。这允许您在服务器代码中使用JIFF的功能。)

[//]: # (然后，您创建了一个新的JIFFServer实例，并将其分配给变量jiffServer。这个实例将处理与JIFF相关的所有服务器端逻辑。)

[//]: # (在创建jiffServer实例时，您传递了两个参数：http和options。其中，http是一个HTTP服务器实例，用于处理HTTP请求和响应。options是一个可选的配置对象，用于配置JIFF服务器的各种设置。)

[//]: # (最后，您使用http.listen方法指定服务器应监听的端口号，并在服务器成功启动后调用回调函数cb)
Similarly, you can require the client module in your node.js clients using:
```javascript
const { JIFFClient } = require('jiff-mpc');

// create a jiff client.
const jiffClient = new JIFFClient("<server address>", "<computation_id>", <options>);

// perform some computation.
let shares = jiffClient.share(<secret>);
...
您使用require语句从jiff-mpc包中引入了JIFFClient类。这将允许您在客户端代码中使用JIFF的功能。
然后，您创建了一个新的JIFFClient实例，并将其分配给变量jiffClient。这个实例将与服务器进行通信，并处理与安全多方计算相关的所有客户端逻辑。
在创建jiffClient实例时，您传递了三个参数：<server address>、<computation_id>和<options>。其中，<server address>是服务器的地址，用于指定客户端应与哪个服务器进行通信。<computation_id>是一个字符串，用于标识特定的计算。<options>是一个可选的配置对象，用于配置JIFF客户端的各种设置。
最后，您使用jiffClient.share方法来对一个秘密值进行共享，并将结果存储在变量shares中。这将使用安全多方计算协议来生成秘密值的共享，使得多个参与者可以协同工作来恢复秘密值，而无需显式地交换共享的值。


```

### Client - Browser

To use our bundle, include the provided pre-built JS file in a script tag. Make sure
that you set up your web-server to serve this JS file.
```html
<!-- exposes JIFFClient to the global scope -->
<script src="/dist/jiff-client.js"></script>
```

[//]: # (如何在浏览器端使用一个JavaScript捆绑包的说明。它告诉读者如何将一个预构建的JavaScript文件包含在一个<script>标签中，以便使用该文件中的JIFFClient对象。)

[//]: # (src属性指定了预构建的JavaScript文件的路径，即/dist/jiff-client.js。这应该是读者将文件放置在web服务器上的位置。)

Then inside a script tag (and after the page loads), initialize a JIFF object and set up a computation:
```javascript
const jiffClient = new JIFFClient("<server address>", "<computation_id>", <options>);
```

[//]: # (在JavaScript中初始化一个JIFF（Jiffy）客户端对象，并设置一个计算)

[//]: # (<server address>替换为实际的服务器地址，<computation_id>替换为实际的计算ID，<options>替换为实际的选项（如果有）)
The jiffClient object provides methods for sharing, opening, and performing operations on shares.

Alternatively, you can use the same code for both Node.js and browser-based clients, using tools
such as [browserify](https://browserify.readthedocs.io/en/latest/readme/).

jiffClient对象提供了共享、打开和执行共享操作的方法。

或者，您可以使用相同的代码为Node.js和基于浏览器的客户端，使用工具
例如browserify。
To do this, require JIFF from npm in your client JS code normally, e.g. using `const { JIFFClient } = require('jiff-mpc');`,
and then build your JS code into a bundle using browserify. You can then serve that bundle
via your web server, and include it in your HTML using script tags.

To see an example of this, look at this [JIFF standalone example repo](https://github.com/multiparty/jiff-standalone-example).

为此，通常需要在客户端 JS 代码中使用 npm 的 JIFF，例如使用 const { JIFFClient } = require('jiff-mpc');，
然后使用 browserify 将 JS 代码构建到包中。然后，您可以为该包提供服务
通过您的网络服务器，并使用脚本标记将其包含在您的HTML中。
### Extensions

If you want to support more complex data types, such as Fixedpoint numbers or infinite precision integers,
you should apply the corresponding extension to your client and/or server JIFF instances.

The extensions can be imported via npm, bundled into web clients via browserify, or included directly via
script tags into the browser.

如果你想支持更复杂的数据类型，比如定点数或无限精度整数，
您应该将相应的扩展应用于您的客户端和/或服务器JIFF实例。

扩展可以通过 npm 导入，通过 browserify 打包到 Web 客户端，或者直接通过
将脚本标签插入浏览器。

```javascript
// Server
const { JIFFServer, JIFFServerBigNumber } = require('jiff-mpc');
const jiffServer = new JIFFServer(http, options);
jiffServer.apply_extension(JIFFServerBigNumber);

// Client using node.js or browserify.
const { JIFFClient, JIFFClientBigNumber } = require('jiff-mpc');
const jiffClient = new JIFFClient("<server address>", "<computation_id>", {
  autoConnect: false,
  <other options>
});
jiffClient.apply_extension(JIFFClientBigNumber, options);
jiffClient.connect();
```

```html
<!-- Plain JS without browserify -->
<!-- include the extension and any of its dependencies directly using script tags -->
<!-- make sure your web server serves these files at the corresponding URLs -->
<script src="/bignumber.js/bignumber.min.js"></script>
<script src="/lib/ext/jiff-client-bignumber.js"></script>
```

## Project Layout

    ├─ demos/               Example of common jiff use-cases and functionality
    ├─ docs/                JSDoc config and generated docs
    ├─ lib/                 Libraries for both client and server-side jiff instances
    │  ├─ client/           Implementation of the client side library
    │  ├─ server/           Implementation of the server side library
    │  ├─ ext/              Extended functionality for use cases (e.g. negative numbers): Includes server and client extensions
    │  ├─ common/           Some common helpers between both client and server code
    │  ├─ jiff-client.js    Main module for the client side library, include this (or the bundle under dist/) in your projects
    │  └─ jiff-server.js    Main module for the server side library, include this in your server code
    ├─ test/                Unit testing for base Jiff, demos, and extensions
    │  ├─ dev/              Limited tests for testing some features under development
    │  ├─ live/             Template and setup for live coding with JIFF with nodejs's command line shell (REPL)
    │  └─ suite/            Base Jiff and extension tests (See test/suite/README.md)
    ├─ tutorial/            Contains interactive tutorial files that can be run locally to learn JIFF!

## Running Tutorials

Clone the github repo, and run `npm run tutorial` inside its root directory.

On your terminal, you will see a list of "Routes/Documents". Open either document in your browser to go through the tutorial.

Each document is an independent tutorial. However, beginners are encouraged to view them in order.

## Running Demos and Examples

Run a sample server from one of the demos under `demos` in the following way:
```shell
node demos/<demo-name>/server.js
```
The output from the example server will direct you to open `localhost:8080/demos/<demo-name>/client.html` in a browser (you must open
an instance in a separate window/tab for every distinct party participating in the protocol).
You can then proceed with the protocol using the client interfaces.

Note that you can run Node.js parties that can also participate in the protocol by executing (e.g., a separate terminal for each party):
```shell
node demos/<demo-name>/party.js <input-value>
```

## Documentation

The latest documentation can be viewed on the [project page](https://multiparty.org/jiff/). The documentation can be generated using [JSDoc](http://usejsdoc.org/); you will find these docs in `docs/jsdocs/`:
```shell
./node_modules/.bin/jsdoc -r -c docs/jsdoc.conf.json
npm run-script gen-docs # shortcut
```
### Where to Look in the Docs

The documentation for the client side library is separated into the distinct modules, namespaces, and classes:


    ├─ modules
    │  └─ jiff-client            Parent module: represents the exposed JIFFClient global variable
    ├─ classes
    │  ├─ JIFFClient             Represents a client side jiff instance including the main API of JIFF
    │  ├─ SecretShare            Contains the API for SecretShare objects
    │  ├─ GuardedSocket          Internal wrapper around socket.io for added reliability
    │  └─ Deferred               Polyfill to construct deferred from native Promises
    ├─ namespaces
    │  ├─ protocols              Common protocols exposed by jiff client instances, suitable for preprocessing
    │  ├─ bits                   Primitives for operating on bit-wise shared secrets (hybrid protocols)
    │  └─ hooks                  Available hooks that can be used by users to customize behavior

## Running Tests

All of the JIFF library test cases can be run in the following way:
```shell
npm test
```

Demos are accompanied by test cases. The following command can be used to run the demo servers and test cases:
```shell
npm run-script test-demo -- demos/<demo-name>
```
The command assumes that the server is located at demos/<demo-name>/server.js and the test cases are located at demos/<demo-name>/test.js
See demos/run-test.sh for instructions on running test cases located in different directories or with different names.

See the [testing suite framework documentation](tests/suite/README.md) for more details on running and creating tests for the JIFF library.

## Bundling

If you made changes to the library and would like to bundle it again into a single browser-friendly file, you can run this command:
```shell
npm run-script build # will override dist/jiff-client.js
```

## Development

The JIFF libraries allow developers to customize or extend their functionality by introducing new *hooks*. Multiple hooks can be combined to form a library *extension*.

### Hooks

The JIFF client and server libraries support hooks. Hooks can be provided in the options parameter during instantiation or afterwards. Hooks allow the introduction of custom functionality to be executed at critical times during the computation, or the introduction of different implementations of specified primitives and operations (e.g. using a different sharing scheme).

The client-side [hooks documentation](lib/ext/Hooks.md) provides more details. If hooks are used to provide important reusable functionality, then it is recommended to bundle these hooks within a JIFF extension.

### Extensions

JIFF supports implementing extensions on top of the base implementations that can provide additional extended functionality. Some extensions can be found under `lib/ext`. Two important modules are implemented and provided in this repository: bignumbers and fixed point arithmetic.

See the [extensions documentation](lib/ext/README.md) and the documentation inside `src/ext/jiff-client-bignumber.js` for instructions on how to create additional extensions.

Both client and server libraries support extensions. Some extensions require customizing both the server and client libraries to behave properly (such as the bignumbers extension). Other extensions may require only server or client-side modifications (e.g., the fixed point arithmetic module is only client-side). A server that wants to participate in the computation would require only the client-side extension to use the additional functionality (unless, of course, that extension depends on additional server-side modifications as in bignumbers).

For examples on how to use an extension, see the following files:

1. `demos/sum-fixed/server.js`: using the server with the Node bignumber.js module.
2. `demos/sum-fixed/client.html`: using fixed point arithmetic extension in the browser.

Run the bignumber test suite in the following way:
```shell
npm run-script test-bignumber
```

## How to Contribute
Check out our contribution guidelines and resources @ [contributing](CONTRIBUTING.md).

# For Cryptographers

## Security Model and Assumptions

JIFF is secure against semi-honest adversaries.

JIFF's default preprocessing protocol for beaver triples generation is based on bgw. All protocols that depend on triplets/multiplication are
secure with an honest majority in the preprocessing phase, and against a dishonest majority in the online stage. This is important, since the parties
performing the preprocessing may be different than the ones carrying out the online computation.

If preprocessing is not used, and `crypto_provider` option is set to true during instance creation, JIFF will acquire all required
corelated randomness and preprocessing material from the server. This yields an asymetric trust model, where the computation is secure
against a dishonest majority of non-server parties, but insecure against coalitions of one or more party plus the server. Conretely, this
reduces to more traditional models in certain cases. For example, if the computation is made out of two parties and a server, this becomes
equivalent to 3-party computation with honest majority.

## Costs of Operations: [OUTDATED]
Below is a table of the current costs of operations in the *base* JIFF without extensions:


| Operation         | Rounds            | Total Messages                    | Preprocessing Rounds | Preprocessing Total Messages                 | Dependenices |
|-------------------|-------------------|-----------------------------------|----------------------|----------------------------------------------|--------------|
| Share             | 1                 | senders \* receivers              | 0                    | 0                                            | N/A          |
| Open              | 2                 | sender + sender \* receivers      | 1                    | senders \* senders                           | N/A          |
| +, -, c+, c-, c\* | 0                 | 0                                 | 0                    | 0                                            | N/A          |
| \*                | 2                 | 2\*parties + parties\*(parties-1) | 2                    | 2 \* (parties \* parties - 1)                | triplet,open |
| <, <=, >, >=      | 2\*(bits+3)       | O( bits \* parties^2 )            | 3                    | bits \* (2\*parties + parties^2)             | \*, open     |
| c<, c<=, c>, c>=  | 2\*(bits+3)       | O( bits \* parties^2 )            | 3                    | bits \* (2\*parties + parties^2)             | \*, open     |
| =, c=, !=, c!=    | 2\*(bits+4)       | O( bits \* parties^2 )            | 3                    | 2\*bits \* (2\*parties + parties^2)          | c<, c>, \*   |
| /                 | bits^2 + 5\*bits  | O( bits^2 \* parties^2 )          | 3                    | bits\*(2\*bits \* (2\*parties + parties^2))  | <, c<, \*    |
| c/                | 2\*(bits+3) + 5   | O( bits \* parties^2 )            | 3                    | 4 \* bits \* (2\*parties + parties^2)        | open, \*, c< |
| bits+             | 8\*bits           | O( parties^2 \* bits )            | 2                    | 8 \* bits \* (parties \* parties - 1)        | triplet,open | 
| bits-             | 8\*bits           | O( parties^2 \* bits )            | 2                    | 8 \* bits \* (parties \* parties - 1)        | triplet,open |
| bits*             | 12\*bits          | O( parties^4 \* bits^2 )          | 2                    | 12 \* bits^2 \* (parties \* parties - 1)^2   | triplet,open |
| bits/             | 25\*bits^2        | O( parties^2 \* bits^2 )          | 2                    | 25 \* bits^2 \* (parties \* parties - 1)     | triplet,open |

Some exact costs not shown in the table:
1. Exact total number of messages for secret inequalities is: 3\*(parties + parties^2 + (bits+1) \* (2\*parties + parties\*(parties-1))) + 2\*parties + parties\*(parties-1)
2. Exact total number of messages for constant inequalities is: 2\*(parties + parties^2 + (bits+1) \* (2\*parties + parties\*(parties-1))) + 2\*parties + parties\*(parties-1)
3. Exact total number of messages for equality checks: 2\*(\*(parties + parties^2 + (bits+1) \* (2\*parties + parties\*(parties-1))) + 2\*parties + parties\*(parties-1)) + 2\*parties + parties\*(parties-1)
4. Exact total number of messages for division is: bits \* ( 5\*(parties + parties^2 + (bits+1) \* (2\*parties + parties\*(parties-1))) + 2\*parties + parties\*(parties-1) + 2\*parties + parties\*(parties-1) )
5. Exact total number of messages for constant division is: 1 + 7\*parties + 4\*parties^2 + 8\*(parties + parties^2 + (bits+1) \* (2\*parties + parties\*(parties-1)))

Dependenices:
1. Multiplication has one message to synchronize beaver triplets and one open in sequence.
2. inequality tests has 3 less than half primes in parallel, each has an open and as many multiplication in sequence as bits.
3. constant inequality test has 2 less than half primes in parallel.
4. equality and constant equality tests have 2 inequalities in parallel, sequenced with a multiplication.
5. division has as many sequential iterations as bits, each iteration contains a constant inequality, secret inequality, and multiplication.
6. constant division has one open sequenced with 4 parallel constant inequality checks and two multiplications.
7. Secret XORs and ORs are equivalent to a single multiplication, constant XORs and ORs are free.


## Information and Collaborators

More information about this project, including collaborators and publications, can be found at [multiparty.org](https://multiparty.org/).
