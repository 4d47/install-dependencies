# Install Dependencies

## Install

Copy `install-dependencies` script to your path.
Make it executable and be sure PHP cli (yikes!) is installed.

## Usage

You define your dependencies in a file named `Dependencies` at top of your
project. Listing files and third-party artifacts (with an optional checksum).
The fragment part in the url can be added to point a subdirectory in an archive.

Then run `install-dependencies`.

The artifacts will be downloaded _once_, saved to `~/.install-dependencies` 
and linked in the projet. You can change the location using `env INSTALL_DEPENDENCIES_HOME`.

### Example

```bash
cat << 'END' > Dependencies

# Example file using old, unexciting dependencies.
# First notice there is no .lock file, no semver, only fixed dependencies.

library/Zend https://github.com/zendframework/zf1/archive/release-1.12.3.zip#library/Zend

# So yeah it is homemade TEXT format
# local-path url[#optional-subpath-if-url-is-an-archive] [optional-url-checksum]

library/PHPThumb https://github.com/masterexploder/PHPThumb/archive/v1.0-final.zip#src

# There is no centeral registry, accounts, registration, only the public Internet.
public/js/jquery.js http://code.jquery.com/jquery-1.10.2.min.js sha256-C6CB9UYIS9UJeqinPHWTHVqh/E1uhG5Twh+Y5qFQmYg=
END

install-dependencies
```
