# Contributing

This repository is maintained for collaborative development of the Drone EGO Swarming project.

## Branch workflow

Do not make experimental changes directly on `main`.

Create a separate branch for each focused change.

Examples:

```text
docs/installation-guide
docs/troubleshooting
fix/vehicle-status-topic
feature/multi-drone-launch
feature/search-pattern-planner
```

## Standard contribution process

1. Begin from the current `main` branch.
2. Create a descriptive branch.
3. Make one focused group of changes.
4. Commit each logical change with a descriptive message.
5. Open a pull request into `main`.
6. Describe what changed and why.
7. Request review from another team member when possible.
8. Address review comments.
9. Merge after approval and testing.
10. Delete the merged branch.

## Pull request requirements

Each pull request should explain:

- what changed,
- why the change was needed,
- which files were affected,
- how the change was tested,
- known limitations,
- and whether the documentation was updated.

## Documentation requirements

Update the documentation when any of these change:

- installation command,
- launch command,
- ROS topic name,
- ROS message version,
- source-file path,
- keyboard command,
- workspace layout,
- required dependency,
- expected terminal output,
- or troubleshooting procedure.

## Files that must not be committed

Do not upload:

- ROS 2 `build/`, `install/`, or `log/` directories,
- PX4 compiled build output,
- generated Gazebo caches,
- QGroundControl AppImages,
- ROS bag recordings unless specifically approved,
- passwords,
- access tokens,
- private keys,
- API credentials,
- or private machine configuration.

## Simulation requirement

Changes to the flight-control or planning path should be tested in simulation before being proposed for physical-vehicle use.
