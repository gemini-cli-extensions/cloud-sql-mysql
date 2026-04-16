# Changelog

## [0.2.0](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.9...0.2.0) (2026-04-16)


### ⚠ BREAKING CHANGES

* add support for skills ([#111](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/111)) ([8da2132](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/8da213253d1acc7b69149ad88b02bff8627524f1))

### Features

* **skill:** Attach user agent metadata for generated skill ([mcp-toolbox#​2697](https://redirect.github.com/googleapis/mcp-toolbox/issues/2697)) ([9598a6a](https://redirect.github.com/googleapis/mcp-toolbox/commit/9598a6a32597b9c9abdb0f20c06d86a01b0d011f)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))
* **skill:** Update skill generation logic ([mcp-toolbox#​2646](https://redirect.github.com/googleapis/mcp-toolbox/issues/2646)) ([c233eee](https://redirect.github.com/googleapis/mcp-toolbox/commit/c233eee98cd9621526cb286245f3874f5bd6e7da)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))
* **skills:** Add Claude Code support to generated scripts ([mcp-toolbox#​2966](https://redirect.github.com/googleapis/mcp-toolbox/issues/2966)) ([a1609e1](https://redirect.github.com/googleapis/mcp-toolbox/commit/a1609e10a2eaf4ea68eae36acec3eed355b8a052)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))
* **skills:** Add codex user agent ([mcp-toolbox#​2973](https://redirect.github.com/googleapis/mcp-toolbox/issues/2973)) ([070e939](https://redirect.github.com/googleapis/mcp-toolbox/commit/070e9399c02f088d43175ce6bf343378beb7f584)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))
* **skills:** Tool invocation via npx ([mcp-toolbox#​2916](https://redirect.github.com/googleapis/mcp-toolbox/issues/2916)) ([377dc5b](https://redirect.github.com/googleapis/mcp-toolbox/commit/377dc5b00145a0044eef39314dd6b0ef5966fcd7)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))
* **tools/mysql:** Add list-table-stats-tool to list table statistics in MySQL and Cloud SQL MySQL source. ([mcp-toolbox#​2938](https://redirect.github.com/googleapis/mcp-toolbox/issues/2938)) ([dc2c2b4](https://redirect.github.com/googleapis/mcp-toolbox/commit/dc2c2b44e512e34d4d3a0b9c63b59374c37c4c4a)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))
* add claude code plugin config ([#113](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/113)) ([7a8c918](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/7a8c9181a69bf45e66be13014d53f2377a085f8b))
* add codex plugin config ([#114](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/114)) ([0d41575](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/0d41575abb5717f87349c95a16ccdbd7eabf5965))

### Bug Fixes

* **skill:** Fix env variable propagation ([mcp-toolbox#​2645](https://redirect.github.com/googleapis/mcp-toolbox/issues/2645)) ([5271368](https://redirect.github.com/googleapis/mcp-toolbox/commit/52713687208994c423da64333cb0a04fb483f794)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))
* **skills:** Fix integer parameter parsing through agent skills ([mcp-toolbox#​2847](https://redirect.github.com/googleapis/mcp-toolbox/issues/2847)) ([4564efe](https://redirect.github.com/googleapis/mcp-toolbox/commit/4564efe75436b4081d9f3d1f7c912bc64c13f850)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))
* **skills:** Fix skill generation template ([mcp-toolbox#​2914](https://redirect.github.com/googleapis/mcp-toolbox/issues/2914)) ([a01a15e](https://redirect.github.com/googleapis/mcp-toolbox/commit/a01a15ed1aa9a83eda8362578fed2e3a3c8dde99)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))
* **skills:** Prevent empty strings overriding optional env vars in node scripts ([mcp-toolbox#​2963](https://redirect.github.com/googleapis/mcp-toolbox/issues/2963)) ([c52adeb](https://redirect.github.com/googleapis/mcp-toolbox/commit/c52adeba76fc13d0e6e415f6393def0648e478d6)) ([3797d44](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3797d44030cb12e4502367ed9e34c849db8e3db5))


## [0.1.9](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.8...0.1.9) (2026-02-24)


### Bug Fixes

* remove broken keychain support for password ([#98](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/98)) ([0e0db45](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/0e0db45d816bd61bcd0065b773f307935544b565))

## [0.1.8](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.7...0.1.8) (2026-01-30)


### Features

* add Configuration settings ([#83](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/83)) ([36d4433](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/36d443385c94d188f16d33e36a156cb7a0215b23))
* **deps:** update dependency googleapis/mcp-toolbox to v0.26.0 ([#84](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/84)) ([306aaa9](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/306aaa9c39c0834528efd3728ee6f3056ef6ea5d))

## [0.1.7](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.6...0.1.7) (2026-01-09)


### Features

* **prebuilt/cloud-sql-mysql:** Update CSQL MySQL prebuilt tools to use IAM ([mcp-toolbox#​2202](https://redirect.github.com/googleapis/mcp-toolbox/issues/2202)) ([731a32e](https://redirect.github.com/googleapis/mcp-toolbox/commit/731a32e5360b4d6862d81fcb27d7127c655679a8)) ([186293e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/186293e1fcbe9bc576aeb360227e638c1df6d57a))
* **source/cloudsqlmysql:** Add support for IAM authentication in Cloud SQL MySQL source ([mcp-toolbox#​2050](https://redirect.github.com/googleapis/mcp-toolbox/issues/2050)) ([af3d3c5](https://redirect.github.com/googleapis/mcp-toolbox/commit/af3d3c52044bea17781b89ce4ab71ff0f874ac20)) ([186293e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/186293e1fcbe9bc576aeb360227e638c1df6d57a))
* **tools/mysql-get-query-plan:** Add new `mysql-get-query-plan` tool for MySQL source ([mcp-toolbox#​2123](https://redirect.github.com/googleapis/mcp-toolbox/issues/2123)) ([0641da0](https://redirect.github.com/googleapis/mcp-toolbox/commit/0641da0353857317113b2169e547ca69603ddfde)) ([186293e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/186293e1fcbe9bc576aeb360227e638c1df6d57a))


### Bug Fixes

* List tables tools null fix ([mcp-toolbox#​2107](https://redirect.github.com/googleapis/mcp-toolbox/issues/2107)) ([2b45266](https://redirect.github.com/googleapis/mcp-toolbox/commit/2b452665983154041d4cd0ed7d82532e4af682eb)) ([186293e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/186293e1fcbe9bc576aeb360227e638c1df6d57a))

## [0.1.6](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.5...0.1.6) (2025-12-08)


### Features

* **prebuilt/cloud-sql:** Add clone instance tool for cloud sql ([mcp-toolbox#​1845](https://redirect.github.com/googleapis/mcp-toolbox/issues/1845)) ([5e43630](https://redirect.github.com/googleapis/mcp-toolbox/commit/5e43630907aa2d7bc6818142483a33272eab060b)) ([438f03e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/438f03e135d5e76e7d58e2a0a560d4fbd1cacdac))

## [0.1.5](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.4...0.1.5) (2025-11-18)


### Features

* **source/alloydb, source/cloud-sql-postgres,source/cloud-sql-mysql,source/cloud-sql-mssql:** Use project from env for alloydb and cloud sql control plane tools ([mcp-toolbox#​1588](https://redirect.github.com/googleapis/mcp-toolbox/issues/1588)) ([12bdd95](https://redirect.github.com/googleapis/mcp-toolbox/commit/12bdd954597e49d3ec6b247cc104584c5a4d1943)) ([7f085eb](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/7f085eb47d12a8049318dd0ed28990ba293967a0))
* Added prompt support for toolbox ([mcp-toolbox#​1798](https://redirect.github.com/googleapis/mcp-toolbox/issues/1798)) ([cd56ea4](https://redirect.github.com/googleapis/mcp-toolbox/commit/cd56ea44fbdd149fcb92324e70ee36ac747635db)) ([7f085eb](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/7f085eb47d12a8049318dd0ed28990ba293967a0))

## [0.1.4](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.3...0.1.4) (2025-10-27)

### Bug Fixes

* **sources/mysql:** Escape mysql user agent ([#1707](https://redirect.github.com/googleapis/mcp-toolbox/issues/1707)) ([eeb694c](https://redirect.github.com/googleapis/mcp-toolbox/commit/eeb694c20facc40a38bfa67073c4cb1f3dd657ff)) ([05248f0](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/05248f0c43238ed98d7fa66031320624e86df9aa))
* **sources/mysql:** Escape program\_name for MySQL ([#1717](https://redirect.github.com/googleapis/mcp-toolbox/issues/1717)) ([02f7f8a](https://redirect.github.com/googleapis/mcp-toolbox/commit/02f7f8af979057efe99fd138cb1b958130355b68)) ([05248f0](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/05248f0c43238ed98d7fa66031320624e86df9aa))

## [0.1.3](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.2...0.1.3) (2025-10-17)


### Bug Fixes

* update context for install instructions ([#47](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/47)) ([3afaa60](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3afaa601ef8a55cd051563fb9833c0adce96032d))

## [0.1.2](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.1...0.1.2) (2025-10-13)


### Features

* add full table name to context file ([#34](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/34)) ([2e5337a](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/2e5337ab1aa1991104772fa6ecce94c3fc3931cb))
* **deps:** update dependency googleapis/mcp-toolbox to v0.17.0 ([#43](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/43)) ([382f390](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/382f390d75b0f97905e4dd03eb01561491d7bea9))

## [0.1.1](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.0...0.1.1) (2025-09-30)


### Features

* additional instructions for the context file ([#32](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/32)) ([bd680cb](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/bd680cb3c977f5941ba0370a3049e1615f308ae3))
* standardize mcp server names ([#30](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/30)) ([4d663a5](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/4d663a5701cc8ecd11d04acd0197cc46b3640b39))
* update context file to recommend observability extension ([#18](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/18)) ([80dcca7](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/80dcca71bf96c22fbb6e2d682e298f59cc14ba4b))

## 0.1.0 (2025-09-20)


### Feature

* Add Cloud SQL for MySQL Extension
