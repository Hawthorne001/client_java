# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-07T09:57:02Z
- **Commit:** [`39b7be7`](https://github.com/Hawthorne001/client_java/commit/39b7be77c78d870ade240791d6066f1b7464fdfa)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.04K | ± 830.40 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.02K | ± 1.69K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.22K | ± 897.89 | ops/s | 1.1x slower |
| prometheusAdd | 28.47K | ± 359.12 | ops/s | 1.1x slower |
| simpleclientInc | 7.17K | ± 73.34 | ops/s | 4.3x slower |
| simpleclientAdd | 6.82K | ± 42.58 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.64K | ± 115.89 | ops/s | 4.7x slower |
| openTelemetryInc | 1.45K | ± 58.93 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 1.41K | ± 97.76 | ops/s | 22x slower |
| openTelemetryAdd | 1.38K | ± 45.68 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.58K | ± 31.15 | ops/s | **fastest** |
| prometheusClassic | 3.18K | ± 290.17 | ops/s | 1.4x slower |
| prometheusNative | 2.39K | ± 57.64 | ops/s | 1.9x slower |
| openTelemetryClassic | 488.22 | ± 9.14 | ops/s | 9.4x slower |
| openTelemetryExponential | 431.54 | ± 24.81 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 337.81K | ± 3.08K | ops/s | **fastest** |
| prometheusWriteToByteArray | 334.57K | ± 3.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 311.89K | ± 2.54K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 309.33K | ± 1.59K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29221.291    ± 897.894  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1378.211     ± 45.679  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1451.795     ± 58.929  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1414.324     ± 97.758  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28473.311    ± 359.117  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31041.850    ± 830.399  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30024.201   ± 1694.030  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6822.484     ± 42.582  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7171.363     ± 73.344  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6638.500    ± 115.893  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        488.217      ± 9.136  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        431.544     ± 24.807  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3176.569    ± 290.171  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2390.142     ± 57.645  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4578.188     ± 31.153  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     309332.189   ± 1591.077  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     311893.785   ± 2541.461  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     334566.177   ± 3653.282  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     337808.538   ± 3084.664  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
