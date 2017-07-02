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
- centralized uptime
- exposure
- usage statistics
- ?


## License

[Apache 2.0](LICENSE)
