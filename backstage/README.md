# [Backstage](https://backstage.io)

This is your newly scaffolded Backstage App, Good Luck!

To start the app, run:

```sh
yarn install
yarn dev
```

## Ingress Configuration

To access Backstage over ingress, let's say a domain like `backstage.dev-cluster.example.com`, following changes have 
to be done in `app-config.yaml`:
```
app:
  title: Scaffolded Backstage App
  baseUrl: http://backstage.dev-cluster.example.com:3000
  listen:
    host: 0.0.0.0

organization:
  name: My Company

backend:
  # Used for enabling authentication, secret is shared by all backend plugins
  # See https://backstage.io/docs/auth/service-to-service-auth for
  # information on the format
  # auth:
  #   keys:
  #     - secret: ${BACKEND_SECRET}
  baseUrl: http://backstage.dev-cluster.example.com:7007
  listen:
    port: 7007
    host: 0.0.0.0
    # Uncomment the following host directive to bind to specific interfaces
    # host: 127.0.0.1
  csp:
    connect-src: ["'self'", 'http:', 'https:']
    # Content-Security-Policy directives follow the Helmet format: https://helmetjs.github.io/#reference
    # Default Helmet Content-Security-Policy values can be removed by setting the key to false
  cors:
    origin: http://backstage.dev-cluster.example.com:3000
    methods: [GET, HEAD, PATCH, POST, PUT, DELETE]
    credentials: true
  # This is for local development only, it is not recommended to use this in production
  # The production database configuration is stored in app-config.production.yaml
  database:
    client: better-sqlite3
    connection: ':memory:'
  # workingDirectory: /tmp # Use this to configure a working directory for the scaffolder, defaults to the OS temp-dir
  ```

Once the ingress rules are created in the kubernetes cluster based on the ingress driver, the Backstage App can 
then be accessed over the browser at `http://backstage.dev-cluster.example.com:3000`.
