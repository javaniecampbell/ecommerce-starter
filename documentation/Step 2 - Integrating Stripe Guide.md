## Stripe Integration Guide

1. Need to create a list of products that's not client side (i.e. database, a JSON file, etc)
2. Cannot trust data sent from the client, because it can be corrupted or tampered with.
3. Buy Button will trigger a Netlify Function, that will be called to get the price, etc.
4. The Function will then create a stripe checkout session
5. Return the session back to the client
6. Stripe JS redirects using the session to the Stripe Checkout Service

### Step 1: Install the packages and create `functions/`

#### Create directory

Make the `functions/` directory at the root of your client application

```bash
mkdir functions
```

Then initialize the `functions/` directory as follows:

```bash
npm init -y
```

OR

```bash
yarn init -y
```

Then install your packages in the `functions/` directory so that they manage it's own packages and reducing build errors at deployment:

```bash
npm install stripe node-fetch --prefix=functions
```

OR

```bash
yarn add stripe node-fetch --cwd functions
```
