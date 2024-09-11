Create an Nx Project
1. npx create-nx-workspace --pm yarn
2. Name the workspace
3. Select none for 'stack'
4. Select "Package-based monorepo"
5. Select "Do It Later"
6. Select "No" to remote caching

(In my case here, I also removed the .nx/workspace-data folder from the git ignore so I could trace changes)

Create a JS Lib
1. npx nx g @nx/js:lib mylib 
2. Select "None"
3. Select "None"
4. Select "As provided"

1. Run `yarn nx run-many -t lint`
2. This populates the local cache
3. Run `yarn nx run-many -t lint` again, result is cached
4. In Finder, delete `mylib/src/index.ts` and then hit `cmd+z` to undo
5. You will see that the `.nx/workspace-data/file-map.json` file changes significantly
6. Run `yarn nx run-many -t lint` again, result is NOT cached
7. Repeat the delete, undo and lint run, result is cached again
8. Now note that running `yarn nx reset` followed by the lint command will revert the changes that happened to the `.nx/workspace-data/file-map.json` in step 5
9. Subsequent deletes to not alter the `file-map.json` file now
