---
title: Introduction & Usage
description: DSL for defining initializer params and options
layout: gem-single
order: 8
type: gem
name: dry-initializer
sections:
  - container-version
  - params-and-options
  - options-tolerance
  - optionals-and-defaults
  - type-constraints
  - readers
  - inheritance
  - rails-support
  - custom-plugins
---

`dry-initializer` is a simple mixin of class methods `params` and `options` for instances.

## Synopsis

```ruby
require 'dry-initializer'

class User
  extend Dry::Initializer::Mixin

  param  :name,  type: String
  param  :role,  default: proc { 'customer' }
  option :admin, default: proc { false }
end

user = User.new 'Vladimir', 'admin', admin: true

user.name  # => 'Vladimir'
user.role  # => 'admin'
user.admin # => true
```

This is pretty the same as the following ruby code:

```ruby
class User
  attr_reader :name, :role, :admin

  def initialize(name, role = 'customer', admin: false)
    @name  = name
    @role  = role
    @admin = admin

    fail TypeError unless String === @name
  end
end
```
