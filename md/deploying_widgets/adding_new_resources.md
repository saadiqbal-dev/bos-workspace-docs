## Adding new Resources

### Adding a main Route

the process of adding new resources/documentations is simple and quick.
To upload new resources we need the following

- the `.md` file uploaded to `github` and the `RAW file` URL
  just as given below:
  ![Raw File URL](https://ipfs.near.social/ipfs/bafkreicomtt6i4hnrjtxmmo35kdod3rph4jt6jsieslwqifotjfq2uenua)

The next step is to edit the `Index.jsx` file for `resources path`

1. add a new route to the Index file

```js
new_route: {
        path: "${alias_old}/widget/Resources",
        blockHeight: "final",
        label: "[ADD A LABEL IF YOU WANT TO CATEGORIZE IT]",
        init: {
          name: "[ADD A RESPECTIVE TITLE]",
          icon: "[ADD AN ICON]",
          mdPath:
            "[ADD THE MD PATH HERE]",
        },
      },
```

### Adding a sub Route (Tab) within a main Route

the steps are the same except the we need to add route to the existing main route:
To upload new resources we need the following

- the `.md` file uploaded to `github` and the `RAW file` URL
  just as given below:
  ![Raw File URL](https://ipfs.near.social/ipfs/bafkreicomtt6i4hnrjtxmmo35kdod3rph4jt6jsieslwqifotjfq2uenua)

The next step is to edit the `Index.jsx` file for `resources path`

```js
new_route: {
        path: "${alias_old}/widget/Resources",
        blockHeight: "final",
        label: "[ADD A LABEL IF YOU WANT TO CATEGORIZE IT]",
        init: {
          name: "[ADD A RESPECTIVE TITLE]",
          icon: "[ADD AN ICON]",
          mdPath:
            "[ADD THE MD PATH HERE]",
        },

        route: {
          new_sub_route: {
            init: {
              name: "[GIVE IT A NAME]"
            }
          }
        }
      },

      new_sub_route: {
        path: "${alias_old}/widget/Resources",
        blockHeight: "final",
        label: "[ADD A LABEL IF YOU WANT TO CATEGORIZE IT]",
        init: {
          name: "[ADD A RESPECTIVE TITLE]",
          icon: "[ADD AN ICON]",
          mdPath:
            "[ADD THE MD PATH HERE]",
        },
        hide: true,
      }
```
