# Ruby

Language-specific instructions for Ruby development.

## Version Management

Detect the active Ruby version manager:
- `rbenv` → Check with `rbenv version`
- `rvm` → Check with `rvm current`
- `asdf` → Check with `asdf current ruby`
- `chruby` → Check with `ruby -v`

Set Ruby version if needed:
- `rbenv local 3.x.x` - Set per-project version
- `rvm use 3.x.x` - Set for current session

## Package Management

### Bundler
- `bundle install` - Install dependencies from Gemfile
- `bundle add <gem>` - Add gem to Gemfile and install
- `bundle update` - Update gems to latest versions
- `bundle exec <command>` - Run command in bundle context
- `bundle outdated` - Check for outdated gems

### Common Commands
- `ruby script.rb` - Run Ruby script
- `irb` - Interactive Ruby shell
- `pry` - Better IRB alternative (if installed)
- `rspec` - Run RSpec tests
- `rake -T` - List available Rake tasks

## Code Quality

### Linting & Formatting
- `rubocop` - Run linter
- `rubocop -a` / `rubocop --auto-correct` - Auto-fix issues
- `rubocop <file>` - Lint specific file
- `standardrb` - Alternative opinionated formatter (if used)
- `bundle exec rubocop` - Run within bundle context

### Type Checking (optional)
- `steep` - Type checker (if project uses RBS signatures)
- `sord` or `rbs-inline` - Generate type signatures

## Testing

### RSpec (most common)
- `rspec` - Run all tests
- `rspec <spec_file>` - Run specific spec file
- `rspec -f d` - Run with documentation format
- `rspec --only-failures` - Re-run only failed tests
- `rspec --seed <number>` - Run with specific random seed

### Minitest
- `rake test` - Run all tests
- `ruby test/<test_file>.rb` - Run specific test file

### Testing Patterns
- Use `describe` blocks for context
- Use `it` / `specify` for individual examples
- Use `before` / `after` hooks for setup/teardown
- Use `let` for lazy-evaluated test data
- Mock external dependencies with doubles

## Ruby Best Practices

### Naming Conventions
- snake_case for methods and variables
- PascalCase for classes and modules
- SCREAMING_SNAKE_CASE for constants
- `?` suffix for predicate methods (e.g., `valid?`)
- `!` suffix for mutating methods (e.g., `save!`)
- `to_` prefix for type conversion (e.g., `to_s`, `to_i`)

### Code Style
- Follow community style guide (rubocop default)
- Use `%w[]` / `%i[]` for word/symbol arrays
- Use `&:method` syntax for blocks (e.g., `map(&:to_s)`)
- Use double quotes for strings with interpolation
- Prefer `{ ... }` for single-line blocks, `do...end` for multi-line
- Use guard clauses for early returns
- Use safe navigation operator (`&.`) to avoid nil checks

### Metaprogramming
- Avoid metaprogramming when possible
- Use `define_method` over `eval`
- Prefer public APIs over monkey-patching
- Use modules and `prepend` for shared behavior

### Error Handling
- Use specific exception types
- Create custom exceptions for domain errors
- Always provide informative error messages
- Use `ensure` for cleanup
- Use exception tagging with `rescue => e` sparingly

### Performance
- Avoid string interpolation in loops (use frozen strings)
- Use `freeze` on constant strings/arrays
- Benchmark with `ruby -bm` or `benchmark` module
- Use `Enumerator` for lazy evaluation
- Be careful with object allocation in hot paths

## File Conventions

### File Naming
- snake_case for files (e.g., `user_service.rb`)
- `test_` prefix for test files (Minitest)
- `<name>_spec.rb` for RSpec specs
- `<name>.rb` for implementation files

### Project Structure
```
project/
├── lib/                  # Main source code
│   ├── <project_name>/
│   │   ├── version.rb
│   │   └── ...
│   └── <project_name>.rb
├── spec/ or test/        # Tests
│   ├── spec_helper.rb
│   └── ...
├── Gemfile               # Dependencies
├── Rakefile              # Tasks
├── README.md
└── <gem_name>.gemspec    # If building a gem
```

## Framework-Specific Notes

### Rails
- `rails server` / `rails s` - Start dev server
- `rails console` / `rails c` - Start console
- `rails generate <generator>` - Run generators
- `rails db:migrate` - Run migrations
- `rails db:rollback` - Rollback last migration
- `rails test` - Run all tests
- `rails test:system` - Run system tests
- `rails routes` - List routes
- Check `config/database.yml` for database config
- Use strong parameters for mass assignment protection
- Follow RESTful conventions for routes/controllers

### Sinatra
- `ruby app.rb` - Run app
- Check `config.ru` for Rackup configuration
- Use before/after filters for shared logic
- Keep routes organized in separate files

### Gems
- Build with `gem build <gem_name>.gemspec`
- Install locally with `gem install <gem_name>-<version>.gem`
- Use `bundler` for gem development
- Follow semantic versioning

## Build Verification

Before completing work:
1. Lint: `rubocop` or `bundle exec rubocop`
2. Fix auto-correctable issues: `rubocop -a`
3. Tests: `rspec` or `rake test`
4. Fix any failures before committing

## Security

- Never use `eval` with user input
- Sanitize input in Rails (`params.permit` or strong params)
- Keep gems updated: `bundle outdated`
- Use `bundler-audit` to check for vulnerabilities
- Use `brakeman` for Rails security scanning
- Never commit secrets (use `.env` or credentials system)

## Common Patterns

### Blocks & Procs
- Use blocks for DSL-like APIs
- Use `&block` to capture blocks as arguments
- Use `Proc.new` or `lambda` for reusable blocks
- Understand `return` behavior difference between proc/lambda

### Modules & Mixins
- Use modules for namespacing
- Use `extend` for class methods
- Use `include` for instance methods
- Use `prepend` to override module methods

### Enumerable Methods
- Prefer `map`/`select`/`reject` over loops
- Use `each` for side effects
- Use `reduce` / `inject` for accumulation
- Use `flat_map` for nested collections
- Leverage `lazy` for infinite chains

## When to Ask for Clarification

- Which web framework (Rails, Sinatra, Hanami, etc.)
- Test framework preference (RSpec vs Minitest)
- Ruby version if multiple are available
- Whether to use Sorbet/RBS for type checking
- Database ORM (ActiveRecord, Sequel, etc.)
