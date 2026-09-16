# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-15T16:53:47Z
- **Commit:** [`fcc4466`](https://github.com/Hawthorne001/client_java/commit/fcc4466e36262d155e3f7b0211fd8da6b013e3af)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.46K | ± 1.56K | ops/s |
| prometheusNoLabelsInc | 56.63K | ± 353.04 | ops/s |
| prometheusAdd | 51.12K | ± 838.75 | ops/s |
| codahaleIncNoLabels | 50.26K | ± 154.78 | ops/s |
| openTelemetryIncNoLabels | 18.41K | ± 156.24 | ops/s |
| openTelemetryInc | 14.90K | ± 508.32 | ops/s |
| openTelemetryAdd | 12.94K | ± 79.98 | ops/s |
| simpleclientInc | 6.56K | ± 37.07 | ops/s |
| simpleclientNoLabelsInc | 6.45K | ± 123.50 | ops/s |
| simpleclientAdd | 6.20K | ± 332.35 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.30K | ± 31.93 | ops/s |
| prometheusClassic | 5.32K | ± 1.83K | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 19.85 | ops/s |
| simpleclient | 4.43K | ± 36.54 | ops/s |
| prometheusNative | 2.92K | ± 224.18 | ops/s |
| openTelemetryClassic | 844.45 | ± 19.49 | ops/s |
| openTelemetryExponential | 748.56 | ± 155.28 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.41K | ± 948.97 | ops/s |
| openMetricsWriteToNull | 23.13K | ± 740.59 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 417.91K | ± 6.16K | ops/s |
| prometheusWriteToByteArray | 413.04K | ± 6.16K | ops/s |
| openMetricsWriteToNull | 405.97K | ± 6.08K | ops/s |
| openMetricsWriteToByteArray | 402.89K | ± 2.39K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50264.490    ± 154.775  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12936.558     ± 79.981  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14902.131    ± 508.323  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18414.963    ± 156.239  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51115.766    ± 838.752  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64456.843   ± 1557.352  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56634.074    ± 353.042  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6202.714    ± 332.346  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6558.053     ± 37.074  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6453.889    ± 123.500  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        844.449     ± 19.488  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        748.563    ± 155.281  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5316.655   ± 1827.490  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12297.650     ± 31.932  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4541.699     ± 19.854  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2919.145    ± 224.177  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4430.715     ± 36.537  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23126.376    ± 740.593  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23412.890    ± 948.973  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     402885.412   ± 2390.250  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     405969.627   ± 6081.871  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     413043.443   ± 6160.696  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     417907.564   ± 6164.054  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
