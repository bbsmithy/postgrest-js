# `postgrest-js`

Fork with small change for switching out supabase request URL with and evervault relay.
For use in https://github.com/bbsmithy/supabase-js

```
useEvervault() {
  const isUsingEvervaultRelay =
    this.url.href.includes('relay') && this.url.href.includes('evervault')
  if (isUsingEvervaultRelay) {
    return this
  } else {
    const oldURL = this.url
    let replacementUrl = this._replaceAll(oldURL.host, '.', '-')
    replacementUrl = `${oldURL.protocol}//${replacementUrl}.relay.evervault.com${oldURL.pathname}${oldURL.search}`
    this.url = new URL(replacementUrl)
    return this
  }
}
```

[![Build](https://github.com/supabase/postgrest-js/workflows/CI/badge.svg)](https://github.com/supabase/postgrest-js/actions?query=branch%3Amaster)
[![Package](https://img.shields.io/npm/v/@supabase/postgrest-js)](https://www.npmjs.com/package/@supabase/postgrest-js)
[![License: MIT](https://img.shields.io/npm/l/@supabase/postgrest-js)](#license)

Isomorphic JavaScript client for [PostgREST](https://postgrest.org). The goal of this library is to make an "ORM-like" restful interface.

Full documentation can be found [here](https://supabase.github.io/postgrest-js/).

### Quick start

Install

```bash
npm install @supabase/postgrest-js
```

Usage

```js
import { PostgrestClient } from '@supabase/postgrest-js'

const REST_URL = 'http://localhost:3000'
const postgrest = new PostgrestClient(REST_URL)
```

- select(): https://supabase.io/docs/reference/javascript/select
- insert(): https://supabase.io/docs/reference/javascript/insert
- update(): https://supabase.io/docs/reference/javascript/update
- delete(): https://supabase.io/docs/reference/javascript/delete

#### Custom `fetch` implementation

`postgrest-js` uses the [`cross-fetch`](https://www.npmjs.com/package/cross-fetch) library to make HTTP requests, but an alternative `fetch` implementation can be provided as an option. This is most useful in environments where `cross-fetch` is not compatible, for instance Cloudflare Workers:

```js
import { PostgrestClient } from '@supabase/postgrest-js'

const REST_URL = 'http://localhost:3000'
const postgrest = new PostgrestClient(REST_URL, {
  fetch: (...args) => fetch(...args),
})
```

## License

This repo is licensed under MIT License.

## Sponsors

We are building the features of Firebase using enterprise-grade, open source products. We support existing communities wherever possible, and if the products don’t exist we build them and open source them ourselves. Thanks to these sponsors who are making the OSS ecosystem better for everyone.

[![New Sponsor](https://user-images.githubusercontent.com/10214025/90518111-e74bbb00-e198-11ea-8f88-c9e3c1aa4b5b.png)](https://github.com/sponsors/supabase)
