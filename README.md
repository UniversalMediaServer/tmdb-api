## Running tests
You need the following environment variables in order to run all tests:
```
TMDB_API_KEY
TMDB_API_READ_TOKEN
TMDB_API_ACCESS_TOKEN
TMDB_USERNAME
TMDB_PASSWORD
TMDB_ACCOUNT
```

Most are easy to get via TMDB but `TMDB_API_ACCESS_TOKEN` is tricky. See https://github.com/UniversalMediaServer/UniversalMediaServer/pull/4037#issuecomment-2081531952 for instructions.

## Deployment

### Initial setup

In the Maven config file `settings.xml` you will need the encrypted versions of your credentials, which can be seen at https://oss.sonatype.org/#profile;User%20Token by clicking `Access User Token`. It will look like this:
```
<settings>
  ...
  <servers>
    <server>
      <id>ossrh</id>
      <username>USER_TOKEN_USERNAME</username>
      <password>USER_TOKEN_PASS</password>
    </server>
  </servers>
</settings>
```

#### Optional hints

You can use the `gpg.keyname` property in the Maven settings.xml to specify which GPG key to use to sign the files, as described at https://central.sonatype.org/publish/requirements/gpg/#listing-keys

On macOS you might need to symlink `gpg2` to `gpg` as described at https://stackoverflow.com/a/69920288/2049714

### Deploy

1. Run `mvn deploy -P release` to upload the release to staging.
1. Follow the instructions at https://central.sonatype.org/publish/release/#close-and-drop-or-release-your-staging-repository to "Close" and "Release". The terminology confuses me every time...
