# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-09T09:35:22Z
- **Commit:** [`565a583`](https://github.com/Hawthorne001/client_java/commit/565a58396c92ddfbe1b64de37c40a0a8c165a612)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 64.52K | ± 1.97K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.01K | ± 445.86 | ops/s | 1.1x slower |
| prometheusAdd | 50.97K | ± 232.55 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.58K | ± 1.82K | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 18.29K | ± 113.57 | ops/s | 3.5x slower |
| openTelemetryInc | 14.96K | ± 236.71 | ops/s | 4.3x slower |
| openTelemetryAdd | 12.91K | ± 92.52 | ops/s | 5.0x slower |
| simpleclientInc | 6.59K | ± 94.86 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.45K | ± 122.57 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 179.15 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.24K | ± 73.69 | ops/s | **fastest** |
| prometheusClassic | 5.12K | ± 1.63K | ops/s | 2.4x slower |
| prometheusClassicSingleThread | 4.58K | ± 39.37 | ops/s | 2.7x slower |
| simpleclient | 4.39K | ± 54.36 | ops/s | 2.8x slower |
| prometheusNative | 2.96K | ± 349.08 | ops/s | 4.1x slower |
| openTelemetryExponential | 881.67 | ± 23.77 | ops/s | 14x slower |
| openTelemetryClassic | 836.08 | ± 63.62 | ops/s | 15x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 23.57K | ± 548.27 | ops/s | **fastest** |
| prometheusWriteToNull | 23.29K | ± 147.98 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 438.30K | ± 19.48K | ops/s | **fastest** |
| openMetricsWriteToNull | 422.16K | ± 6.61K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 419.92K | ± 15.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 416.73K | ± 7.80K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49582.990   ± 1823.899  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12914.721     ± 92.524  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14960.594    ± 236.710  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18291.501    ± 113.568  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50968.846    ± 232.554  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64520.991   ± 1972.853  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57005.751    ± 445.856  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6317.797    ± 179.150  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6593.244     ± 94.860  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6445.718    ± 122.573  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        836.081     ± 63.623  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        881.666     ± 23.770  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5115.819   ± 1626.352  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12240.106     ± 73.689  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4578.053     ± 39.374  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2956.281    ± 349.081  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4391.875     ± 54.356  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23571.067    ± 548.271  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23286.912    ± 147.981  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     416726.614   ± 7804.178  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     422163.653   ± 6607.234  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     419921.902  ± 15100.867  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     438295.119  ± 19479.162  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
