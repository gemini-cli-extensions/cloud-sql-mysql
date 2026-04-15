You're a senior software engineer who's working to support skills in extensions for Google Data Cloud.

To support that create the following PRs in your repo. For each PR, first make the desired changes and then create a PR in the github repo. Please ensure that the PRs have good branch names as well as PR titles and descriptions. Directly create PRs in the repo. DO NOT CREATE ANY FORKS. All PRs should be created in a draft state.

# PR1: Add support for skills

1. Generate new skills using the latest toolbox binary (v1.1.0). Toolbox installation command:

```bash
export VERSION=1.1.0
curl -L -o toolbox2 https://storage.googleapis.com/mcp-toolbox-for-databases/v$VERSION/darwin/arm64/toolbox
chmod +x toolbox2
```

Then set the required env vars for configuration. You can
find those in the configuration section in the readme file. Eg. https://github.com/gemini-cli-extensions/alloydb?tab=readme-ov-file#configuration.

Command example to generate skills for a toolset:

```bash
./toolbox2 --prebuilt cloud-sql-postgres skills-generate --name "cloud-sql-postgres-health" --description "Use these skills when you need to audit database health, identify storage bloat, find invalid indexes, analyze table statistics, and manage maintenance configurations like autovacuum." --toolset=monitor  --license-header "// Copyright 2026 Google LLC
//
// Licensed under the Apache License, Version 2.0 (the \"License\");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//      http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an \"AS IS\" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License." --additional-notes="Note: The scripts automatically load the environment variables from various .env files. Do not ask the user to set vars unless skill executions fails due to env var absence." --additional-notes="Note: The scripts automatically load the environment variables from various .env files. Do not ask the user to set vars unless skill executions fails due to env var absence."
```

Write the commands for all tools in generate-skills-repo.sh script. Do not commit this file.

Remember to generate skills for all toolsets mentioned in https://github.com/googleapis/mcp-toolbox/tree/main/internal/prebuiltconfigs/tools for the source. Eg. AlloyDB Source: https://github.com/googleapis/mcp-toolbox/blob/main/internal/prebuiltconfigs/tools/alloydb-postgres.yaml.

Find list of sources and their tools grouping along with toolset descriptions [here](./db_groups.md).

After skills generation, cross check the generated skills from the [source yaml files](https://github.com/googleapis/mcp-toolbox/tree/main/internal/prebuiltconfigs/tools) and the [document](./db_groups.md) provided above.

Now, for all generated skills, replace skill descriptions from using tools -> skills.

2. Add skills validation workflow. Eg: https://github.com/gemini-cli-extensions/cloud-sql-postgresql/blob/main/.github/workflows/skills-validate.yml and https://github.com/gemini-cli-extensions/cloud-sql-postgresql/blob/main/.github/workflows/skills-validate-fallback.yml.

3. Remove the MCP servers from the gemini-extension.json file.

# PR2: Remove packaging workflow

1. Remove the github package and upload assets workflow: .github/workflows/package-and-upload-assets.yml.

# PR3: Add Claude code plugin config

1. Replicate this PR: https://github.com/gemini-cli-extensions/cloud-sql-postgresql/pull/137. Ensure that the plugin.json user config is consistent with the env vars in the gemini-extension.json file.

# PR4: Add Codex plugin config

1. Replicate this PR: https://github.com/gemini-cli-extensions/cloud-sql-postgresql/pull/138. Ensure that the system prompt you're using here is consistent with the gemini-extension context file.

# PR5: Auto update plugin versions using rp

1. Replicate this PR: https://github.com/gemini-cli-extensions/cloud-sql-postgresql/pull/155. Also ensure that "README.md" is present in extra-files section for release-please.

# PR6: Make skill docs changes:

1. Find the context file in gemini-extension.json, for eg. CLOUD-SQL-POSTGRESQL.md for the CLOUD SQL repo: https://github.com/gemini-cli-extensions/cloud-sql-postgresql and make changes analogous to what was done in https://github.com/gemini-cli-extensions/cloud-sql-postgresql/pull/109/.

2. Make changes to the README.md and DEVELOPER.md files. Use https://github.com/gemini-cli-extensions/cloud-sql-postgresql/blob/main/DEVELOPER.md and https://github.com/gemini-cli-extensions/cloud-sql-postgresql/blob/main/README.md on potential changes.

3. Check for any "tools" mention in the repository that needs to be updated to skills.

4. Ensure that you have covered updates on the README on how to use the extensions with Gemini CLI, Claude Code, Codex and Antigravity. Be very through with looking into this: https://github.com/gemini-cli-extensions/cloud-sql-postgresql/blob/main/README.md and making updates. Notice that this readme has a table of contents and collapsible sections for claude code etc.
