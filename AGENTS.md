# Repository Guidelines

## Project Structure & Module Organization
Core C++ entry points sit in the repo root: `black_hole.cpp` drives the 3D sim, `2D_lensing.cpp` renders the lightweight lensing view, and `CPU-geodesic.cpp` prototypes CPU tracing. Shaders (`geodesic.comp`, `grid.vert`, `grid.frag`) must match the uniform layout defined in `black_hole.cpp`. `CMakeLists.txt` and `vcpkg.json` handle builds and deps, while IDE helpers live under `vs_code/`. Generated binaries belong in `build/`; keep deliverables such as `black_hole.exe` outside version control.

## Build, Test, and Development Commands
Configure through vcpkg-aware CMake:  
`cmake -B build -S . -DCMAKE_TOOLCHAIN_FILE=$VCPKG_ROOT/scripts/buildsystems/vcpkg.cmake`  
Build targets: `cmake --build build` (add `--config Release` on Windows). Run the sim via `./build/black_hole`; launch the 2D sample with `./build/2D_lensing`. Regenerate compile commands for editors using `cmake -B build -S . -DCMAKE_EXPORT_COMPILE_COMMANDS=ON`.

## Coding Style & Naming Conventions
Stick to C++17, four-space indentation, and brace-on-same-line declarations. Favor explicit qualifiers (`glm::clamp`) and avoid `using namespace` in new files. Types stay PascalCase, functions and variables camelCase, GLSL uniforms snake_case to mirror shader conventions. Update host and shader structs together.

## Testing Guidelines
No automated suite ships yet. Validate manually by running the sim, toggling gravity with `G`, and exercising camera orbit and zoom. Capture before/after frame timings or screenshots whenever you touch rendering logic. If you add deterministic utilities, introduce lightweight tests under `tests/` and wire them into CMake for `ctest`.

## Commit & Pull Request Guidelines
Keep commits focused with imperative subjects (`Fix build for Ubuntu`). In PRs, summarize visual or performance impact, call out asset or shader updates, and list the commands reviewers should run. Link issues or references and mention minimum GPU/API expectations.

## Workflow & Collaboration
Use UV for any Python tooling; it creates per-project environments at `.venv`. Before starting feature work, confirm you are on a dedicated branch and create one if needed. Share a short plan for major efforts (new features, refactors) and wait for approval. Stay scoped to the requested task, aim for the simplest production-ready solution, and keep comments brief and purposeful. Manage project artifacts and docs in English, but communicate with stakeholders in Chinese or CN/EN mix as needed. When tackling long docs, propose an outline-first, iterative drafting process; proceed solo only if the requester opts out of collaboration.
