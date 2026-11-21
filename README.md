# Chmod KYC Web SDK

Compiled releases of the Chmod KYC Web SDK: document capture and face liveness in the browser.
Installing it needs no GitHub account or token.

## npm

```bash
npm install https://github.com/ChmodLab/chmod-kyc-sdk-web/releases/download/kyc-web-v1.0.0/chmodlab-kyc-web-1.0.0.tgz
```

```js
import { startVerification } from '@chmodlab/kyc-web';
import '@chmodlab/kyc-web/style.css';

const handle = startVerification({
  container: '#kyc',          // element or selector; the SDK fills it
  baseUrl: 'https://<api-id>.execute-api.us-east-1.amazonaws.com',
  sdkToken,                   // created by your backend with the transaction
  onResult: (result) => {     // { type: 'Completed' | 'Cancelled' | 'Failed', transactionId, code, message }
    handle.destroy();
  },
});
```

## Script tag

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/ChmodLab/chmod-kyc-sdk-web@main/kyc-web/1.0.0/chmod-kyc.css">
<script src="https://cdn.jsdelivr.net/gh/ChmodLab/chmod-kyc-sdk-web@main/kyc-web/1.0.0/chmod-kyc.iife.js"></script>
<script>
  ChmodKyc.startVerification({ container: '#kyc', baseUrl, sdkToken, onResult: console.log });
</script>
```

You can also download both files from the release and serve them from your own site.

## Requirements

- A phone or tablet browser (iOS, iPadOS or Android). On a computer the SDK ends with
  `DESKTOP_NOT_SUPPORTED`.
- HTTPS (or `localhost`), so the camera works.
- If your page has a Content-Security-Policy: `script-src 'wasm-unsafe-eval'`, `worker-src blob:`,
  `img-src blob: data:`, `media-src blob:`, `style-src 'unsafe-inline'`, and `connect-src` with the Chmod API,
  `https://*.amazonaws.com`, `wss://streaming-rekognition.us-east-1.amazonaws.com` and
  `https://cdn.liveness.rekognition.amazonaws.com`.

## Contents

| Folder | What it is |
|---|---|
| `kyc-web/<version>/` | The SDK: the `.tgz` for npm, and `chmod-kyc.iife.js` + `chmod-kyc.css` for a script tag. |
| `kyc-liveness-web/<version>/` | The liveness component bundled inside the SDK. You don't need to install it. |

The latest version is the newest `kyc-web-v*` release. Each version is published once and never
replaced. This repository is written by Chmod's release pipeline: don't edit it by hand.

## License

The SDK is proprietary: see [LICENSE](LICENSE). Only Chmod customers with a current agreement may use it.
`kyc-liveness-web` is derived from AWS Amplify UI under the Apache License 2.0; its license and notice are
inside its `.tgz`.
