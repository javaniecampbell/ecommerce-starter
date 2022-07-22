## Netlify Identity Setup

### Setup

```javascript
yarn add react-netlify-identity react-netlify-identity-widget @reach/dialog @reach/tabs @reach/visually-hidden
```

Add provider to `gatsby-ssr.js`

```javascript
import React from "react";
import { IdentityContextProvider } from "react-netlify-identity-widget";
const url =
  process.env.REACT_APP_NETLIFY_IDENTITY_URL ||
  "https://ddow-ecommerce.netlify.app";
if (!url)
  throw new Error(`process.env.REACT_APP_NETLIFY_IDENTITY_URL is blank2`);
export const wrapRootElement = ({ element }) => {
  return <IdentityContextProvider url={url}>{element}</IdentityContextProvider>;
};
```

Add provider to `gatsby-browser.js`

```javascript
export { wrapRootElement } from "./gatsby-ssr";
```

Add Identity modal to `page.js`

```javascript
import React, { useState } from "react";
import { Link } from "gatsby";
// Step 1 - Adding Netlify Identity
import {
  IdentityModal,
  useIdentityContext,
} from "react-netlify-identity-widget";

import Layout from "../components/layout";
import Image from "../components/image";
import SEO from "../components/seo";

const IndexPage = () => {
  const identity = useIdentityContext();
  const [dialog, setDialog] = useState(false);
  return (
    <Layout>
      <SEO title="Login" />
      {identity && identity.isLoggedIn && (
        <pre>{JSON.stringify(identity, null, 2)}</pre>
      )}

      {!dialog && <button onClick={() => setDialog(true)}>Login</button>}
      <IdentityModal
        showDialog={dialog}
        onCloseDialog={() => setDialog(false)}
        onLogin={(user) => console.log(`Hello `, user?.user_metadata)}
        onSignup={(user) => console.log(`Hello `, user?.user_metadata)}
        onLogout={() => console.log("bye")}
      />
    </Layout>
  );
};

export default IndexPage;
```

```bash
git config user.email "1676496+javaniecampbell@users.noreply.github.com"
```

### References

https://github.com/sw-yx/gatsby-plugin-netlify-identity
