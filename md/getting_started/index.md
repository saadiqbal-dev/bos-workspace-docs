# bos-workspace

🕰️ **Legacy `bos-workspace` users can use the [migration guide](https://github.com/NEARBuilders/bos-workspace/blob/main/MIGRATION_GUIDE.md) to upgrade or read the legacy documentation for v0.0.1-alpha.6 [here](https://github.com/NEARBuilders/bos-workspace/tree/version/0.0.1-alpha.6).**

🧰 `bos-workspace` is a comprehensive toolset designed to simplify the development and deployment of [NEAR components](https://docs.near.org/bos/tutorial/quickstart) and applications. With support for hot reload, TypeScript, and multiple app management, it caters to developers looking for an efficient and scalable development environment.

## Quickstart 🏃🏾

### Installation 🏗️

You can install `bos-workspace` globally on your machine or within your existing project workspace using npm (or other package manager):

global install:

```js
npm -g install bos-workspace
```

or navigate to your project directory and install:

```js
npm install bos-workspace
```

To verify `bos-workspace` in installed, you can check for a current version:

```js
bos - workspace - V;
```

![Verify `bos-workspace` version](https://ipfs.near.social/ipfs/bafkreicfg4xkejbblvcx25l4h7m33ldsghe5ktyut3crttqtb3ju4srinu)

To start, you may clone an existing project by navigating to your project directory and running the `clone` command:

```js
bos-workspace clone [accountId]
```

where `accountId ` is your named NEAR account (yourname.near)

![Cloned BOS Components](https://ipfs.near.social/ipfs/bafkreieema6nmzovnqoyd5nvfuvlwknhw3nlc7ahpqwa3wasj7vwpimdia)

In the terminal, navigate to the account name workspace, then run `bos-workspace-dev` to start the development server.

The image below is an example of what your terminal and browser should look like once you've opened the local gateway.

![Development Server Running](https://ipfs.near.social/ipfs/bafkreialqprya6kmcziz2n2ws4utp7yr5vt4k3ddazmxr4c54my42lqeum)

### Usage 👷🏽‍♀️

You can use your `bos-workspace` for both single and multi app development by taking advantage of the relationship between `Apps` and `Workspaces`

**App:** 🛠️

- belongs to an Account
- described by a `bos.config.json` where the content is:

```js
{
    "account": "app.near"
}
```

- path to code: `{projectId}/widget/*`
- cloning: `bos-workspace clone {accountId}` to create an App with `bos.config.json` set up and pull in all of the widgets from that `accountId`
  <br><br>

_Sample directory structure_

![Sample App Structure](https://ipfs.near.social/ipfs/bafkreifbfspi2oa74ueyfrtnhllwbgfqsjahd7l4jjpw4hdzne3f5bqq7i)
<br><br>

**Workspace:** 🛠️

- able to hold multiple Apps at the same time (similar to a monrepo)
- described by a `bos.workspace.json` where the content is:

```js
{
    "apps": ["/apps/*"]
}
```

<br>
*Sample directory structure*

![Sample Workspace Structure](https://ipfs.near.social/ipfs/bafkreieev4w5jaghtmhvif66oeyra4riabo7gd3t4katupqmxlqw7lwh74)

<br><br>

📝 **Note:** App names are not required to end in `.near` or be stored in a directory named `/apps`. Be sure your `bos.config.json` is located at the same level as directories like `/widget` and your `bos.workspace.json` reflects the name of the directory where your apps are located

### Commands 🤖

To see the list of commands, run `bw` or `bos-workspace`

📝 **Note:** `bos-workspace help [command]` will return additional information about any of the commands listed here

Usage: `bos-workspace [options] [command]`

Build decentralized apps

Options:

- `-V`, --version
- `-h`, --help

Commands:

### dev [options] [src] - Run the development server

Usage: `bos-workspace dev [options] [src]`

Arguments:

- `src`: Path to the app source code (default: ".")

Options:

- `-p, --port <port>`: Port to run the server on (default: "8080")
- `-g, --gateway <gateway>`: Path to custom gateway dist
- `--no-gateway`: Disable the gateway
- `--no-hot`: Disable hot reloading
- `--no-open`: Disable opening the browser
- `-h, --help`: Display help for command

---

### build [options] [src] [dest] - Build the project

Usage: `bos-workspace build [options] [src] [dest]`

Arguments:

- `src`: Path to the app source code (default: ".")
- `dest`: Destination path

Options:

- `-n, --network <network>`: Network
- `-l, --loglevel <loglevel>`: Log level (ERROR, WARN, INFO, DEV, BUILD, DEBUG) (default: "BUILD")
- `-h, --help`: Display help for command

---

### workspace|ws [options] [command] [src] [dest] - Work with multiple apps

Usage: `workspace|ws [options] [command] [src] [dest]`

Arguments:

- `command`: Command to run
- `src`: Path to the workspace (default: ".")
- `dest`: Destination path

Options:

- `-n, --network <network>`: Network
- `-l, --loglevel <loglevel>`: Log level (ERROR, WARN, INFO, DEV, BUILD, DEBUG) (default: "BUILD")
- `-p, --port <port>`: Port to run the server on (default: "8080")
- `-g, --gateway <gateway>`: Path to custom gateway dist
- `--no-gateway`: Disable the gateway
- `--no-hot`: Disable hot reloading
- `--no-open`: Disable opening the browser
- `-h, --help`: Display help for command

---

### init [options] [path] - Initialize a new project

Usage: `bos-workspace init [options] [path]`

Arguments:

- `path`: Where to init the project

Options:

- `-t, --template <template>`: Template to use (js-single, js-multi) (default: "js-single")
- `-h, --help`: Display help for command

---

### clone [account] [dest] - Clone a SocialDB repository

Usage: `bos-workspace clone [account] [dest]`

Arguments:

- `account`: Account ID
- `dest`: Destination path

Options:

- `-h, --help`: Display help for command

---

### pull [account] - Pull updates from a SocialDB repository

Usage: `bos-workspace pull [account]`

Arguments:

- `account`: Account ID

Options:

- `-h, --help`: Display help for command
