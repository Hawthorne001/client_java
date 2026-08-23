# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-22T12:25:55Z
- **Commit:** [`dfeba03`](https://github.com/Hawthorne001/client_java/commit/dfeba0312720214e99c42a890fa3e2c0f7c6039d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.53K | ± 409.94 | ops/s |
| prometheusNoLabelsInc | 56.78K | ± 382.42 | ops/s |
| prometheusAdd | 50.91K | ± 497.96 | ops/s |
| codahaleIncNoLabels | 47.21K | ± 391.85 | ops/s |
| openTelemetryIncNoLabels | 18.59K | ± 55.97 | ops/s |
| openTelemetryInc | 15.09K | ± 369.77 | ops/s |
| openTelemetryAdd | 12.64K | ± 51.40 | ops/s |
| simpleclientInc | 6.49K | ± 103.84 | ops/s |
| simpleclientAdd | 6.47K | ± 68.42 | ops/s |
| simpleclientNoLabelsInc | 6.33K | ± 39.80 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.28K | ± 24.75 | ops/s |
| prometheusClassic | 7.03K | ± 2.26K | ops/s |
| prometheusClassicSingleThread | 4.55K | ± 48.49 | ops/s |
| simpleclient | 4.36K | ± 119.21 | ops/s |
| prometheusNative | 3.06K | ± 276.61 | ops/s |
| openTelemetryExponential | 877.18 | ± 166.07 | ops/s |
| openTelemetryClassic | 775.94 | ± 22.30 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.28K | ± 613.76 | ops/s |
| openMetricsWriteToNull | 23.29K | ± 473.95 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 505.32K | ± 3.45K | ops/s |
| prometheusWriteToByteArray | 502.86K | ± 6.39K | ops/s |
| openMetricsWriteToNull | 488.95K | ± 1.99K | ops/s |
| openMetricsWriteToByteArray | 484.74K | ± 1.86K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47210.830    ± 391.851  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12639.629     ± 51.398  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15094.226    ± 369.775  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18589.899     ± 55.974  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50907.399    ± 497.961  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65532.156    ± 409.940  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56784.551    ± 382.423  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6469.033     ± 68.416  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6485.428    ± 103.845  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6327.841     ± 39.795  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        775.941     ± 22.302  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        877.182    ± 166.068  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7025.307   ± 2259.444  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12278.642     ± 24.755  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4546.397     ± 48.493  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3059.293    ± 276.609  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4361.952    ± 119.212  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23285.498    ± 473.953  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24275.932    ± 613.761  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484736.853   ± 1859.728  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488945.251   ± 1992.399  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     502862.584   ± 6386.662  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     505322.384   ± 3448.504  ops/s
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
