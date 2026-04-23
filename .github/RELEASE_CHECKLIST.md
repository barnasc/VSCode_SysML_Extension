# Release Checklist

## Before Release

1. Ensure `CHANGELOG.md` has entries under `## [Unreleased]`
   - Use subsections: `### Added`, `### Changed`, `### Deprecated`, `### Removed`, `### Fixed`, `### Security`
2. Ensure CI is green on `main`

## Creating the Release

1. Go to **Actions → Prepare Release** → **Run workflow**
2. Select the branch to release from (usually `main`)
3. Enter the version (e.g. `0.36.0`) — no `v` prefix
4. Optionally tick **Dry run** to validate without pushing
5. Click **Run workflow**

The [prepare-release workflow](../workflows/prepare-release.yml) will:

- Validate the version format and check the tag doesn't exist
- Run `npm run compile` and `npm run test:unit`
- Bump `package.json` version
- Stamp `CHANGELOG.md` (replace `[Unreleased]` with the version, add a fresh `[Unreleased]` section)
- Commit, tag `v<version>`, and push

The tag push then triggers the [release workflow](../workflows/release.yml), which will:

- Build and package the VSIX
- Extract release notes from `CHANGELOG.md`
- Create a GitHub Release with the notes and VSIX attached
- Publish to the VS Code Marketplace and Open VSX (if tokens are configured)

## After Release

- Verify the [GitHub Release](https://github.com/daltskin/VSCode_SysML_Extension/releases) looks correct
- Confirm the VSIX is downloadable
- Start adding entries under the new `## [Unreleased]` section in `CHANGELOG.md`
