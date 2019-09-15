# npm-publish-git

Works, or should work, as `npm publish` does towards an npm registry,
except the target is the git repository itself.


## Install

```shell
npm install --save-dev git://github.com/andreineculau/npm-publish-git.git
```

## Usage

```shell
npm version patch
# tag v1.0.1 created

node_modules/.bin/npm-publish-git
# tag v1.0.1-src created, pointing to the v1.0.1 commit above
# tag v1.0.1 updated (=moved) to point to a commit that contains
#            only the artifacts sourced from the v1.0.1 commit above
```

Alternatively, you can publish to a tag of your choice, from any commit:

```shell
node_modules/.bin/npm-publish-git --tag latest
# tag latest created/updated to point to a commit that contains
#            only the artifacts sourced from the current commit
```

Now anyone that wants to use your package can turn their `package.json` into

```json
{
  "...": "...",
  "dependencies": {
    "example1": "git://github.com/user/example1.git#semver:^1.2.3",
    "example2": "git+ssh://git@git.intra/example2.git#commitish"
  },
  "...": "...",
}
```

meaning they can install your package via
`npm install git://github.com/user/example1.git#semver:^1.2.3`, etc.

**NOTE** the `semver:` pattern is only available since npm@5 .


## Raison d'être

In the world of binary artifacts, it may make sense to have a package manager.
But in the world of text artifacts?

Most of what gets published to NPM is not only just text,
but probably more or less the same as the source.

So with that in mind, why would you go through the trouble of:
- creating an NPM account
- publish artifacts on an NPM registry
- maybe even set up a local/mirror NPM registry
- give others in your team rights to publish updated artifacts
- etc. etc.

when you can leverage git dependencies in `package.json`
and you don't need any of the above overhead?

The only advantages of publishing to NPM are:
- caching - [track issue](https://github.com/zkat/pacote/issues/94)
- centralized uptime (read "if npm is down, the whole world is down, and everyone will work/wait for a fix";
  it is obviously a disadvantage otherwise)
- exposure
- usage statistics
- ?


## Comparison

In my initial search, I did not find any previous implementations that serve the purpose, but there are. In retrospect, `npm-publish-git` is still superior in stability, parity with npm and simplicity (a bash script treating git and npm as blackboxes). Don't trust me, I'm biased, verify for yourself.

* https://github.com/theoy/npm-git-publish (implemented via TypeScript, calling npm's JS APIs)
* https://github.com/finom/deploy-to-git (not npm specific, pushes a folder to a git repository)
* ?


## References

* https://glebbahmutov.com/blog/use-github-instead-of-npm/
* ?


## License

[Apache 2.0](LICENSE)
