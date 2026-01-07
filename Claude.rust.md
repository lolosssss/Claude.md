# Rust

Language-specific instructions for Rust development.

## Package Management

### Cargo Commands
- `cargo build` - Compile the project
- `cargo build --release` - Compile with optimizations
- `cargo run` - Build and run src/main.rs or binary
- `cargo run --bin <name>` - Run specific binary
- `cargo check` - Quick compile check (no code generation)
- `cargo clean` - Clean build artifacts

### Dependencies
- `cargo add <crate>` - Add dependency (use `cargo-edit` if available)
- Manually edit `Cargo.toml` under `[dependencies]`
- `cargo update` - Update dependencies to latest compatible versions
- `cargo outdated` - Check for outdated dependencies (install cargo-outdated first)

## Common Commands

### Development
- `cargo run` - Run the project
- `cargo test` - Run all tests
- `cargo doc --open` - Generate and open documentation
- `cargo clippy` - Run the linter
- `cargo fmt` - Format code

### Type Checking
- `cargo check` - Fast type check without building
- `cargo check --tests` - Check tests too
- `cargo check --benches` - Check benches too

### Testing
- `cargo test` - Run all tests (unit and doc tests)
- `cargo test <test_name>` - Run specific test
- `cargo test --lib` - Run library tests only
- `cargo test --bins` - Run binary tests only
- `cargo test -- --nocapture` - Show print output
- `cargo test -- --ignored` - Run ignored tests
- `cargo test -- --test-threads=1` - Single-threaded tests

### Building & Release
- `cargo build --release` - Optimized build for production
- `cargo install --path .` - Install binary locally
- `cargo build --release --bin <name>` - Build specific binary

## Code Quality

### Clippy (Linter)
- `cargo clippy` - Run linter
- `cargo clippy --fix` - Auto-fix warnings
- `cargo clippy -- -W <warning>` - Treat warning as error
- `cargo clippy -- -D <warning>` - Deny specific warnings

### Formatting
- `cargo fmt` - Format all code
- `cargo fmt --check` - Check formatting without modifying
- `rustfmt <file>.rs` - Format specific file

### Documentation
- `cargo doc` - Generate documentation
- `cargo doc --open` - Generate and open in browser
- `cargo doc --no-deps` - Document only this crate
- Document public API with `///` (outer) or `//!` (inner)

## Rust Best Practices

### Ownership & Borrowing
- Understand ownership rules: one owner, move semantics
- Borrow with `&` for immutable references
- Borrow mutably with `&mut` (only one mutable reference at a time)
- Use `.clone()` sparingly (can be expensive)
- Prefer borrowing over cloning when possible
- Use `Copy` types for small, cheap-to-copy values

### Error Handling
- Use `Result<T, E>` for recoverable errors
- Use `Option<T>` for optional values
- Use `?` operator to propagate errors (not `unwrap()` or `expect()`)
- Use `unwrap()` or `expect()` only in tests or when truly infallible
- Create custom error types with `thiserror` crate
- Use `anyhow` for application-level error handling
- Use `map()` and `and_then()` / `?` for error chaining

### Async/Await
- Use `tokio` or `async-std` runtime
- Mark async functions with `async fn`
- Use `.await` to wait for futures
- Prefer `tokio::spawn` for concurrent tasks
- Use `tokio::join!` for waiting on multiple futures
- Be careful with blocking operations in async code

### Iterators
- Prefer iterator methods over loops (lazy, no allocation)
- Use `collect()` to consume iterators into collections
- Use `map()` for transformations
- Use `filter()` / `filter_map()` for filtering
- Use `find()` / `find_map()` for searching
- Use `fold()` / `reduce()` for accumulation
- Use `for_each()` for side effects (but prefer explicit loops)

### Concurrency
- Use threads with `std::thread::spawn`
- Use channels (`std::sync::mpsc`) for message passing
- Use `Arc<Mutex<T>>` or `Arc<RwLock<T>>` for shared state
- Prefer message passing over shared memory
- Use `Atomic*` types for lock-free synchronization

### Unsafe Rust
- Avoid `unsafe` unless absolutely necessary
- Document why `unsafe` is needed
- Keep `unsafe` blocks small and isolated
- Verify safety invariants manually
- Consider using safe wrappers or libraries instead

## File Conventions

### File Naming
- snake_case for files and directories
- `lib.rs` - Library entry point
- `main.rs` - Binary entry point
- `mod.rs` - Module entry point in directory
- `tests/` - Integration tests
- `benches/` - Benchmarks
- `examples/` - Example code

### Project Structure
```
project/
├── src/
│   ├── main.rs          # Binary entry point
│   ├── lib.rs           # Library entry point
│   └── modules/
├── tests/               # Integration tests
├── benches/             # Benchmarks
├── examples/            # Examples
├── Cargo.toml           # Manifest
└── README.md
```

### Module System
- Use `mod <name>;` to declare modules
- Use `use crate::<module>::<item>;` for imports
- Re-export with `pub use`
- Keep modules focused and small
- Use `pub(crate)` for crate-internal visibility

## Common Crates & Patterns

### Serialization
- `serde` - Serialization framework (add `derive` feature)
- `serde_json` - JSON support
- Derive `Serialize` and `Deserialize` traits

### Async Runtime
- `tokio` - Most common async runtime (use `features = ["full"]`)
- `async-std` - Alternative async runtime

### Web Frameworks
- `axum` - Modern web framework (tokio-based)
- `actix-web` - Actor-based framework
- `rocket` - Fast web framework

### Error Handling
- `thiserror` - Derive error types
- `anyhow` - Application error context
- `color-eyre` - Colored error reports

### Utilities
- `itertools` - Extra iterator methods
- `rayon` - Parallel iterators
- `regex` - Regular expressions
- `rand` - Random number generation
- `tracing` - Instrumentation and logging

## Testing Patterns

### Unit Tests
- Put tests in same file with `#[cfg(test)]` module
- Use `#[test]` attribute for test functions
- Use `assert_eq!`, `assert_ne!`, `assert!` macros
- Use `should_panic` for expected panics

### Integration Tests
- Put in `tests/` directory
- Import crate with `use <crate_name>;`
- Test public API only

### Property-Based Testing
- Use `quickcheck` or `proptest` crate
- Test invariants with random inputs

## Performance

### Profiling
- `cargo build --release` - Always profile release builds
- Use `cargo flamegraph` for flame graphs
- Use `cargo bench` for benchmarking
- Check `cargo-assembler` for assembly output

### Optimization Tips
- Use `#[inline]` for small, frequently called functions
- Use `Box<T>` to reduce stack size
- Use `Vec::with_capacity` when size is known
- Avoid allocations in hot loops
- Use `Cow<str>` / `Cow<[T]>` for conditional ownership
- Profile before optimizing

## Build Verification

Before completing work:
1. Fast check: `cargo check`
2. Format: `cargo fmt --check`
3. Lint: `cargo clippy -- -D warnings`
4. Test: `cargo test`
5. Build release: `cargo build --release` (if performance matters)
6. Fix any issues before committing

## Common Issues

### Borrow Checker
- Can't borrow mutable while immutable borrowed
- Solution: Restructure code, use clones sparingly, or use `Rc<RefCell<T>>`

### Lifetime Errors
- Solution: Annotate lifetimes explicitly with `'a`
- Use `'static` for static data only
- Consider restructing data to avoid complex lifetimes

### Send/Sync
- Use `Arc<T>` for shared ownership across threads
- Use `Mutex<T>` or `RwLock<T>` for interior mutability
- Implement `Send` / `Sync` manually only if safe

## When to Ask for Clarification

- Which async runtime to use (tokio vs async-std)
- Web framework choice (axum vs actix-web vs rocket)
- Error handling strategy (thiserror vs anyhow)
- Whether to use unsafe code
- Concurrency primitives (channels vs shared state)
- Target platform if cross-compiling
