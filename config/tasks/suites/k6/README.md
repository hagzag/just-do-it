# k6 intro

## Install

```bash
brew install k6
```

## Run

```bash
k6 run api-test.js
```

## Run with iterations

```bash
k6 run --iterations 10 api-test.js
```

## Use Taskfile to run

* For single test:

```bash
task run
```

* For test with iterations:
```bash
task run-with-itterations
```

* For install:

```bash
task install
```

