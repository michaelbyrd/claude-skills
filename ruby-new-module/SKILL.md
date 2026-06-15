---
name: ruby-new-module
description: Use when creating a new Ruby module during a pair programming session or interview. Pass the module name as an argument (e.g. /ruby-new-module Greetable) to scaffold lib/greetable.rb and spec/greetable_spec.rb.
disable-model-invocation: true
---

# ruby-new-module

Scaffold a Ruby module and its RSpec spec file from a module name argument.

## Steps

1. Derive `snake_case` from the argument (e.g. `Greetable` → `greetable`)
2. Create `lib/snake_case.rb`
3. Create `spec/snake_case_spec.rb`
4. Create `spec/spec_helper.rb` **only if it does not already exist**

## Templates

Replace `ModuleName` with the argument and `snake_case` with the derived filename stem.

### `lib/snake_case.rb`

```ruby
module ModuleName
end
```

### `spec/snake_case_spec.rb`

```ruby
require 'spec_helper'
require_relative '../lib/snake_case'

RSpec.describe ModuleName do
  let(:including_class) do
    Class.new do
      include ModuleName
    end
  end

  subject { including_class.new }

  context 'when included' do
    it 'is included successfully' do
      expect(subject.class.ancestors).to include(ModuleName)
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
