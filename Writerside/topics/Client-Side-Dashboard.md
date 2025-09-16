# Client Side App

<video src="https://www.youtube.com/watch?v=tYCd0zxfYHE"></video>

The new client side app is under `clients` of your WGDashboard. If your WGD is in `https://wgd.com`, then client side app is in `https://wgd.com/client`

> **Not required, but strongly recommend**
> Setup [](Email-Service.md) so that your clients can receive service emails

## Usage

### Enable / Disable

By default, client side app is enabled, but if you don't need this feature, you can head to **Clients > Settings > Enable Client Side App** and toggle it off

### Sign In / Up

Currently, we offer 2 ways to sign in: **Email & Password** or **OIDC**

#### Sign In / Up Using Email & Password

If you have not signed up, click on the **Sign Up** button and follow the form, once you're done, click **Continue** button to finish.

To sign in, Simply enter the email password you signed up earlier, if your credentials are correct, you will be prompt to enter a **TOTP**. 

#### Sign In / Up Using OIDC

There is no need to sign up when using OIDC, WGDashboard will automatically sign up users when they first sign in with their OIDC provider

#### Configure OIDC

Currently, you will need to manually edit `wg-dashboard-oidc-providers.json` under `WGDashboard/src`

Once you opened, you should see something like this, with an example Object `Provider`:

```json
{
    "Client": {
        "Provider": {
            "client_id": "",
            "client_secret": "",
            "issuer": ""
        }
    }
}
```

To add a new OIDC provider, simply rename `Provider` to a name you want, then fill in the rest 3 required fields: `client_id`, `client_secret` and `issuer` 

For example, I'm using authentik and created a OIDC provider:

```json
{
    "Client": {
        "Provider": {
            "client_id": "1Iaesod8Cmqe660yxr3koyV1FxBnHGDjGR7fHlaw",
            "client_secret": "Xy6Lt9uYYLiurnK0UdjaEEdgmukiahFJ7jBXdxUzaWwvarG3JEdTxngQOs618yLCnegM4rYi1EyBSvMdkH2Dtwsu3B7qnaVQbOBoKFjlHIb0HLr0gAJ0SUnA4tP7vHq4",
            "issuer": "http://localhost:9000/application/o/wg-dashboard/"
        }
    }
}
```

> Don't forget to set your redirect URL correctly back to `http://wgd_host:port/client`

Then save the file and restart WGDashboard, and if your OIDC provider is valid, you should see an output when restarting WGD like this:

```
...
[Datetime] INFO in DashboardOIDC: Registered OIDC Provider: [Provider's Name]
...
```

and if you visit `http://wgd_host:port/client`, you should see a button on the sign in page to allow you to sign in with your provider.

## Manage Clients

You should see all signed up clients in the **Clients** page of WGDashboard. Click on the client's name and should be quite straight forward to setup your clients.

You can do the following:
1. Update Client's name
2. Assign Peers
   1. Click on the blue **Manage** button
   2. You should see a list of available peers popped up
   3. Click on the green **Plus** button next to each peer to assign it to the client
3. Unassign Peer
   1. Simply click on the red **Trash Bin** button to unassign
4. Delete Client
   1. If you delete a local clients, all information will get remove
   2. If you delete an OIDC client, all information will get remove, but it still able to sign back in unless you removed permission to access on the OIDC provider.

### Assign Peer to clients on Peers List

You can also assign clients on peers list. 

Simply click on the **3-dots** dropdown on each peer in a configuration, you should see a menu option **Assign Peer**. 

Then you can choose which client should have the access to this peer but clicking the green **Plus** button, or remove access by clicking the red **Trash Bin** button.