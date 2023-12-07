## Prerequisites

```bash
# 1. install dependencies
npm i


# 2. build app
npm run build -w packages/svelte-kit-app
```

## Reproduce

In `packages/svelte-kit-app` we use the `packages/svelte-kit-library` in `src/routes/+page.svelte`. First use the module import in line 7.

```jsx
import { Heading } from "svelte-kit-library";
```

```bash
# build app
npm run build -w packages/svelte-kit-app

```

Now check the output `packages/svelte-kit-app/.svelte-kit`. If you search for `.unwanted` which is styling of the `Unwanted` component of `packages/svelte-kit-library` you realize that styling exists in the build result. However, we have not imported the component at any point in the project.  
Now change the import statement and use explicit import in line 10.

```jsx
import Heading from "svelte-kit-library/Heading.svelte";
```

```bash
# build app
npm run build -w packages/svelte-kit-app

```

Now the `.unwanted` class is no longer included in the build. It seems that the tree shaking does not work correctly at this point.

## Rebuild library

```bash
# 1. build library
npm run package -w packages/svelte-kit-library

# 2. pack library
npm pack -w packages/svelte-kit-library

# 3. install library
npm i svelte-kit-library-0.0.1.tgz -w packages/svelte-kit-app

```
