## Usage

Install [Now.app](https://zeit.co/app), setup the Now CLI and run this:

```bash
$ now -e SLACK_API_TOKEN="<token>" -e SLACK_SUBDOMAIN="<team-name>" rauchg/slackin
```

Other platforms:

- [Heroku](https://heroku.com/deploy?template=https://github.com/rauchg/slackin/tree/master)
- [Azure](https://azuredeploy.net/)
- [OpenShift](https://github.com/rauchg/slackin/wiki/OpenShift)
- [IBM Bluemix](https://bluemix.net/deploy?repository=https://github.com/rauchg/slackin)

### The Command

Install it and launch it on your server:

```bash
$ npm install -g slackin
$ slackin "your-team-id" "your-slack-token"
```

Your team id is what you use to access your login page on Slack (eg: https://**{this}**.slack.com).

You can find or generate your API test token at [api.slack.com/web](https://api.slack.com/web) – note that the user you use to generate the token must be an admin. You need to create a dedicated `@slackin-inviter` user (or similar), mark that user an admin, and use a test token from that dedicated admin user.  Note that test tokens have actual permissions so you do not need to create an OAuth 2 app. Also check out the Slack docs on [generating a test token](https://get.slack.help/hc/en-us/articles/215770388-Creating-and-regenerating-API-tokens).

**Important: if you use Slackin in single-channel mode, you'll only be
able to invite as many external accounts as paying members you have
times 5. If you are not getting invite emails, this might be the reason.
Workaround: sign up for a free org, and set up Slackin to point to it
(all channels will be visible).**

### Realtime Badge

[![](https://cldup.com/IaiPnDEAA6.gif)](http://slack.socket.io)

```html
<script async defer src="https://slack.yourdomain.com/slackin.js"></script>
```

or for the large version, append `?large`:

```html
<script async defer src="https://slack.yourdomain.com/slackin.js?large"></script>
```

### SVG

[![](https://cldup.com/jWUT4QFLnq.png)](http://slack.socket.io)

```html
<img src="https://slack.yourdomain.com/badge.svg">
```

Done in Markdown this looks like:

    [![Slack Status](https://slack.yourdomain.com/badge.svg)](https://yourdomain.com)

### Landing page

[![](https://cldup.com/WIbawiqp0Q.png)](http://slack.socket.io)

Point to `https://slack.yourdomain.com`.

**Note:** the image for the logo of the landing page
is retrieved from the Slack API. If your organization
doesn't have one configured, it won't be shown.

## API

Requiring `slackin` as a module will return
a `Function` that creates a `HTTP.Server` instance
that you can manipulate.

```js
require('slackin').default({
  token: 'yourtoken', // required
  interval: 1000,
  org: 'your-slack-subdomain', // required
  path: '/some/path/you/host/slackin/under/', // defaults to '/'
  channels: 'channel,channel,...', // for single channel mode
  silent: false // suppresses warnings
}).listen(3000);
```

This will show response times from Slack and how many
online users you have on the console.

By default logging is enabled.

The returned `http.Server` has an `app` property that is
the `express` application that you can define or override
routes on.

### JSON

All the metadata for your organization can be fetched
via a JSON HTTP request to `/data`.

If you wish to turn on CORS, pass `-x` or `--cors` to `slackin`.

## Developing

Slackin's server side code is written in ES6. It uses babel to transpile the
ES6 code to a format node understands. After cloning Slackin, you should
install the prerequisite node libraries with npm:

```bash
$ npm install
```

After the libraries install, the postinstall script will run `gulp` to invoke
babel on the source. It is important to run `gulp` manually after updating any
files in lib/ to update the versions in node/.

## Credits

- The SVG badge generation was taken from the
excellent [shields](https://github.com/badges/shields) project.
- The button CSS is based on
[github-buttons](https://github.com/mdo/github-buttons).