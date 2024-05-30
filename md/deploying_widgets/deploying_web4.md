## deploy to web4

(needs [bos-cli-rs](https://github.com/bos-cli-rs/bos-cli-rs))

![TEst](https://ipfs.near.social/ipfs/bafkreieema6nmzovnqoyd5nvfuvlwknhw3nlc7ahpqwa3wasj7vwpimdia)

1. create a subaccount

```cmd
near account create-account fund-myself web4.alice.near '1 NEAR' autogenerate-new-keypair save-to-keychain sign-as alice.near network-config mainnet sign-with-keychain send
```

2. deploy [minimum web4 contract](https://github.com/vgrichina/web4-min-contract)

```cmd
cd packages/web4-deploy/data

near contract deploy web4.alice.near use-file web4-min.wasm without-init-call network-config mainnet sign-with-keychain send
```

3. change default widgetSrc in `near-bos-webcomponent/src/App#24` and build

```cmd
cd near-bos-webcomponent
yarn build
```

4. export keys to use in web4 deploy of `dist`

```cmd
near account export-account web4.alice.near using-private-key network-config mainnet

NEAR_ENV=mainnet NEAR_SIGNER_KEY=${PRIVATE_KEY} npx web4-deploy dist web4.alice.near --nearfs
```

5. done, app deployed at alice.near.page

### TODO

- [ ] combine create-bos-app to bos-workspace init
- [ ] modify init to use zeeshan's template
- [ ] create-bos-app needs recent version of bos-workspace

### Breakdown

- /VM - What is the VM?
- /gateway - runs a local React App configured with the VM for displaying widgets served from /apps
- /apps - widgets to be served by bos-workspace, displayed on the gateway. The root account is "urbit.near" as configured in apps/urbit/bos.config.json. Nested paths in /widget will resolve to dot notation (e.g. urbit.near/widget/page.home). Your gateway will redirect references to prioritize the widgets from local.
  /packages - has bos-workspace and create-bos-app

### TODO

- [ ] convert gateway -> near-bos-webcomponent (we probably want a next.js gateway too, something connected to Tauri, Proximity bos-template Mike.near)
- [ ] import apps
- [ ] simple change in the VM that can signify if using local or not
- [ ] web4 contract
- [ ] .github/.workflows

```
everything
    apps
        every.near - default viewer, thing ability, browser, search
        devs.near - bos blocks, component library
        create.near - generic editor/creator/canvas
        apps.near - app creator and browser
        sdks.near - sdk creator browser for sdks
        maps.near - browser for maps
        embeds.near - feeds
        video.every.near
        nearbuilders.near - build dao gateway specific code
    gateway
        near-everything/viewer
        NearSocial/viewer
        nearbuilders/gateway
        create-next-app/starter
        near-bos-webcomponent
    VM
    packages/bos-workspace
```
