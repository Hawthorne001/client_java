# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-11T17:00:19Z
- **Commit:** [`39a91dd`](https://github.com/Hawthorne001/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.94K | ± 251.18 | ops/s |
| prometheusNoLabelsInc | 55.99K | ± 747.62 | ops/s |
| prometheusAdd | 51.39K | ± 410.12 | ops/s |
| codahaleIncNoLabels | 48.70K | ± 1.36K | ops/s |
| openTelemetryIncNoLabels | 18.54K | ± 63.33 | ops/s |
| openTelemetryInc | 15.09K | ± 81.50 | ops/s |
| openTelemetryAdd | 12.93K | ± 30.56 | ops/s |
| simpleclientInc | 6.62K | ± 63.51 | ops/s |
| simpleclientAdd | 6.42K | ± 31.11 | ops/s |
| simpleclientNoLabelsInc | 6.36K | ± 41.15 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.32K | ± 35.07 | ops/s |
| prometheusClassic | 7.52K | ± 173.37 | ops/s |
| prometheusClassicSingleThread | 4.57K | ± 51.70 | ops/s |
| simpleclient | 4.44K | ± 16.85 | ops/s |
| prometheusNative | 3.00K | ± 310.39 | ops/s |
| openTelemetryExponential | 872.49 | ± 123.90 | ops/s |
| openTelemetryClassic | 789.40 | ± 17.40 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.28K | ± 317.42 | ops/s |
| openMetricsWriteToNull | 22.72K | ± 545.43 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 495.85K | ± 4.95K | ops/s |
| prometheusWriteToByteArray | 486.44K | ± 5.43K | ops/s |
| openMetricsWriteToNull | 474.81K | ± 5.65K | ops/s |
| openMetricsWriteToByteArray | 465.89K | ± 3.35K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48700.495   ± 1356.790  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12926.840     ± 30.564  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15086.720     ± 81.497  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18542.569     ± 63.325  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51393.991    ± 410.115  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65944.521    ± 251.176  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55986.952    ± 747.622  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6423.710     ± 31.107  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6622.279     ± 63.511  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6356.087     ± 41.148  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        789.395     ± 17.399  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        872.494    ± 123.902  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7516.029    ± 173.373  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12322.469     ± 35.074  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4568.155     ± 51.705  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3003.005    ± 310.388  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4439.215     ± 16.846  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      22719.683    ± 545.430  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23279.198    ± 317.418  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     465887.827   ± 3351.276  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474808.135   ± 5645.625  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486441.107   ± 5434.233  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495850.741   ± 4946.813  ops/s
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
