---
name: ruby-new-file
description: Use when creating a new Ruby class during a pair programming session or interview. Pass the class name as an argument (e.g. /ruby-new-file FooBar) to scaffold lib/foo_bar.rb and spec/foo_bar_spec.rb.
disable-model-invocation: true
---

# ruby-new-file

Scaffold a Ruby class and its RSpec spec file from a class name argument.

## Steps

1. Derive `snake_case` from the argument (e.g. `FooBar` → `foo_bar`)
2. Create `lib/snake_case.rb`
3. Create `spec/snake_case_spec.rb`
4. Create `spec/spec_helper.rb` **only if it does not already exist**

## Templates

Replace `ClassName` with the argument and `snake_case` with the derived filename stem.

### `lib/snake_case.rb`

```ruby
class ClassName
  def initialize
  end
end
```

### `spec/snake_case_spec.rb`

```ruby
require 'spec_helper'
require_relative '../lib/snake_case'

RSpec.describe ClassName do
  subject(:snake_case) { described_class.new }

  describe '#initialize' do
    it 'creates a new instance' do
      expect(subject).to be_a(described_class)
    end
  end

  context 'when ' do
    it '' do
    end
  end
end
```

### `spec/spec_helper.rb` (only if missing)

```ruby
require 'rspec'

RSpec.configure do |config|
  config.expect_with :rspec do |c|
    c.syntax = :expect
  end
end
```
