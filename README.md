# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-03T15:35:57Z
- **Commit:** [`e43f451`](https://github.com/Hawthorne001/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.42K | ± 1.42K | ops/s |
| prometheusNoLabelsInc | 55.36K | ± 899.77 | ops/s |
| prometheusAdd | 51.03K | ± 714.69 | ops/s |
| codahaleIncNoLabels | 47.92K | ± 1.77K | ops/s |
| openTelemetryIncNoLabels | 18.20K | ± 325.44 | ops/s |
| openTelemetryInc | 14.98K | ± 343.57 | ops/s |
| openTelemetryAdd | 12.90K | ± 125.46 | ops/s |
| simpleclientInc | 6.56K | ± 40.89 | ops/s |
| simpleclientAdd | 6.51K | ± 58.44 | ops/s |
| simpleclientNoLabelsInc | 6.36K | ± 31.86 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.07K | ± 320.40 | ops/s |
| prometheusClassic | 6.14K | ± 1.57K | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 51.86 | ops/s |
| simpleclient | 4.38K | ± 26.00 | ops/s |
| prometheusNative | 2.88K | ± 267.74 | ops/s |
| openTelemetryClassic | 865.93 | ± 59.73 | ops/s |
| openTelemetryExponential | 664.14 | ± 19.70 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.32K | ± 437.02 | ops/s |
| openMetricsWriteToNull | 23.40K | ± 284.98 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 492.72K | ± 6.52K | ops/s |
| prometheusWriteToNull | 492.56K | ± 8.31K | ops/s |
| openMetricsWriteToNull | 472.09K | ± 12.67K | ops/s |
| openMetricsWriteToByteArray | 467.09K | ± 7.97K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47918.900   ± 1771.666  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12901.976    ± 125.460  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14984.654    ± 343.571  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18195.274    ± 325.439  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51029.285    ± 714.687  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64416.546   ± 1415.897  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55361.372    ± 899.773  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6508.540     ± 58.444  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6562.761     ± 40.892  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6364.661     ± 31.858  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        865.932     ± 59.733  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        664.137     ± 19.700  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6137.070   ± 1572.776  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12071.822    ± 320.404  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4543.847     ± 51.856  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2884.579    ± 267.744  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4382.293     ± 25.996  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23402.002    ± 284.981  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24315.417    ± 437.021  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467085.751   ± 7969.111  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472086.556  ± 12670.669  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492715.507   ± 6521.335  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492555.585   ± 8305.834  ops/s
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
