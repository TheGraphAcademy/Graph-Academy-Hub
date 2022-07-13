# Unit Testing Framework

Matchstick is a unit testing framework, developed by [LimeChain](https://limechain.tech/), that enables subgraph developers to test their mapping logic in a sandboxed environment and deploy their subgraphs with confidence!

### Getting Started <a href="#getting-started" id="getting-started"></a>

#### Install dependencies <a href="#install-dependencies" id="install-dependencies"></a>

In order to use the test helper methods and run the tests, you will need to install the following dependencies:

```
yarn add --dev matchstick-as
```

❗ `graph-node` depends on PostgreSQL, so if you don't already have it, you will need to install it. We highly advise using the commands below as adding it in any other way may cause unexpected errors!

**MacOS**

Postgres installation command:

```
brew install postgresql
```

**Linux**

Postgres installation command (depends on your distro):

```
sudo apt install postgresql
```

#### WSL (Windows Subsystem for Linux) <a href="#wsl-windows-subsystem-for-linux" id="wsl-windows-subsystem-for-linux"></a>

You can use Matchstick on WSL both using the Docker approach and the binary approach. As WSL can be a bit tricky, here's a few tips in case you encounter issues like

```
static BYTES = Symbol("Bytes") SyntaxError: Unexpected token =
```

or

```
<PROJECT_PATH>/node_modules/gluegun/build/index.js:13 throw up;
```

Please make sure you're on a newer version of Node.js graph-cli doesn't support **v10.19.0** anymore, and that is still the default version for new Ubuntu images on WSL. For instance Matchstick is confirmed to be working on WSL with **v18.1.0**, you can switch to it either via **nvm** or if you update your global Node.js. Don't forget to delete `node_modules` and to run `npm install` again after updating you nodejs! Then, make sure you have **libpq** installed, you can do that by running

```
sudo apt-get install libpq-dev
```

And finally, do not use `graph test` (which uses your global installation of graph-cli and for some reason that looks like it's broken on WSL currently), instead use `yarn test` or `npm run test` (that will use the local, project-level instance of graph-cli, which works like a charm. For that you would of course need to have a `"test"` script in your `package.json` file which can be something as simple as

```
{  "name": "demo-subgraph",  "version": "0.1.0",  "scripts": {    "test": "graph test",    ...  },  "dependencies": {    "@graphprotocol/graph-cli": "^0.30.0",    "@graphprotocol/graph-ts": "^0.27.0",    "matchstick-as": "^0.5.0"  }}
```

#### Usage <a href="#usage" id="usage"></a>

To use **Matchstick** in your subgraph project just open up a terminal, navigate to the root folder of your project and simply run `graph test [options] <datasource>` - it downloads the latest **Matchstick** binary and runs the specified test or all tests in a test folder (or all existing tests if no datasource flag is specified).

#### CLI options <a href="#cli-options" id="cli-options"></a>

This will run all tests in the test folder:

```
graph test
```

This will run a test named gravity.test.ts and/or all test inside of a folder named gravity:

```
graph test gravity
```

This will run only that specific test file:

```
graph test path/to/file.test.ts
```

**Options:**

```
-c, --coverage                Run the tests in coverage mode-d, --docker                  Run the tests in a docker container (Note: Please execute from the root folder of the subgraph)-f  --force                   Binary: Redownloads the binary. Docker: Redownloads the Dockerfile and rebuilds the docker image.-h, --help                    Show usage information-l, --logs                    Logs to the console information about the OS, CPU model and download url (debugging purposes)-r, --recompile               Forces tests to be recompiled-v, --version <tag>           Choose the version of the rust binary that you want to be downloaded/used
```

#### Docker <a href="#docker" id="docker"></a>

From `graph-cli 0.25.2`, the `graph test` command supports running `matchstick` in a docker container with the `-d` flag. The docker implementation uses [bind mount](https://docs.docker.com/storage/bind-mounts/) so it does not have to rebuild the docker image every time the `graph test -d` command is executed. Alternatively you can follow the instructions from the [matchstick](https://github.com/LimeChain/matchstick#docker-) repository to run docker manually.

❗ If you have previously ran `graph test` you may encounter the following error during docker build:

```
error from sender: failed to xattr node_modules/binary-install-raw/bin/binary-<platform>: permission denied
```

In this case create a `.dockerignore` in the root folder and add `node_modules/binary-install-raw/bin`

#### Configuration <a href="#configuration" id="configuration"></a>

Matchstick can be configured to use a custom tests, libs and manifest path via `matchstick.yaml` config file:

```
testsFolder: path/to/testslibsFolder: path/to/libsmanifestPath: path/to/subgraph.yaml
```

#### Demo subgraph <a href="#demo-subgraph" id="demo-subgraph"></a>

You can try out and play around with the examples from this guide by cloning the [Demo Subgraph repo](https://github.com/LimeChain/demo-subgraph)

#### Video tutorials <a href="#video-tutorials" id="video-tutorials"></a>

Also you can check out the video series on ["How to use Matchstick to write unit tests for your subgraphs"](https://www.youtube.com/playlist?list=PLTqyKgxaGF3SNakGQwczpSGVjS\_xvOv3h)

### Tests structure (>=0.5.0) <a href="#tests-structure-0-5-0" id="tests-structure-0-5-0"></a>

_**IMPORTANT: Requires matchstick-as >=0.5.0**_

#### describe() <a href="#describe" id="describe"></a>

`describe(name: String , () => {})` - Defines a test group.

_**Notes:**_

* _Describes are not mandatory. You can still use test() the old way, outside of the describe() blocks_

Example:

```
import { describe, test } from "matchstick-as/assembly/index"import { handleNewGravatar } from "../../src/gravity"
describe("handleNewGravatar()", () => {  test("Should create a new Gravatar entity", () => {    ...  })})
```

Nested `describe()` example:

```
import { describe, test } from "matchstick-as/assembly/index"import { handleUpdatedGravatar } from "../../src/gravity"
describe("handleUpdatedGravatar()", () => {  describe("When entity exists", () => {    test("updates the entity", () => {      ...    })  })
  describe("When entity does not exists", () => {    test("it creates a new entity", () => {      ...    })  })})
```

***

#### test() <a href="#test" id="test"></a>

`test(name: String, () =>, should_fail: bool)` - Defines a test case. You can use test() inside of describe() blocks or independently.

Example:

```
import { describe, test } from "matchstick-as/assembly/index"import { handleNewGravatar } from "../../src/gravity"
describe("handleNewGravatar()", () => {  test("Should create a new Entity", () => {    ...  })})
```

or

```
test("handleNewGravatar() should create a new entity", () => {  ...})
```

***

#### beforeAll() <a href="#before-all" id="before-all"></a>

Runs a code block before any of the tests in the file. If `beforeAll` is declared inside of a `describe` block, it runs at the beginning of that `describe` block.

Examples:

Code inside `beforeAll` will execute once before _all_ tests in the file.

```
import { describe, test, beforeAll } from "matchstick-as/assembly/index"import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"import { Gravatar } from "../../generated/schema"
beforeAll(() => {  let gravatar = new Gravatar("0x0")  gravatar.displayName = “First Gravatar”  gravatar.save()  ...})
describe("When the entity does not exist", () => {  test("it should create a new Gravatar with id 0x1", () => {    ...  })})
describe("When entity already exists", () => {  test("it should update the Gravatar with id 0x0", () => {    ...  })})
```

Code inside `beforeAll` will execute once before all tests in the first describe block

```
import { describe, test, beforeAll } from "matchstick-as/assembly/index"import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"import { Gravatar } from "../../generated/schema"
describe("handleUpdatedGravatar()", () => {  beforeAll(() => {    let gravatar = new Gravatar("0x0")    gravatar.displayName = “First Gravatar”    gravatar.save()    ...  })
  test("updates Gravatar with id 0x0", () => {    ...  })
  test("creates new Gravatar with id 0x1", () => {    ...  })})
```

***

#### afterAll() <a href="#after-all" id="after-all"></a>

Runs a code block after all of the tests in the file. If `afterAll` is declared inside of a `describe` block, it runs at the end of that `describe` block.

Example:

Code inside `afterAll` will execute once after _all_ tests in the file.

```
import { describe, test, afterAll } from "matchstick-as/assembly/index"import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"import { store } from "@graphprotocol/graph-ts"
afterAll(() => {  store.remove("Gravatar", "0x0")  ...})
describe("handleNewGravatar, () => {  test("creates Gravatar with id 0x0", () => {    ...  })})
describe("handleUpdatedGravatar", () => {  test("updates Gravatar with id 0x0", () => {    ...  })})
```

Code inside `afterAll` will execute once after all tests in the first describe block

```
import { describe, test, afterAll, clearStore } from "matchstick-as/assembly/index"import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"
describe("handleNewGravatar", () => {	afterAll(() => {    store.remove("Gravatar", "0x1")    ...	})
  test("It creates a new entity with Id 0x0", () => {    ...  })
  test("It creates a new entity with Id 0x1", () => {    ...  })})
describe("handleUpdatedGravatar", () => {  test("updates Gravatar with id 0x0", () => {    ...  }) })
```

***

#### beforeEach() <a href="#before-each" id="before-each"></a>

Runs a code block before every test. If `beforeEach` is declared inside of a `describe` block, it runs before each test in that `describe` block.

Examples: Code inside `beforeEach` will execute before each tests.

```
import { describe, test, beforeEach, clearStore } from "matchstick-as/assembly/index"import { handleNewGravatars } from "./utils"
beforeEach(() => {  clearStore() // <-- clear the store before each test in the file})
describe("handleNewGravatars, () => {  test("A test that requires a clean store", () => {    ...  })
  test("Second that requires a clean store", () => {    ...  })})
 ...
```

Code inside `beforeEach` will execute only before each test in the that describe

```
import { describe, test, beforeEach } from "matchstick-as/assembly/index"import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"
describe("handleUpdatedGravatars", () => {  beforeEach(() => {    let gravatar = new Gravatar("0x0")    gravatar.displayName = "First Gravatar"    gravatar.imageUrl = ""    gravatar.save()  })
  test("Upates the displayName", () => {     assert.fieldEqual("Gravatar", "0x0", "displayNamd", "First Gravatar")
    // code that should update the displayName to 1st Gravatar
    assert.fieldEqual("Gravatar", "0x0", "displayName", "1st Gravatar")    store.remove("Gravatar", "0x0")  })
  test("Updates the imageUrl", () => {    assert.fieldEqual("Gravatar", "0x0", "imageUrl", "")
    // code that should changes the imageUrl to https://www.gravatar.com/avatar/0x0
    assert.fieldEqual("Gravatar", "0x0", "imageUrl", "https://www.gravatar.com/avatar/0x0")    store.remove("Gravatar", "0x0")  })})
```

***

#### afterEach() <a href="#after-each" id="after-each"></a>

Runs a code block after every test. If `afterEach` is declared inside of a `describe` block, it runs after each test in that `describe` block.

Examples:

Code inside `afterEach` will execute after every test.

```
import { describe, test, beforeEach, afterEach } from "matchstick-as/assembly/index"import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"
beforeEach(() => {  let gravatar = new Gravatar("0x0")  gravatar.displayName = “First Gravatar”  gravatar.save()})
afterEach(() => {  store.remove("Gravatar", "0x0")})
describe("handleNewGravatar", () => {  ...})
describe("handleUpdatedGravatar", () => {  test("Upates the displayName", () => {     assert.fieldEqual("Gravatar", "0x0", "displayNamd", "First Gravatar")
    // code that should update the displayName to 1st Gravatar
    assert.fieldEqual("Gravatar", "0x0", "displayName", "1st Gravatar")  })
  test("Updates the imageUrl", () => {    assert.fieldEqual("Gravatar", "0x0", "imageUrl", "")
    // code that should changes the imageUrl to https://www.gravatar.com/avatar/0x0
    assert.fieldEqual("Gravatar", "0x0", "imageUrl", "https://www.gravatar.com/avatar/0x0")  })})
```

Code inside `afterEach` will execute after each test in that describe

```
import { describe, test, beforeEach, afterEach } from "matchstick-as/assembly/index"import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"
describe("handleNewGravatar", () => {  ...})
describe("handleUpdatedGravatar", () => {  beforeEach(() => {    let gravatar = new Gravatar("0x0")    gravatar.displayName = "First Gravatar"    gravatar.imageUrl = ""    gravatar.save()  })
  afterEach(() => {    store.remove("Gravatar", "0x0")  })
  test("Upates the displayName", () => {     assert.fieldEqual("Gravatar", "0x0", "displayNamd", "First Gravatar")
    // code that should update the displayName to 1st Gravatar
    assert.fieldEqual("Gravatar", "0x0", "displayName", "1st Gravatar")  })
  test("Updates the imageUrl", () => {    assert.fieldEqual("Gravatar", "0x0", "imageUrl", "")
    // code that should changes the imageUrl to https://www.gravatar.com/avatar/0x0
    assert.fieldEqual("Gravatar", "0x0", "imageUrl", "https://www.gravatar.com/avatar/0x0")  })})
```

### Asserts <a href="#asserts" id="asserts"></a>

```
fieldEquals(entityType: string, id: string, fieldName: string, expectedVal: string)
equals(expected: ethereum.Value, actual: ethereum.Value)
notInStore(entityType: string, id: string)
addressEquals(address1: Address, address2: Address)
bytesEquals(bytes1: Bytes, bytes2: Bytes)
i32Equals(number1: i32, number2: i32)
bigIntEquals(bigInt1: BigInt, bigInt2: BigInt)
booleanEquals(bool1: boolean, bool2: boolean)
stringEquals(string1: string, string2: string)
arrayEquals(array1: Array<ethereum.Value>, array2: Array<ethereum.Value>)
tupleEquals(tuple1: ethereum.Tuple, tuple2: ethereum.Tuple)
assertTrue(value: boolean)
assertNull<T>(value: T)
assertNotNull<T>(value: T)
entityCount(entityType: string, expectedCount: i32)
```

### Write a Unit Test <a href="#write-a-unit-test" id="write-a-unit-test"></a>

Let's see how a simple unit test would look like using the Gravatar examples in the [Demo Subgraph](https://github.com/LimeChain/demo-subgraph/blob/main/src/gravity.ts).

Assuming we have the following handler function (along with two helper functions to make our life easier):

```
export function handleNewGravatar(event: NewGravatar): void {  let gravatar = new Gravatar(event.params.id.toHex())  gravatar.owner = event.params.owner  gravatar.displayName = event.params.displayName  gravatar.imageUrl = event.params.imageUrl  gravatar.save()}
export function handleNewGravatars(events: NewGravatar[]): void {  events.forEach((event) => {    handleNewGravatar(event)  })}
export function createNewGravatarEvent(  id: i32,  ownerAddress: string,  displayName: string,  imageUrl: string): NewGravatar {  let mockEvent = newMockEvent()  let newGravatarEvent = new NewGravatar(    mockEvent.address,    mockEvent.logIndex,    mockEvent.transactionLogIndex,    mockEvent.logType,    mockEvent.block,    mockEvent.transaction,    mockEvent.parameters  )  newGravatarEvent.parameters = new Array()  let idParam = new ethereum.EventParam('id', ethereum.Value.fromI32(id))  let addressParam = new ethereum.EventParam(    'ownderAddress',    ethereum.Value.fromAddress(Address.fromString(ownerAddress))  )  let displayNameParam = new ethereum.EventParam('displayName', ethereum.Value.fromString(displayName))  let imageUrlParam = new ethereum.EventParam('imageUrl', ethereum.Value.fromString(imageUrl))
  newGravatarEvent.parameters.push(idParam)  newGravatarEvent.parameters.push(addressParam)  newGravatarEvent.parameters.push(displayNameParam)  newGravatarEvent.parameters.push(imageUrlParam)
  return newGravatarEvent}
```

We first have to create a test file in our project. This is an example of how that might look like:

```
import { clearStore, test, assert } from 'matchstick-as/assembly/index'import { Gravatar } from '../../generated/schema'import { NewGravatar } from '../../generated/Gravity/Gravity'import { createNewGravatarEvent, handleNewGravatars } from '../mappings/gravity'
test('Can call mappings with custom events', () => {  // Create a test entity and save it in the store as initial state (optional)  let gravatar = new Gravatar('gravatarId0')  gravatar.save()
  // Create mock events  let newGravatarEvent = createNewGravatarEvent(12345, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')  let anotherGravatarEvent = createNewGravatarEvent(3546, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')
  // Call mapping functions passing the events we just created  handleNewGravatars([newGravatarEvent, anotherGravatarEvent])
  // Assert the state of the store  assert.fieldEquals('Gravatar', 'gravatarId0', 'id', 'gravatarId0')  assert.fieldEquals('Gravatar', '12345', 'owner', '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7')  assert.fieldEquals('Gravatar', '3546', 'displayName', 'cap')
  // Clear the store in order to start the next test off on a clean slate  clearStore()})
test('Next test', () => {  //...})
```

That's a lot to unpack! First off, an important thing to notice is that we're importing things from `matchstick-as`, our AssemblyScript helper library (distributed as an npm module). You can find the repository [here](https://github.com/LimeChain/matchstick-as). `matchstick-as` provides us with useful testing methods and also defines the `test()` function which we will use to build our test blocks. The rest of it is pretty straightforward - here's what happens:

* We're setting up our initial state and adding one custom Gravatar entity;
* We define two `NewGravatar` event objects along with their data, using the `createNewGravatarEvent()` function;
* We're calling out handler methods for those events - `handleNewGravatars()` and passing in the list of our custom events;
* We assert the state of the store. How does that work? - We're passing a unique combination of Entity type and id. Then we check a specific field on that Entity and assert that it has the value we expect it to have. We're doing this both for the initial Gravatar Entity we added to the store, as well as the two Gravatar entities that gets added when the handler function is called;
* And lastly - we're cleaning the store using `clearStore()` so that our next test can start with a fresh and empty store object. We can define as many test blocks as we want.

There we go - we've created our first test! 👏

Now in order to run our tests you simply need to run the following in your subgraph root folder:

`graph test Gravity`

And if all goes well you should be greeted with the following:

![Matchstick saying “All tests passed!”](https://thegraph.com/docs/img/matchstick-tests-passed.png)

### Common test scenarios <a href="#common-test-scenarios" id="common-test-scenarios"></a>

#### Hydrating the store with a certain state <a href="#hydrating-the-store-with-a-certain-state" id="hydrating-the-store-with-a-certain-state"></a>

Users are able to hydrate the store with a known set of entities. Here's an example to initialise the store with a Gravatar entity:

```
let gravatar = new Gravatar('entryId')gravatar.save()
```

#### Calling a mapping function with an event <a href="#calling-a-mapping-function-with-an-event" id="calling-a-mapping-function-with-an-event"></a>

A user can create a custom event and pass it to a mapping function that is bound to the store:

```
import { store } from 'matchstick-as/assembly/store'import { NewGravatar } from '../../generated/Gravity/Gravity'import { handleNewGravatars, createNewGravatarEvent } from './mapping'
let newGravatarEvent = createNewGravatarEvent(12345, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')
handleNewGravatar(newGravatarEvent)
```

#### Calling all of the mappings with event fixtures <a href="#calling-all-of-the-mappings-with-event-fixtures" id="calling-all-of-the-mappings-with-event-fixtures"></a>

Users can call the mappings with test fixtures.

```
import { NewGravatar } from '../../generated/Gravity/Gravity'import { store } from 'matchstick-as/assembly/store'import { handleNewGravatars, createNewGravatarEvent } from './mapping'
let newGravatarEvent = createNewGravatarEvent(12345, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')
let anotherGravatarEvent = createNewGravatarEvent(3546, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')
handleNewGravatars([newGravatarEvent, anotherGravatarEvent])
```

```
export function handleNewGravatars(events: NewGravatar[]): void {    events.forEach(event => {        handleNewGravatar(event);    });}
```

#### Mocking contract calls <a href="#mocking-contract-calls" id="mocking-contract-calls"></a>

Users can mock contract calls:

```
import { addMetadata, assert, createMockedFunction, clearStore, test } from 'matchstick-as/assembly/index'import { Gravity } from '../../generated/Gravity/Gravity'import { Address, BigInt, ethereum } from '@graphprotocol/graph-ts'
let contractAddress = Address.fromString('0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7')let expectedResult = Address.fromString('0x90cBa2Bbb19ecc291A12066Fd8329D65FA1f1947')let bigIntParam = BigInt.fromString('1234')createMockedFunction(contractAddress, 'gravatarToOwner', 'gravatarToOwner(uint256):(address)')  .withArgs([ethereum.Value.fromSignedBigInt(bigIntParam)])  .returns([ethereum.Value.fromAddress(Address.fromString('0x90cBa2Bbb19ecc291A12066Fd8329D65FA1f1947'))])
let gravity = Gravity.bind(contractAddress)let result = gravity.gravatarToOwner(bigIntParam)
assert.equals(ethereum.Value.fromAddress(expectedResult), ethereum.Value.fromAddress(result))
```

As demonstrated, in order to mock a contract call and hardcore a return value, the user must provide a contract address, function name, function signature, an array of arguments, and of course - the return value.

Users can also mock function reverts:

```
let contractAddress = Address.fromString('0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7')createMockedFunction(contractAddress, 'getGravatar', 'getGravatar(address):(string,string)')  .withArgs([ethereum.Value.fromAddress(contractAddress)])  .reverts()
```

#### Mocking IPFS files (from matchstick 0.4.1) <a href="#mocking-ipfs-files-from-matchstick-0-4-1" id="mocking-ipfs-files-from-matchstick-0-4-1"></a>

Users can mock IPFS files by using `mockIpfsFile(hash, filePath)` function. The function accepts two arguments, the first one is the IPFS file hash/path and the second one is the path to a local file.

NOTE: When testing `ipfs.map/ipfs.mapJSON`, the callback function must be exported from the test file in order for matchstck to detect it, like the `processGravatar()` function in the test example bellow:

`.test.ts` file:

```
import { assert, test, mockIpfsFile } from 'matchstick-as/assembly/index'import { ipfs } from '@graphprotocol/graph-ts'import { gravatarFromIpfs } from './utils'
// Export ipfs.map() callback in order for matchstck to detect itexport { processGravatar } from './utils'
test('ipfs.cat', () => {  mockIpfsFile('ipfsCatfileHash', 'tests/ipfs/cat.json')
  assert.entityCount(GRAVATAR_ENTITY_TYPE, 0)
  gravatarFromIpfs()
  assert.entityCount(GRAVATAR_ENTITY_TYPE, 1)  assert.fieldEquals(GRAVATAR_ENTITY_TYPE, '1', 'imageUrl', 'https://i.ytimg.com/vi/MELP46s8Cic/maxresdefault.jpg')
  clearStore()})
test('ipfs.map', () => {  mockIpfsFile('ipfsMapfileHash', 'tests/ipfs/map.json')
  assert.entityCount(GRAVATAR_ENTITY_TYPE, 0)
  ipfs.map('ipfsMapfileHash', 'processGravatar', Value.fromString('Gravatar'), ['json'])
  assert.entityCount(GRAVATAR_ENTITY_TYPE, 3)  assert.fieldEquals(GRAVATAR_ENTITY_TYPE, '1', 'displayName', 'Gravatar1')  assert.fieldEquals(GRAVATAR_ENTITY_TYPE, '2', 'displayName', 'Gravatar2')  assert.fieldEquals(GRAVATAR_ENTITY_TYPE, '3', 'displayName', 'Gravatar3')})
```

`utils.ts` file:

```
import { Address, ethereum, JSONValue, Value, ipfs, json, Bytes } from "@graphprotocol/graph-ts"import { Gravatar } from "../../generated/schema"
...
// ipfs.map callbackexport function processGravatar(value: JSONValue, userData: Value): void {  // See the JSONValue documentation for details on dealing  // with JSON values  let obj = value.toObject()  let id = obj.get('id')
  if (!id) {    return  }
  // Callbacks can also created entities  let gravatar = new Gravatar(id.toString())  gravatar.displayName = userData.toString() + id.toString()  gravatar.save()}
// function that calls ipfs.catexport function gravatarFromIpfs(): void {  let rawData = ipfs.cat("ipfsCatfileHash")
  if (!rawData) {    return  }
  let jsonData = json.fromBytes(rawData as Bytes).toObject()
  let id = jsonData.get('id')  let url = jsonData.get("imageUrl")
  if (!id || !url) {    return  }
  let gravatar = new Gravatar(id.toString())  gravatar.imageUrl = url.toString()  gravatar.save()}
```

#### Asserting the state of the store <a href="#asserting-the-state-of-the-store" id="asserting-the-state-of-the-store"></a>

Users are able to assert the final (or midway) state of the store through asserting entities. In order to do this, the user has to supply an Entity type, the specific ID of an Entity, a name of a field on that Entity, and the expected value of the field. Here's a quick example:

```
import { assert } from 'matchstick-as/assembly/index'import { Gravatar } from '../generated/schema'
let gravatar = new Gravatar('gravatarId0')gravatar.save()
assert.fieldEquals('Gravatar', 'gravatarId0', 'id', 'gravatarId0')
```

Running the assert.fieldEquals() function will check for equality of the given field against the given expected value. The test will fail and an error message will be outputted if the values are **NOT** equal. Otherwise the test will pass successfully.

#### Interacting with Event metadata <a href="#interacting-with-event-metadata" id="interacting-with-event-metadata"></a>

Users can use default transaction metadata, which could be returned as an ethereum.Event by using the `newMockEvent()` function. The following example shows how you can read/write to those fields on the Event object:

```
// Readlet logType = newGravatarEvent.logType
// Writelet UPDATED_ADDRESS = '0xB16081F360e3847006dB660bae1c6d1b2e17eC2A'newGravatarEvent.address = Address.fromString(UPDATED_ADDRESS)
```

#### Asserting variable equality <a href="#asserting-variable-equality" id="asserting-variable-equality"></a>

```
assert.equals(ethereum.Value.fromString("hello"); ethereum.Value.fromString("hello"));
```

#### Asserting that an Entity is **not** in the store <a href="#asserting-that-an-entity-is-not-in-the-store" id="asserting-that-an-entity-is-not-in-the-store"></a>

Users can assert that an entity does not exist in the store. The function takes an entity type and an id. If the entity is in fact in the store, the test will fail with a relevant error message. Here's a quick example of how to use this functionality:

```
assert.notInStore('Gravatar', '23')
```

#### Printing the whole store (for debug purposes) <a href="#printing-the-whole-store-for-debug-purposes" id="printing-the-whole-store-for-debug-purposes"></a>

You can print the whole store to the console using this helper function:

```
import { logStore } from 'matchstick-as/assembly/store'
logStore()
```

#### Expected failure <a href="#expected-failure" id="expected-failure"></a>

Users can have expected test failures, using the shouldFail flag on the test() functions:

```
test(  'Should throw an error',  () => {    throw new Error()  },  true)
```

If the test is marked with shouldFail = true but DOES NOT fail, that will show up as an error in the logs and the test block will fail. Also, if it's marked with shouldFail = false (the default state), the test executor will crash.

#### Logging <a href="#logging" id="logging"></a>

Having custom logs in the unit tests is exactly the same as logging in the mappings. The difference is that the log object needs to be imported from matchstick-as rather than graph-ts. Here's a simple example with all non-critical log types:

```
import { test } from "matchstick-as/assembly/index";import { log } from "matchstick-as/assembly/log";
test("Success", () => {    log.success("Success!". []);});test("Error", () => {    log.error("Error :( ", []);});test("Debug", () => {    log.debug("Debugging...", []);});test("Info", () => {    log.info("Info!", []);});test("Warning", () => {    log.warning("Warning!", []);});
```

Users can also simulate a critical failure, like so:

```
test('Blow everything up', () => {  log.critical('Boom!')})
```

Logging critical errors will stop the execution of the tests and blow everything up. After all - we want to make sure you're code doesn't have critical logs in deployment, and you should notice right away if that were to happen.

#### Testing derived fields <a href="#testing-derived-fields" id="testing-derived-fields"></a>

Testing derived fields is a feature which (as the example below shows) allows the user to set a field in a certain entity and have another entity be updated automatically if it derives one of its fields from the first entity. Important thing to note is that the first entity needs to be reloaded as the automatic update happens in the store in rust of which the AS code is agnostic.

```
test('Derived fields example test', () => {  let mainAccount = new GraphAccount('12')  mainAccount.save()  let operatedAccount = new GraphAccount('1')  operatedAccount.operators = ['12']  operatedAccount.save()  let nst = new NameSignalTransaction('1234')  nst.signer = '12'  nst.save()
  assert.assertNull(mainAccount.get('nameSignalTransactions'))  assert.assertNull(mainAccount.get('operatorOf'))
  mainAccount = GraphAccount.load('12')!
  assert.i32Equals(1, mainAccount.nameSignalTransactions.length)  assert.stringEquals('1', mainAccount.operatorOf[0])})
```

#### Testing dynamic data sources <a href="#testing-dynamic-data-sources" id="testing-dynamic-data-sources"></a>

Testing dynamic data sources can be be done by mocking the return value of the `context()`, `address()` and `network()` functions of the dataSource namespace. These functions currently return the following: `context()` - returns an empty entity (DataSourceContext), `address()` - returns `0x0000000000000000000000000000000000000000`, `network()` - returns `mainnet`. The `create(...)` and `createWithContext(...)` functions are mocked to do nothing so they don't need to be called in the tests at all. Changes to the return values can be done through the functions of the `dataSourceMock` namespace in `matchstick-as` (version 0.3.0+).

Example below:

First we have the following event handler (which has been intentionally repurposed to showcase datasource mocking):

```
export function handleApproveTokenDestinations(event: ApproveTokenDestinations): void {  let tokenLockWallet = TokenLockWallet.load(dataSource.address().toHexString())!  if (dataSource.network() == 'rinkeby') {    tokenLockWallet.tokenDestinationsApproved = true  }  let context = dataSource.context()  if (context.get('contextVal')!.toI32() > 0) {    tokenLockWallet.setBigInt('tokensReleased', BigInt.fromI32(context.get('contextVal')!.toI32()))  }  tokenLockWallet.save()}
```

And then we have the test using one of the methods in the dataSourceMock namespace to set a new return value for all of the dataSource functions:

```
import { assert, test, newMockEvent, dataSourceMock } from 'matchstick-as/assembly/index'import { BigInt, DataSourceContext, Value } from '@graphprotocol/graph-ts'
import { handleApproveTokenDestinations } from '../../src/token-lock-wallet'import { ApproveTokenDestinations } from '../../generated/templates/GraphTokenLockWallet/GraphTokenLockWallet'import { TokenLockWallet } from '../../generated/schema'
test('Data source simple mocking example', () => {  let addressString = '0xA16081F360e3847006dB660bae1c6d1b2e17eC2A'  let address = Address.fromString(addressString)
  let wallet = new TokenLockWallet(address.toHexString())  wallet.save()  let context = new DataSourceContext()  context.set('contextVal', Value.fromI32(325))  dataSourceMock.setReturnValues(addressString, 'rinkeby', context)  let event = changetype<ApproveTokenDestinations>(newMockEvent())
  assert.assertTrue(!wallet.tokenDestinationsApproved)
  handleApproveTokenDestinations(event)
  wallet = TokenLockWallet.load(address.toHexString())!  assert.assertTrue(wallet.tokenDestinationsApproved)  assert.bigIntEquals(wallet.tokensReleased, BigInt.fromI32(325))
  dataSourceMock.resetValues()})
```

Notice that dataSourceMock.resetValues() is called at the end. That's because the values are remembered when they are changed and need to be reset if you want to go back to the default values.

### Test Coverage <a href="#test-coverage" id="test-coverage"></a>

Using **Matchstick**, subgraph developers are able to run a script that will calculate the test coverage of the written unit tests. The tool only works on **Linux** and **MacOS**, but when we add support for Docker (see progress on that [here](https://github.com/LimeChain/matchstick/issues/222)) users should be able to use it on any machine and almost any OS.

The test coverage tool is really simple - it takes the compiled test `wasm` binaries and converts them to `wat` files, which can then be easily inspected to see whether or not the handlers defined in `subgraph.yaml` have actually been called. Since code coverage (and testing as whole) is in very early stages in AssemblyScript and WebAssembly, **Matchstick** cannot check for branch coverage. Instead we rely on the assertion that if a given handler has been called, the event/function for it have been properly mocked.

#### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

To run the test coverage functionality provided in **Matchstick**, there are a few things you need to prepare beforehand:

**Export your handlers**

In order for **Matchstick** to check which handlers are being run, those handlers need to be exported from the **test file**. So for instance in our example, in our gravity.test.ts file we have the following handler being imported:

```
import { handleNewGravatar } from '../../src/gravity'
```

In order for that function to be visible (for it to be included in the `wat` file **by name**) we need to also export it, like this:

```
export { handleNewGravatar }
```

#### Usage <a href="#usage-2" id="usage-2"></a>

Once that's all set up, to run the test coverage tool, simply run:

```
graph test -- -c
```

You could also add a custom `coverage` command to your `package.json` file, like so:

```
"scripts": {    /.../    "coverage": "graph test -- -c"  },
```

Hopefully that should execute the coverage tool without any issues. You should see something like this in the terminal:

```
$ graph test -cSkipping download/install step because binary already exists at /Users/petko/work/demo-subgraph/node_modules/binary-install-raw/bin/0.4.0
___  ___      _       _         _   _      _|  \/  |     | |     | |       | | (_)    | || .  . | __ _| |_ ___| |__  ___| |_ _  ___| | __| |\/| |/ _` | __/ __| '_ \/ __| __| |/ __| |/ /| |  | | (_| | || (__| | | \__ \ |_| | (__|   <\_|  |_/\__,_|\__\___|_| |_|___/\__|_|\___|_|\_\
Compiling...
Running in coverage report mode. ️Reading generated test modules... 🔎️
Generating coverage report 📝
Handlers for source 'Gravity':Handler 'handleNewGravatar' is tested.Handler 'handleUpdatedGravatar' is not tested.Handler 'handleCreateGravatar' is tested.Test coverage: 66.7% (2/3 handlers).
Handlers for source 'GraphTokenLockWallet':Handler 'handleTokensReleased' is not tested.Handler 'handleTokensWithdrawn' is not tested.Handler 'handleTokensRevoked' is not tested.Handler 'handleManagerUpdated' is not tested.Handler 'handleApproveTokenDestinations' is not tested.Handler 'handleRevokeTokenDestinations' is not tested.Test coverage: 0.0% (0/6 handlers).
Global test coverage: 22.2% (2/9 handlers).
```

#### Test run time duration in the log output <a href="#test-run-time-duration-in-the-log-output" id="test-run-time-duration-in-the-log-output"></a>

The log output includes the test run duration. Here's an example:

`[Thu, 31 Mar 2022 13:54:54 +0300] Program executed in: 42.270ms.`

### Common compiler errors <a href="#common-compiler-errors" id="common-compiler-errors"></a>

> Critical: Could not create WasmInstance from valid module with context: unknown import: wasi\_snapshot\_preview1::fd\_write has not been defined

This means you have used `console.log` in your code, which is not supported by AssemblyScript. Please consider using the [Logging API](http://localhost:3000/en/developer/assemblyscript-api/#logging-api)

> ERROR TS2554: Expected ? arguments, but got ?.
>
> return new ethereum.Block(defaultAddressBytes, defaultAddressBytes, defaultAddressBytes, defaultAddress, defaultAddressBytes, defaultAddressBytes, defaultAddressBytes, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt);
>
> in \~lib/matchstick-as/assembly/defaults.ts(18,12)
>
> ERROR TS2554: Expected ? arguments, but got ?.
>
> return new ethereum.Transaction(defaultAddressBytes, defaultBigInt, defaultAddress, defaultAddress, defaultBigInt, defaultBigInt, defaultBigInt, defaultAddressBytes, defaultBigInt);
>
> in \~lib/matchstick-as/assembly/defaults.ts(24,12)

The mismatch in arguments is caused by mismatch in `graph-ts` and `matchstick-as`. The best way to fix issues like this one is to update everything to the latest released version.

### Feedback <a href="#feedback" id="feedback"></a>

If you have any questions, feedback, feature requests or just want to reach out, the best place would be The Graph Discord where we have a dedicated channel for Matchstick, called 🔥| unit-testing.
