---
name: ruby-init
description: Use when setting up a new Ruby project directory from scratch, especially at the start of a pair programming session or interview. Creates Gemfile, .rspec, lib/ and spec/ directories, then runs bundle install.
disable-model-invocation: true
---

# ruby-init

Initialize a Ruby project directory with RSpec, RuboCop, and Pry.

## Steps

Create each file below in the current working directory, then run `bundle install`.

### `Gemfile`

```ruby
source 'https://rubygems.org'

gem 'pry'
gem 'pry-byebug'
gem 'rspec'
gem 'rubocop'
```

### `.rspec`

```
--require spec_helper
```

### `spec/spec_helper.rb`

```ruby
$LOAD_PATH.unshift(File.join(File.dirname(__FILE__), '..', 'lib'))

require 'rspec'
require 'pry'
require 'pry-byebug'

RSpec.configure do |config|
  config.expect_with :rspec do |c|
    c.syntax = :expect
  end
end
```

### `.rubocop.yml`

```yaml
AllCops:
  NewCops: enable
  SuggestExtensions: false

# Disabled to preserve intentional visual alignment in constants
Layout/HashAlignment:
  Enabled: false

Layout/ExtraSpacing:
  Enabled: false

Layout/SpaceInsideArrayLiteralBrackets:
  Enabled: false

# POODR-style classes are self-documenting via naming; no class-level doc comments
Style/Documentation:
  Enabled: false

# Single-letter params are correct for coordinate methods (x, y)
Naming/MethodParameterName:
  Enabled: false

# RSpec describe/context blocks routinely exceed 25 lines — not a useful metric here
Metrics/BlockLength:
  Enabled: false

# Noise with no practical benefit at this scale
Style/FrozenStringLiteralComment:
  Enabled: false
```

### `CLAUDE.md`

Create `CLAUDE.md` with this content:

````
# Project Guidelines

## Ruby Design Principles (POODR)

All Ruby code in this project follows Sandi Metz's Practical Object-Oriented Design principles:

- **Single Responsibility** — every class and method has one reason to change; extract anything that needs a comment to explain what it does
- **Hide instance variables** — wrap all ivars with `attr_reader`; never reference `@var` directly outside its accessor, even internally
- **Dependency injection** — pass collaborators as constructor arguments; never instantiate dependencies inside a class
- **Tell, don't ask** — send messages to objects to trigger behavior; don't reach into their state and make decisions for them
- **Small, intention-revealing methods** — each method does one thing and is named after what it accomplishes, not how
- **Depend on behavior, not data** — objects communicate via messages (method calls), not by exposing raw data structures

## Code Quality

Before every commit, run:

```bash
bundle exec rubocop
bundle exec rspec
```

Both must be clean (0 offenses, 0 failures) before committing. Use `bundle exec rubocop -A` to autocorrect fixable violations. See `.rubocop.yml` for disabled cops and the reasoning behind each.
````

### Directories

```bash
mkdir -p lib spec
```

### After creating files

```bash
bundle install
```

Expected: Bundler installs pry, rspec, rubocop and their dependencies.
