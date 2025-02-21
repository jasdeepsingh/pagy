# CHANGELOG

## Version 5.0.0

### Breaking changes - 1. Code update

Pagy 4 dropped the compatibility for old ruby versions `>2.5` and started to refactor the code using more modern syntax and paradigms and better performance. It deprecated the legacy ones, printing deprecation warnings and upgrading instruction in the log, but still supporting its legacy API. Pagy 5.0.0 cleans up and removes all that transitional support code.

The changes for upgrading your app cannot be fixed with simple search and replace, but fear not! Fixing them should just take a few minutes with the following steps:

- Upgrade to the latest version of pagy 4
- Run your tests or app
- Check the log for any deprecations message starting with '[PAGY WARNING]'
- Update your code as indicated by the messages
- Ensure that the log is now free from warnings
- Upgrade to pagy 5

FYI: Here is the list of the deprecations that are not supported anymore:

#### Removed support for deprecated variables

- `Pagy::VARS[:anchor]` is now `Pagy::DEFAULT[:fragment]`

#### Removed support for deprecated arguments order

- The argument order in `pagy_url_for(page, pagy)` is now inverted: `pagy_url_for(pagy, page)`

#### Removed support for deprecated positional arguments

The following optional positional arguments are passed with keywords arguments in all the pagy helpers:

- The `id` html attribute string with the `pagy_id` keyword
- The `url|absolute` flag with the `absolute` keyword
- The `item_name` string with the `item_name` keyword
- The `extra|link_extra` string with the `link_extra` keyword
- The `text` string with the `text` keyword

### Breaking changes - 2. Simple search and replace

There are a few renaming that have not been deprecated in previous versions because they are extremely easy to fix with simple search and replace (while implementing deprecations would have been detrimental to performance and complex for no reason)

#### Consistency renaming

A few elements have been renamed: you code may or may not contain them. Just search and replace the following strings:

- Rename `Pagy::VARS` to `Pagy::DEFAULT`
- Rename `enable_items_extra` to `items_extra`
- Rename `enable_trim_extra` to `trim_extra`
- Rename `Pagy::Helpers` to `Pagy::UrlHelpers`
- Rename `pagy_get_params` to `pagy_massage_params`

#### Items accessor

The items accessor does not adjust for the actual items in the last page anymore. This should not affect normal usage, so you can ignore this change unless you build something on that assumption.

If your code is relying on the actual number of items **in** the page, then just replace `@pagy.items` with `@pagy.in` wherever you meant that.

FYI: The `@pagy.items` is now always equal to `@pagy.vars[:items]` (i.e. the requested items), while the `@pagy.in` returns the actual items in the page (which could be less than the `items` when the page is the last page)

### Changes

- Removed support for deprecations
- Refactoring of Pagy and Pagy::Countless classes, I18n, and url helpers
- Refactoring of the docker environment, addition of ready to use VSCode setup
- Changed general module structure (use of prepend instead of re-opening modules)
- Added gearbox extra for geared pagination
- Added configuration files for a full working VSCode devcontainer environment
- Added Run Configurations for RubyMine
- Improved the usage of e2e tests
- Updated doc, gemfiles and github workflow
- Other minor fixes and improvements in code and doc

## Version 5.0.1

### Changes 

- Added CHANGELOG_LEGACY
- Refactoring of exceptions
- Simplification of metadata extra
- Refactoring of coverage to include 100% of line and condition branches covered
- Added cypress-dark theme to e2e test
- Updated docs and issue templates

## Version 5.1.0

### Changes 

- Countless extra: simplified code, internal renaming of locals and docs update
- Improved code comments, formatting and docs fixes
- Fix and refactoring of pagy_url_for and relative test:
  - Fix for ignoring the params not coming from the request
  - Fix for ignoring the items_extra variable
  - Refactoring of Mock test classes for better handling of params

## Version 5.1.1

### Changes

- This reverts commit 1d77e672d5b7813108b40c13ca93fdec045f4c03.
  Generating the URL by using the application params method breakes rails apps because it requires manual changes in the apps.

## Version 5.1.2

### Changes

- Refactoring of pagy_url_for and relative test:
  - Fix for ignoring the items_extra variable
  - Replaced request.GET with request.params to enable POST pagination
  - Refactoring of Mock test classes for better handling of params

## Version 5.1.3

- A few details tag in the README should be opened by default
- Documentation improvements
- Fix for rails problem with internal params in pagy URL (closes #341)
- Small improvements in code and docs
- Added single action standalone rails_inline_output.rb

## Version 5.2.0

- Used gem-generic release-gem action
- Docker better mounts
- Updated npm modules and gemfiles
- Enabled rubocop Style/Documentation cop
- Added pagy_labeler frontend method overridable for changing the link text from a simple page number to any arbitrary string
- Implemented calendar extra to paginate a Time periods by unit (year, month, week or day)
- Small changes in code; updated gemfiles, tests and docs
  
## Version 5.2.1

- A few improvements for the Calendar pagination; added the current_page_label method
- Small refactoring of the overview extra
- Reorganization of mock collection classes; enabled rubocop layout in tests

## Version 5.2.2

- Calendar docs improvements and fixes
- Fix for missing defined?(Calendar) checks; small simplification in headers extra
  
## Version 5.2.3

- Refactoring of rails_inline_input.rb (include and close #342)
- docs: add tutorial, simplify header (#343)
- Fix for overflow :empty_page in regular Pagy instances, not returning an empty page

## Version 5.3.0

- Completed overflow fix for pagy Countless
- Added apps README
- Deprecated pagy_massage_params use the :params variable set to a Proc that does the same, but per instance
- Simplified page labelling, moved into the pagy classes and removed frontend methods
- Added support for *nav_js to Calendar
- Renamed internal module and files of SharedExtra to FrontendHelpers
- Implemented localization of time labels through the i18n extra delegation
