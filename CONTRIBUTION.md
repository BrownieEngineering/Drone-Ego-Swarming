# Contributing

Thank you for contributing or referencing the Drone EGO Swarming project.


---

# Branch Workflow

Do **not** develop directly on `main`.

Instead:

1. Create a branch from `main`
2. Make one focused change
3. Commit your work
4. Open a Pull Request
5. Merge into `main`

Example branch names:

```
docs/installation
docs/troubleshooting
feature/multi-drone
feature/search-algorithm
fix/vehicle-status-v4
```

---

# Pull Requests

Every Pull Request should explain:

- What changed
- Why it changed
- Which files changed
- How it was tested
- Any known limitations

---

# Documentation

Whenever code changes, documentation should also be updated.

Examples include:

- launch commands
- ROS topics
- message versions
- build commands
- setup procedures
- troubleshooting steps

---

# Files NOT to Upload

Do not commit:

- build/
- install/
- log/
- PX4 build directories
- Gazebo cache folders
- QGroundControl AppImages
- passwords
- tokens
- private keys
- API credentials

---

# Simulation First

All flight-control modifications should be validated in simulation before being considered for physical hardware.
