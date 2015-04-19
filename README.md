# Ember-cli-deploy-pipeline

This README outlines the details of collaborating on this Ember addon.

## Architecture

A deploy pipeline is a tree of tasks. Each task is an object, provided by another addon (so third parties can extend it). A task only runs if its preceding task succeeds.

Tasks have hooks:
+ `task.run(config)` - do whatever this task does
+ `task.rollback()` - undo whatever this task did
+ `task.cleanup()` - clean up any backups taken in case of rollback

If a task fails, all preceding tasks will be rolled back in reverse order. If no tasks fail, `cleanup()` will be called on every task.

A task is an object, not a singleton, so can be used more than once in a pipeline with different configuration.

Task config can reference data from the output of any preceding task.

Blueprints will be available for the most common pipelines (e.g. Luke Melia, S3+Cloudfront)

`task.run()` will either return null or a POJO if it succeeds, or an `Error` if it fails. If the POJO includes a `message` property this will be logged to the console.

A task's README will document the structure of the required `config` and its output POJO if it has one.

## Installation

* `git clone` this repository
* `npm install`
* `bower install`

## Running

* `ember server`
* Visit your app at http://localhost:4200.

## Running Tests

* `ember test`
* `ember test --server`

## Building

* `ember build`

For more information on using ember-cli, visit [http://www.ember-cli.com/](http://www.ember-cli.com/).
