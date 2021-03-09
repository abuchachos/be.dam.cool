# be.dam.cool 
[![Netlify Status](https://api.netlify.com/api/v1/badges/eb21c0dd-9387-4850-9520-f373c6f954d4/deploy-status)](https://app.netlify.com/sites/be-dam-cool/deploys)
> A URL shortener for my personal links.


## Redirects
All the redirect URLs are maintained in [`redirects.csv`](redirects.csv), which is fetched by the client [`script.js`](script.js) each time someone visits the site. There is no dynamic content as everything is done by the client-side. Alternatively, and if Netlify is set up, then a `_redirects` file can be used to create server-side redirects which improve SEO and are faster.

> Note: server-side redirects only support `http` and `https` protocols. `mailto` links will fallback on `redirects.csv`

## Usage
Redirects can be added or removed by opening a new issue on GitHub. Creating a new issue runs [`update_redirects.py`](update_redirects.py), which modifies `redirects.csv` and `_redirects`.

### Add URL
In order to add a redirect, the issue must be created by the user specified in `config.js`, be titled "Add URL", and have the <kbd>update redirects</kbd> label. The issue body needs to follow this syntax:

```
Short URL --> Long URL
```

### Remove URL
In order to remove a redirect, the issue must be created by the user specified in `config.js`, be titled "Remove URL", and have the <kbd>update redirects</kbd> label. The issue body should contain the short URL to remove.

## Modify
If you'd like to create your own URL shortener, fork this repo, modify [`config.js`](config.js), the meta redirect in [`index.html`](https://github.com/paramt/go.param.me/blob/master/index.html#L6), and the domain name in [`CNAME`](CNAME). Remember to delete the existing redirects too!

### `config.js`
| Option | Description | Type | Example |
| --- | --- | --- | --- |
| `shortDomain` | The short domain that will redirect to other URLs | `str` | `"be.dam.cool"` |
| `defaultRedirect` | The default redirect in case a link that does not exist is requested | `str` | `"https://be.dam.cool"` |
| `repo` | The GitHub repo where `redirects.csv` is located | `str` | `"abuchachos/be.dam.cool"` |
| `users` | The list of GitHub users that are allowed to modify the list of redirects by opening an issue | `str[]` | `["abuchachos"]` |
| `netlify_redirects` | Whether or not the script should generate a `_redirects` file (used by Netlify's server-side redirects) | `bool` | `true` |
| `utm` | Whether or not a UTM code should be appended to the URL when redirecting. *Note: this does not work if server-side redirects are being used*| `bool` | `false` |

## License
The repo is licensed under the [MIT License](LICENSE), so you may use and modify the code in any way as long as the copyright and license notices are kept.
