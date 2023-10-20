https://the-guild.dev/graphql/tools/docs/graphql-tag-pluck

> @graphql-tools/graphql-tag-pluck will take JavaScript code as an input and will pluck all template literals provided to graphql-tag.

Many graphql APIs seem to be documented with just strings inside source files; this code will check for them and pull them out.

I found it via checking what [graphql-eslint uses for parsing out graphql](https://github.com/B2o5T/graphql-eslint/blob/32441a898f1218063db33bff06cc46518616ef63/packages/plugin/src/processor.ts#L59)

Part of the larger [graphql-tools](https://github.com/ardatan/graphql-tools) repo, which is [documented here](https://the-guild.dev/graphql/tools/docs/introduction)