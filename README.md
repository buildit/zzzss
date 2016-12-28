# zzzss

Sleepy styles.

## Usage

The consumable CSS is found in "dist/css/zzzss.css". You can pull this into your project in any number of ways. To see how I'm doing it in a React project, check out my [Style Guide](https://github.com/BillyZac/style-guide/). In that case, I'm using relying on Webpack to inject the CSS into the bundled Javascript.

## For ZZZSS developers
If you want to work on the ZZZSS library, here are some tips and guidelines.

### Deployment
We're using Jenkins to handle continuous deployment. See the Jenkinsfile. Right now, it's very basic. It pulls in the latest code and attempts to publish it to npm's registry.

The publish only happens on tagged commits. Use npm's 'version' command to do the version tags. Here's a sample workflow:

Do some work. Commit it:
```
git add .
git commit -m "Fix bug"
```

If this work is worthy of a version bump, [bump it](https://docs.npmjs.com/cli/version):
```
npm version patch -m "Fix bug"
```

We're using pre and post version hooks (see package.json) to validate and push the code to the remote repo.

The next time someone logs in to our Jenkins server and clicks "Build Now", Jenkins will publish the update to npm. Then any project that depends on Whippersnapper will be able to make use of the updated code.
