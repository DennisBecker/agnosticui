# Pagination

The `Pagination` component is typically used to _paginate_ large sets of data divided into smaller parts called _pages_.

<div class="mbs24"></div>

## Examples

<div class="mbe24"></div>

<PaginationExamples />

<script>
import PaginationExamples from '../../components/PaginationExamples.vue'
import { Alert } from "agnostic-vue";

export default {
  components: { Alert, PaginationExamples }
}
</script>

<div class="mbe32"></div>

## Usage

<div class="flex">
  <h3 id="react" tabindex="-1">
    <img src="/images/React-icon.svg" alt="react logo">React
  </h3>
</div>

```jsx
import { useEffect, useState } from 'react';
import 'agnostic-react/dist/common.min.css';
import 'agnostic-react/dist/esm/index.css';
import { Pagination } from 'agnostic-react';
import { usePagination } from "agnostic-helpers/dist/agnostic-helpers.esm";

export const YourComponent = () => {
  const [page, setPage] = useState(1);
  const paging = usePagination({ offset: 2 });
  // usePagination will generate your paging controls
  const pages = paging.generate(page, 20);

  useEffect(() => {
    // 1. `onPageChange` fires when a user clicks on a new page
    // 2. That calls `setPage` which `onPageChange` is pointed to
    // 3. `useEffect` here fires as we have the `page` dependency
    // listed in our dependencies array below
    // 4. We feed the new page into `paging.generate` and rerender
    paging.generate(page, 20);
  }, [page, pages, paging]);

  return (
    <section className="mbe24">
      <Pagination onPageChange={setPage} current={page} pages={pages} ariaLabel="Pagination to help navigate table" />
    </section>
  )
};
```

React: [component source](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-react/src/Pagination.tsx), [storybook tests](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-react/src/stories/Pagination.stories.tsx)

<div class="mbe32"></div>

<div class="flex">
  <h3 id="vue-3" tabindex="-1">
    <img src="/images/Vue-icon.svg" alt="Vue 3 logo">Vue 3
  </h3>
</div>

```vue
<script>
import "agnostic-vue/dist/common.min.css";
import "agnostic-vue/dist/index.css";
import { usePagingGenerator, Pagination } from "agnostic-vue";

export default {
  name: "PaginationExamples",
  components: {
    Pagination,
  },
  setup() {
    const { currentPaginationPage, paginationPages, handlePaginationUpdate } =
      usePagingGenerator(1, 1, 20);

    const interceptPageUpdate = (newPage) => {
      // Probably we'd make a fetch or update a table here
      console.log("interceptPageUpdate--page: ", newPage);
      // Will take care of the paging control update
      handlePaginationUpdate(newPage);
    };
    return {
      currentPaginationPage,
      paginationPages,
      interceptPageUpdate,
    };
  },
};
</script>
<template>
  <section>
    <h2>Pagination</h2>
    <Pagination
      @update-page="interceptPageUpdate"
      :current="currentPaginationPage"
      :pages="paginationPages"
    />
  </section>
</template>
```

Vue 3: [component source](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-vue/src/components/Table.vue), [storybook tests](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-vue/src/stories/Table.stories.js)

<div class="mbe24"></div>

<Alert type="warning">Note: Vue 2 is not supported</Alert>

<div class="mbe32"></div>

<div class="flex">
  <h3 id="angular" tabindex="-1">
    <img src="/images/Angular-icon.svg" alt="Angular logo">Angular
  </h3>
</div>

<p>COMING SOON!</p>

In your Angular configuration (likely `angular.json`) ensure you're including
the common AgnosticUI styles:

<div class="mbe16"></div>

` "styles": ["agnostic/dist/common.min.css"],`

<div class="mbe24"></div>

Add AgnosticUI's `AgModule` module:

```js{3,9}
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AgModule } from 'agnostic-angular';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, AgModule],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

Now you can use in your components:

```js
import { Component } from '@angular/core';

@Component({
  selector: 'your-component',
  template: ``
})
export class YourComponent {}
```

Angular: [component source](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-angular/libs/ag/src/lib/table.component.ts), [storybook tests](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-angular/libs/ag/src/lib/table.component.stories.ts)

<div class="mbe32"></div>

<div class="flex mbe16">
  <h3 id="svelte" tabindex="-1">
    <img src="/images/Svelte-icon.svg" alt="Svelte logo">Svelte
  </h3>
</div>

<div class="mbe12"></div>

<p>COMING SOON!</p>

```html
<script>
  import 'agnostic-svelte/dist/common.min.css';
  import { Pagination } from "agnostic-svelte";
</script>
```

Svelte: [component source](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-svelte/src/stories/Table.svelte), [storybook tests](https://github.com/AgnosticUI/agnosticui/blob/master/agnostic-svelte/src/stories/Table.stories.js)

## Storybook

You can run the framework Storybooks and see live examples for React, Vue 3, Angular, and Svelte. The following will set this up locally:

```shell
git clone git@github.com:AgnosticUI/agnosticui.git
cd agnosticui && yarn
# You can then run any of the top-level scripts:
yarn start:react # or
yarn start:vue # or
yarn start:angular # or
yarn start:svelte
```

See [Running monorepo](https://github.com/AgnosticUI/agnosticui/blob/master/CONTRIBUTING.md#running-monorepo).