# Repository Secrets Configuration

This document describes the GitHub repository secrets required for CI/CD workflows.

## Required Secrets

### VSCE_PAT (VS Code Extension Publishing Token)

**Purpose:** Required to publish the extension to the Visual Studio Code Marketplace.

**How to create:**

1. Visit [Azure DevOps](https://dev.azure.com/)
2. Sign in with your Microsoft account
3. Click on your profile icon → **Security** → **Personal access tokens**
4. Click **New Token**
5. Configure the token:
   - **Name:** `VSCode Marketplace - vscode-hadolint`
   - **Organization:** All accessible organizations
   - **Expiration:** Custom defined (recommend 90 days and renew regularly)
   - **Scopes:** Select **Marketplace** → Check **Manage**
6. Click **Create**
7. Copy the token immediately (it won't be shown again)
8. Add to GitHub repository secrets:

   ```bash
   gh secret set VSCE_PAT --body "your-token-here"
   ```

**Documentation:** <https://code.visualstudio.com/api/working-with-extensions/publishing-extension#get-a-personal-access-token>

### OVSX_PAT (Open VSX Registry Token)

**Purpose:** Required to publish the extension to the Open VSX Registry (used by VS Codium and other editors).

**Status:** ✅ Already configured

**How to create (for reference):**

1. Visit [open-vsx.org](https://open-vsx.org/)
2. Sign in with GitHub
3. Go to your user settings
4. Click on **Access Tokens**
5. Generate a new token
6. Copy the token
7. Add to GitHub repository secrets:

   ```bash
   gh secret set OVSX_PAT --body "your-token-here"
   ```

**Documentation:** <https://github.com/eclipse/openvsx/wiki/Publishing-Extensions>

## Verification

To verify secrets are set correctly:

```bash
gh secret list
```

You should see:

- `OVSX_PAT` ✅
- `VSCE_PAT` (needs to be created)

## Usage in Workflows

These secrets are used in `.github/workflows/release.yml`:

```yaml
- name: Publish to VS Code Marketplace
  run: npx @vscode/vsce publish -p ${{ secrets.VSCE_PAT }}

- name: Publish to Open VSX Registry
  run: npx ovsx publish *.vsix -p ${{ secrets.OVSX_PAT }}
```

## Security Notes

- Never commit these tokens to the repository
- Rotate tokens regularly (recommend every 90 days)
- Use minimum required scopes
- If a token is compromised, immediately revoke it and generate a new one

## Manual Publishing (Alternative)

If you prefer not to use automated publishing, you can publish manually:

### VS Code Marketplace

```bash
# Login first (one time)
npx @vscode/vsce login TobiasHochguertel

# Package and publish
task package
npx @vscode/vsce publish
```

### Open VSX Registry

```bash
# Package first
task package

# Publish with token
npx ovsx publish *.vsix -p $OVSX_PAT
```

## Additional Resources

- [VS Code Extension Publishing Guide](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)
- [Open VSX Publishing Guide](https://github.com/eclipse/openvsx/wiki/Publishing-Extensions)
- [GitHub Actions Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)
