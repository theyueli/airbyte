# Elasticsearch source

This is the repository for the Elasticsearch source connector, written in Java using Elasticsearch's High Level Rest Client([HLRC](https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/java-rest-high.html)).
For information about how to use this connector within Airbyte, see [the documentation](https://docs.airbyte.io/integrations/sources/elasticsearch).

## Local development

#### Building via Gradle

From the Airbyte repository root, run:

```
./gradlew :airbyte-integrations:connectors:source-elasticsearch:build
```

#### Create credentials

Credentials can be provided in three ways:

1. Basic
2.

### Locally running the connector docker image

#### Build

Build the connector image via Gradle:

```
./gradlew :airbyte-integrations:connectors:source-elasticsearch:buildConnectorImage
```

Once built, the docker image name and tag on your host will be `airbyte/source-elasticsearch:dev`.
the Dockerfile.

#### Run

Then run any of the connector commands as follows:

```
docker run --rm airbyte/source-elasticsearch:dev spec
docker run --rm -v $(pwd)/secrets:/secrets airbyte/source-elasticsearch:dev check --config /secrets/config.json
docker run --rm -v $(pwd)/secrets:/secrets airbyte/source-elasticsearch:dev discover --config /secrets/config.json
docker run --rm -v $(pwd)/secrets:/secrets -v $(pwd)/integration_tests:/integration_tests airbyte/source-elasticsearch:dev read --config /secrets/config.json --catalog /integration_tests/configured_catalog.json
```

#### Sync Mode Support

Current version of this connector only allows the `FULL REFRESH` mode.

## Testing

We use `JUnit` for Java tests.

### Unit and Integration Tests

Place unit tests under `src/test/io/airbyte/integrations/sources/elasticsearch-test`.

#### Acceptance Tests

Airbyte has a standard test suite that all destination connectors must pass. See example(s) in
`src/test-integration/java/io/airbyte/integrations/sources/elasticsearch/`.

### Using gradle to run tests

All commands should be run from airbyte project root.
To run unit tests:

```
./gradlew :airbyte-integrations:connectors:source-elasticsearch:unitTest
```

To run acceptance and custom integration tests:

```
./gradlew :airbyte-integrations:connectors:source-elasticsearch:integrationTest
```

## Dependency Management

### Publishing a new version of the connector

You've checked out the repo, implemented a million dollar feature, and you're ready to share your changes with the world. Now what?

1. Make sure your changes are passing our test suite: `airbyte-ci connectors --name=source-elasticsearch test`
2. Bump the connector version in `metadata.yaml`: increment the `dockerImageTag` value. Please follow [semantic versioning for connectors](https://docs.airbyte.com/contributing-to-airbyte/resources/pull-requests-handbook/#semantic-versioning-for-connectors).
3. Make sure the `metadata.yaml` content is up to date.
4. Make the connector documentation and its changelog is up to date (`docs/integrations/sources/elasticsearch.md`).
5. Create a Pull Request: use [our PR naming conventions](https://docs.airbyte.com/contributing-to-airbyte/resources/pull-requests-handbook/#pull-request-title-convention).
6. Pat yourself on the back for being an awesome contributor.
7. Someone from Airbyte will take a look at your PR and iterate with you to merge it into master.
