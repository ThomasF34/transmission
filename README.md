# @thomasf34/transmission

**This package is using a modified version of [@ctrl/transmission package](https://github.com/scttcper/transmission) that adds the possibility of adding torrent via magnet link or filename**

### Install

```console
npm install @thomasf34/transmission
```

### Changes
**Here are the changes compare to original package**

Here is how to add a Torrent via magnet link or filename

```ts
const data = await client.addTorrent(undefined, { 'filename': magnetLink });
console.log(data);
```

Otherwise, you can use the package as indicated in the original doc

---

# transmission [![npm](https://img.shields.io/npm/v/@ctrl/transmission.svg?maxAge=3600)](https://www.npmjs.com/package/@ctrl/transmission) [![CircleCI](https://circleci.com/gh/scttcper/transmission.svg?style=svg)](https://circleci.com/gh/scttcper/transmission) [![coverage status](https://codecov.io/gh/scttcper/transmission/branch/master/graph/badge.svg)](https://codecov.io/gh/scttcper/transmission)

> TypeScript api wrapper for [transmission](https://transmissionbt.com/) using [got](https://github.com/sindresorhus/got)

### Use

```ts
import { Transmission } from '@thomasf34/transmission';

const client = new Transmission({
  baseUrl: 'http://localhost:9091/',
  password: '',
});

async function main() {
  const res = await client.getAllData();
  console.log(res);
}
```

### Api

Docs: https://transmission.vercel.app
API Docs: https://github.com/transmission/transmission/blob/master/extras/rpc-spec.txt

### Normalized API
These functions have been normalized between torrent clients. Can easily support multiple torrent clients. See below for alternative supported torrent clients

##### getAllData
Returns all torrent data and an array of label objects. Data has been normalized and does not match the output of native `listTorrents()`.

```ts
const data = await client.getAllData();
console.log(data.torrents);
```

##### getTorrent
Returns one torrent data

```ts
const data = await client.getTorrent();
console.log(data);
```

##### pauseTorrent and resumeTorrent
Pause or resume a torrent

```ts
const paused = await client.pauseTorrent();
console.log(paused);
const resumed = await client.resumeTorrent();
console.log(resumed);
```

##### removeTorrent
Remove a torrent. Does not remove data on disk by default.

```ts
// does not remove data on disk
const result = await client.removeTorrent('torrent_id', false);
console.log(result);

// remove data on disk
const res = await client.removeTorrent('torrent_id', true);
console.log(res);
```

### See Also
All of the following npm modules provide the same normalized functions along with supporting the unique apis for each client.

* deluge - https://github.com/scttcper/deluge
* qbittorrent - https://github.com/scttcper/qbittorrent
* utorrent - https://github.com/scttcper/utorrent
