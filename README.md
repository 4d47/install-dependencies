
# The extra lightweight dependencies installer

You define your dependencies in a file named `dependencies.json` at top
of your project. This file is an object with properties defining the
folders that needs code and values pointing to
urls of third-party release artifacts.  The fragment part in the url
can added to point a subdirectory in the release (eg a src/ folder).

Then run `install-dependencies`.

The archives are downloaded only once and saved to
`~/.install-dependencies` but you can change
the location with `env INSTALL_DEPENDENCIES_HOME`.

Currently only zip releases are supported.

```bash
cat << 'JSON' > dependencies.json
{
  "library/Zend":
    "https://github.com/zendframework/zf1/archive/release-1.12.3.zip#library/Zend",
  "library/PHPThumb":
    "https://github.com/masterexploder/PHPThumb/archive/v1.0-final.zip#src",
  "modules/smoke-test":
    "https://bitbucket.org/mat/smoke-test/get/e519fae15059.zip#smoke-test"
}
JSON

install-dependencies
```