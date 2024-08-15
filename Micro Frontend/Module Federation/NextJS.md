You don't necessarily need to create a separate server with Express unless you have specific requirements that can't be handled by the default Next.js server. Next.js should be able to serve the `remoteEntry.js` file from the `.next` directory without additional server setup.

Let's proceed with using the Next.js server itself. The key is to ensure the `remoteEntry.js` file is correctly generated and accessible via the `_next` path. Below is the refined configuration and steps to achieve this.

### Step-by-Step Guide Using the Next.js Server

#### Host Application (`app1`)

**`next.config.js`:**

```javascript
const ModuleFederationPlugin = require('webpack/lib/container/ModuleFederationPlugin');

module.exports = {
  webpack: (config, { isServer }) => {
    if (!isServer) {
      config.plugins.push(
        new ModuleFederationPlugin({
          name: 'app1',
          filename: 'static/chunks/remoteEntry.js',
          exposes: {
            './Component': './components/Component',
          },
          remotes: {
            app2: 'app2@http://localhost:3001/_next/static/chunks/remoteEntry.js',
          },
          shared: {},
        })
      );
    }
    return config;
  },
};
```

#### Remote Application (`app2`)

**`next.config.js`:**

```javascript
const ModuleFederationPlugin = require('webpack/lib/container/ModuleFederationPlugin');

module.exports = {
  webpack: (config, { isServer }) => {
    if (!isServer) {
      config.plugins.push(
        new ModuleFederationPlugin({
          name: 'app2',
          filename: 'static/chunks/remoteEntry.js',
          exposes: {
            './RemoteComponent': './components/RemoteComponent',
          },
          remotes: {},
          shared: {},
        })
      );
    }
    return config;
  },
};
```

### Example Components

#### Component in `app1` (`components/Component.js`):

```javascript
const Component = () => {
  return <div>Hello from App 1</div>;
};

export default Component;
```

#### Component in `app2` (`components/RemoteComponent.js`):

```javascript
const RemoteComponent = () => {
  return <div>Hello from App 2</div>;
};

export default RemoteComponent;
```

### Using Remote Component in `app1`

**`pages/index.js`:**

```javascript
import dynamic from 'next/dynamic';

// Dynamically import the remote component
const RemoteComponent = dynamic(() => import('app2/RemoteComponent'), { ssr: false });

export default function Home() {
  return (
    <div>
      <h1>Host Application (App 1)</h1>
      <RemoteComponent />
    </div>
  );
}
```

### Running Both Applications

#### Start `app1`:

```sh
npm run dev
```

#### Start `app2`:

```sh
PORT=3001 npm run dev
```

### Conclusion

By using the Next.js server, the `remoteEntry.js` file will be correctly placed and served from the `_next/static/chunks/` path. This ensures that the remote applications can access and use the shared modules without the need for a separate custom server. This approach leverages the built-in capabilities of Next.js for a streamlined setup.