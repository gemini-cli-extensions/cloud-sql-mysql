# Changelog

## [0.1.8](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.7...0.1.8) (2026-01-30)


### Features

* add Configuration settings ([#83](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/83)) ([36d4433](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/36d443385c94d188f16d33e36a156cb7a0215b23))
* **deps:** update dependency googleapis/genai-toolbox to v0.26.0 ([#84](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/84)) ([306aaa9](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/306aaa9c39c0834528efd3728ee6f3056ef6ea5d))

## [0.1.7](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.6...0.1.7) (2026-01-09)


### Features

* **prebuilt/cloud-sql-mysql:** Update CSQL MySQL prebuilt tools to use IAM ([genai-toolbox#​2202](https://redirect.github.com/googleapis/genai-toolbox/issues/2202)) ([731a32e](https://redirect.github.com/googleapis/genai-toolbox/commit/731a32e5360b4d6862d81fcb27d7127c655679a8)) ([186293e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/186293e1fcbe9bc576aeb360227e638c1df6d57a))
* **source/cloudsqlmysql:** Add support for IAM authentication in Cloud SQL MySQL source ([genai-toolbox#​2050](https://redirect.github.com/googleapis/genai-toolbox/issues/2050)) ([af3d3c5](https://redirect.github.com/googleapis/genai-toolbox/commit/af3d3c52044bea17781b89ce4ab71ff0f874ac20)) ([186293e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/186293e1fcbe9bc576aeb360227e638c1df6d57a))
* **tools/mysql-get-query-plan:** Add new `mysql-get-query-plan` tool for MySQL source ([genai-toolbox#​2123](https://redirect.github.com/googleapis/genai-toolbox/issues/2123)) ([0641da0](https://redirect.github.com/googleapis/genai-toolbox/commit/0641da0353857317113b2169e547ca69603ddfde)) ([186293e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/186293e1fcbe9bc576aeb360227e638c1df6d57a))


### Bug Fixes

* List tables tools null fix ([genai-toolbox#​2107](https://redirect.github.com/googleapis/genai-toolbox/issues/2107)) ([2b45266](https://redirect.github.com/googleapis/genai-toolbox/commit/2b452665983154041d4cd0ed7d82532e4af682eb)) ([186293e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/186293e1fcbe9bc576aeb360227e638c1df6d57a))

## [0.1.6](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.5...0.1.6) (2025-12-08)


### Features

* **prebuilt/cloud-sql:** Add clone instance tool for cloud sql ([genai-toolbox#​1845](https://redirect.github.com/googleapis/genai-toolbox/issues/1845)) ([5e43630](https://redirect.github.com/googleapis/genai-toolbox/commit/5e43630907aa2d7bc6818142483a33272eab060b)) ([438f03e](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/438f03e135d5e76e7d58e2a0a560d4fbd1cacdac))

## [0.1.5](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.4...0.1.5) (2025-11-18)


### Features

* **source/alloydb, source/cloud-sql-postgres,source/cloud-sql-mysql,source/cloud-sql-mssql:** Use project from env for alloydb and cloud sql control plane tools ([genai-toolbox#​1588](https://redirect.github.com/googleapis/genai-toolbox/issues/1588)) ([12bdd95](https://redirect.github.com/googleapis/genai-toolbox/commit/12bdd954597e49d3ec6b247cc104584c5a4d1943)) ([7f085eb](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/7f085eb47d12a8049318dd0ed28990ba293967a0))
* Added prompt support for toolbox ([genai-toolbox#​1798](https://redirect.github.com/googleapis/genai-toolbox/issues/1798)) ([cd56ea4](https://redirect.github.com/googleapis/genai-toolbox/commit/cd56ea44fbdd149fcb92324e70ee36ac747635db)) ([7f085eb](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/7f085eb47d12a8049318dd0ed28990ba293967a0))

## [0.1.4](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.3...0.1.4) (2025-10-27)

### Bug Fixes

* **sources/mysql:** Escape mysql user agent ([#1707](https://redirect.github.com/googleapis/genai-toolbox/issues/1707)) ([eeb694c](https://redirect.github.com/googleapis/genai-toolbox/commit/eeb694c20facc40a38bfa67073c4cb1f3dd657ff)) ([05248f0](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/05248f0c43238ed98d7fa66031320624e86df9aa))
* **sources/mysql:** Escape program\_name for MySQL ([#1717](https://redirect.github.com/googleapis/genai-toolbox/issues/1717)) ([02f7f8a](https://redirect.github.com/googleapis/genai-toolbox/commit/02f7f8af979057efe99fd138cb1b958130355b68)) ([05248f0](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/05248f0c43238ed98d7fa66031320624e86df9aa))

## [0.1.3](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.2...0.1.3) (2025-10-17)


### Bug Fixes

* update context for install instructions ([#47](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/47)) ([3afaa60](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/3afaa601ef8a55cd051563fb9833c0adce96032d))

## [0.1.2](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.1...0.1.2) (2025-10-13)


### Features

* add full table name to context file ([#34](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/34)) ([2e5337a](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/2e5337ab1aa1991104772fa6ecce94c3fc3931cb))
* **deps:** update dependency googleapis/genai-toolbox to v0.17.0 ([#43](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/43)) ([382f390](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/382f390d75b0f97905e4dd03eb01561491d7bea9))

## [0.1.1](https://github.com/gemini-cli-extensions/cloud-sql-mysql/compare/0.1.0...0.1.1) (2025-09-30)


### Features

* additional instructions for the context file ([#32](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/32)) ([bd680cb](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/bd680cb3c977f5941ba0370a3049e1615f308ae3))
* standardize mcp server names ([#30](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/30)) ([4d663a5](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/4d663a5701cc8ecd11d04acd0197cc46b3640b39))
* update context file to recommend observability extension ([#18](https://github.com/gemini-cli-extensions/cloud-sql-mysql/issues/18)) ([80dcca7](https://github.com/gemini-cli-extensions/cloud-sql-mysql/commit/80dcca71bf96c22fbb6e2d682e298f59cc14ba4b))

## 0.1.0 (2025-09-20)


### Feature

* Add Cloud SQL for MySQL Extension
