## @code-fighter/supabase-management-js

A convenience wrapper for the [Supabase Management API](https://supabase.com/docs/reference/api/introduction) written in TypeScript.

Fork of [supabase-community/supabase-management-js](https://github.com/supabase-community/supabase-management-js) for use with Code Fighter.

### Installation

To install `@code-fighter/supabase-management-js` in a Node.js project:

```sh
npm install @code-fighter/supabase-management-js
```

`@code-fighter/supabase-management-js` requires Node.js 18 and above because it relies on the native `fetch` client.

### Authentication

You can configure the `SupabaseManagementAPI` class with an access token, retrieved either through [OAuth](https://supabase.com/docs/guides/integrations/oauth-apps/authorize-an-oauth-app) or by generating an API token in your [account](https://supabase.com/dashboard/account/tokens) page. Your API tokens carry the same privileges as your user account, so be sure to keep it secret.

```ts
import { SupabaseManagementAPI } from "@code-fighter/supabase-management-js";

const client = new SupabaseManagementAPI({ accessToken: "<access token>" });
```

### Usage

The `SupabaseManagementAPI` class exposes each API endpoint of the [Management API](https://supabase.com/docs/reference/api/introduction) as a function that returns a Promise with the corresponding response data type.

```ts
import { SupabaseManagementAPI } from "@code-fighter/supabase-management-js";

const client = new SupabaseManagementAPI({ accessToken: "<access token>" });

const projects = await client.getProjects();

if (projects) {
  console.log(`Found ${projects.length} projects`);
}
```

### Handling errors

Response errors are thrown as an instance of `SupabaseManagementAPIError` which is a subclass of `Error`. You can use the exported `isSupabaseError` guard function to narrow the type of an `unknown` error object:

```ts
import { SupabaseManagementAPI, isSupabaseError } from "@code-fighter/supabase-management-js";

const client = new SupabaseManagementAPI({ accessToken: "<access token>" });

try {
  await client.getProjects();
} catch (error) {
  if (isSupabaseError(error)) {
    // error is now typed as SupabaseManagementAPI
    console.log(
      `Supabase Error:  ${error.message}, response status: ${error.response.status}`
    );
  }
}
```

### Building

```sh
npm install
npm run build
```

### Publishing to npm

```sh
npm login
npm publish --access public
```
