# Metaprogramming

### Build Systems

- Build systems: encoded build commands in a tool that can do run them for you
    - Targets: things you want to build, e.g. building binaries, PDFs
    - Dependencies: things that need to be built for targets to be built
    - Rules: how to go from built dependencies to building target
- `make`: common built system, good for simple- to moderate-complexity projects
    - Looks in `Makefile`, where all targets, dependencies, and rules are defined
    - Will only run processes on aspects of build that have changed since previous build

### Dependency Management

- Dependencies
    - Can be projects themselves
    - Programs, system packages, or libraries within current coding language
    - Maintained in a repository, e.g. Ubuntu system packages via `apt`, PyPi, etc.
- Versioning: prevents new updates from breaking packages usability as a dependency
    - Semantic versioning: `major`.`minor`.`patch` convention, e.g. `8.1.7`
        - Patch: completely backwards compatible, no external change, e.g. security updates
        - Minor: backwards compatible, i.e. if a project expects an older minor version of dependency, newer ones still work; adds functionality
        - Major: non-backwards compatible, big changes
- When setting dependencies for your software, aiming for a lower minor/patch version is ideal, because it allows for greater flexibility for those who use it
- Lock files: lists versions currently used for each dependency
    - Makes sure you don’t accidentally update something
- Vendoring: moving all dependencies inside of project
    - Allows personal modifications and more control, but updates from upstream maintainers will need to be added manually if desired

### Continuous Integration

- Continuous integration (CI): stuff that runs whenever your code changes
    - e.g. changing documentation, uploading a compiled version, running a test suite, etc.
    - Services like GitHub Actions allow you to add a “recipe” file to repo that describes what to do, like running tests when code is pushed
- GitHub Pages updates the generated website every time you push

### Testing

- Test suite: collection of all tests
- Unit test: “micro” scale, testing specific feature in isolation
- Integration test: “macro” scale, runs large part of system to check if features are working together properly
- Regression test: replicating a previous bug scenario to ensure it is resolved, and that later changes don’t “regress” back to having a prior issue
- Mocking: replacing function, module, type, etc. with fake implementation to avoid testing unrelated functionality