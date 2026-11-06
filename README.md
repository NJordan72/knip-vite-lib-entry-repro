# knip: Vite `build.lib.entry` drops a production entry

`src/index.ts` is a production entry, because `package.json` `exports` names it. `vite.config.ts`
names the same file in `build.lib.entry`.

```sh
npm install
npx knip --production
```

Expected: no issues. `src/index.ts` re-exports `src/greet.ts`.

Actual on 6.44.0 and 6.44.1:

```
Unused files (1)
src/greet.ts
```

6.43.0 reports nothing (`npx knip@6.43.0 --production`).

If you change the entry in `vite.config.ts` to the relative `'src/index.ts'`, 6.42.1, 6.43.0 and
6.44.0 all report `src/greet.ts` as unused. Without `--production`, 6.43.0 and 6.44.0 report
nothing.
