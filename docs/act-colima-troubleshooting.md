# Act (GitHub Actions Local Testing) - Colima Troubleshooting

## Issue Summary

When using `act` with Colima (Docker Desktop alternative for macOS), you may encounter two main issues:

### 1. Docker Socket Mount Error

```
Error: failed to start container: Error response from daemon: error while creating mount source path
'/Users/username/.colima/docker/docker.sock': mkdir: operation not supported
```

**Root Cause**: Act tries to bind mount the Docker socket as a directory instead of recognizing it as a socket file.

**Solution**: Use `--container-daemon-socket=-` flag (configured in `.actrc`)

### 2. Intermittent Docker Authentication Errors

```
Error response from daemon: authentication required - incorrect username or password
```

**Root Cause**: Colima's Docker authentication sometimes fails when pulling images, especially for `catthehacker/ubuntu:act-latest`.

**Solution**: Pre-pull images with correct platform and use `--pull=false` flag

## Fixed Configuration

### `.actrc` File

```
# Don't try to bind mount the Docker socket into containers
--container-daemon-socket=-

# Use linux/amd64 architecture for M-series Macs
--container-architecture=linux/amd64
```

### Taskfile Tasks

1. **Pre-pull images** (run once or when images are updated):

   ```bash
   task act:pull
   ```

2. **Run workflows locally**:
   ```bash
   task act:ci:lint    # Lint only
   task act:ci:test    # Tests only
   task act:ci         # Full CI workflow
   ```

The tasks automatically:

- Use `--pull=false` to avoid authentication issues
- Depend on `act:pull` to ensure images are cached
- Use `.actrc` configuration for Colima compatibility

## Manual Commands

If you need to run act manually:

```bash
# Pre-pull the image with correct platform
docker pull --platform linux/amd64 catthehacker/ubuntu:act-latest

# Run act with --pull=false
act --pull=false -j lint
```

## References

- GitHub Issue: https://github.com/nektos/act/issues/1051
- Colima Documentation: https://github.com/abiosoft/colima
- Act Documentation: https://github.com/nektos/act

## Current Status

✅ **Fixed** (as of act v0.2.84)

- Upgraded from v0.2.82 to v0.2.84
- Added `.actrc` configuration
- Updated Taskfile with `--pull=false` flag
- Pre-pull task to cache images with correct platform

The workflows now run successfully without Docker authentication or socket mount errors.
