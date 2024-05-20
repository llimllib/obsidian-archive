---
updated: '2024-03-12T15:15:06Z'
created: '2024-03-12T15:15:06Z'
---
I use [[ungoogled-chromium]] for debugging sometimes, and wanted to install the react developer tools. 

Unfortunately, the google chrome store arbitrarily restricts the ungoogled browser from installing normally via the extension store.

To fix it, the process was reasonably simple, via [the answer here](https://ungoogled-software.github.io/ungoogled-chromium-wiki/faq#can-i-install-extensions-or-themes-from-the-chrome-webstore):

1. Add a bookmark with this URL:
```javascript
javascript:location.href='https://clients2.google.com/service/update2/crx?response=redirect&acceptformat=crx2,crx3&prodversion='+(navigator.appVersion.match(/Chrome\/(\S+)/)[1])+'&x=id%'+'3D'+(document.querySelector('a[href^="https://chrome.google.com/webstore/report/"]').pathname.match(/[^\/]+\/*$/)[0])+'%'+'26installsource%'+'3Dondemand%'+'26uc';
```
2. Visit `chrome://flags/#extension-mime-request-handling`, set it to `Always prompt for install`
3. Visit an extension page ([example](https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)), and click the bookmarklet

That's it! the extension should now be installed.