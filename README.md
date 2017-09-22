This is a test repo to reproduce a problem I am having with npm.  I am using npm 5.4.2.

The problem is: I have the following package.json:

```json
{
  "name": "npm-update-test",
  "version": "0.1.0",
  "private": true,
  "repository": "https://github.com/matatk/npm-update-test.git",
  "devDependencies": {
    "eslint": "~4.7"
  }
}
```

I have ESLint 4.7.1 installed, as per `package-lock.json`.

If I run

    npm outdated

It tells me the latest available (and wanted) version is 4.7.2.

I expect that when I run

    npm update

it will install ESLint 4.7.2 and update `package-lock.json` accordingly.

However, what happens is this:

- It does install ESLint 4.7.2 as expected, but
- it also changes the `devDependencies` section of `package.json` as follows

```json
. . .
  "devDependencies": {
    "eslint": "^4.7.2"
  }
. . .
```

This has changed the version range that I wanted from "4.7.x" to "4.x", as well as unexpectedly overwriting `package.json`, which feels like a bug to me.

Note: if I run `npm help update` it says that I should have to pass the `--save` switch if I want it to update `package.json` but it overwrites `package.json` regardless.
