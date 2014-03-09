# Install Dependencies

## Install

Copy `install-dependencies` script to your path.
Make sure PHP is installed.

## Usage

You define your dependencies in a file named `dependencies` at top of your
project. Listing files and third-party artifacts (with optional checksum).
The fragment part in the url can be added to point a subdirectory in the
release zip (eg a src/ folder).

Then run `install-dependencies`.

The artifacts are downloaded once and saved to `~/.install-dependencies` but
you can change the location with `env INSTALL_DEPENDENCIES_HOME`.

```bash
cat << 'END' > dependencies
# no .lock file, only fixed dependencies
library/Zend https://github.com/zendframework/zf1/archive/release-1.12.3.zip#library/Zend
# install any subdirectory from a zip archive
library/PHPThumb https://github.com/masterexploder/PHPThumb/archive/v1.0-final.zip#src
# no centeral registry, install from any file on the internet
public/js/jquery.js http://code.jquery.com/jquery-1.10.2.min.js 0511abe9863c2ea7084efa7e24d1d86c5b3974f1
END

install-dependencies
```
