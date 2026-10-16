# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ShopStacc/tests/HomePageGuest.test.ts >> TC_HOME_036: Guest can browse, search and navigate categories without login
- Location: ShopStacc/tests/HomePageGuest.test.ts:5:5

# Error details

```
Error: Set SHOPSTACC_GUEST_HOME_URL to the direct BOBCARD storefront URL, not the SSO login URL
```

# Test source

```ts
  1  | import { test, expect } from '../../utils/testBase';
  2  | import { HomePage } from '../pages/HomePage';
  3  | 
  4  | // Separate file intentionally has no authenticated beforeEach hook.
  5  | test(
  6  |   'TC_HOME_036: Guest can browse, search and navigate categories without login',
  7  |   { tag: ['@bobcard', '@homepage', '@smoke', '@guest', '@sanity', '@functional'] },
  8  |   async ({ browser }, testInfo) => {
  9  |     const homepageUrl = process.env.SHOPSTACC_GUEST_HOME_URL;
  10 |     if (!homepageUrl) {
> 11 |       throw new Error('Set SHOPSTACC_GUEST_HOME_URL to the direct BOBCARD storefront URL, not the SSO login URL');
     |             ^ Error: Set SHOPSTACC_GUEST_HOME_URL to the direct BOBCARD storefront URL, not the SSO login URL
  12 |     }
  13 |     const context = await browser.newContext({
  14 |       ...testInfo.project.use,
  15 |       storageState: { cookies: [], origins: [] },
  16 |     });
  17 |     try {
  18 |       expect(await context.cookies()).toEqual([]);
  19 |       const page = await context.newPage();
  20 |       await test.step('Open homepage in a clean session and verify guest browsing', async () => {
  21 |         await HomePage.verifyGuestHomepage(page, homepageUrl);
  22 |       });
  23 |     } finally {
  24 |       await context.close();
  25 |     }
  26 |   }
  27 | );
  28 | 
```