# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-07T09:27:48Z
- **Commit:** [`565a583`](https://github.com/Hawthorne001/client_java/commit/565a58396c92ddfbe1b64de37c40a0a8c165a612)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.79K | ± 98.55 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.16K | ± 909.25 | ops/s | 1.2x slower |
| prometheusAdd | 50.82K | ± 532.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.91K | ± 1.79K | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 18.59K | ± 70.40 | ops/s | 3.5x slower |
| openTelemetryInc | 14.96K | ± 429.91 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.81K | ± 311.41 | ops/s | 5.1x slower |
| simpleclientInc | 6.60K | ± 72.45 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.37K | ± 35.71 | ops/s | 10x slower |
| simpleclientAdd | 6.26K | ± 394.89 | ops/s | 11x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.30K | ± 15.53 | ops/s | **fastest** |
| prometheusClassic | 7.34K | ± 1.71K | ops/s | 1.7x slower |
| prometheusClassicSingleThread | 4.56K | ± 14.92 | ops/s | 2.7x slower |
| simpleclient | 4.47K | ± 52.68 | ops/s | 2.8x slower |
| prometheusNative | 3.01K | ± 251.88 | ops/s | 4.1x slower |
| openTelemetryExponential | 923.48 | ± 106.31 | ops/s | 13x slower |
| openTelemetryClassic | 811.62 | ± 45.43 | ops/s | 15x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 24.13K | ± 854.46 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.27K | ± 232.08 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 517.38K | ± 8.85K | ops/s | **fastest** |
| prometheusWriteToByteArray | 510.04K | ± 10.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 495.80K | ± 3.48K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 488.55K | ± 7.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48910.918   ± 1794.708  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12809.661    ± 311.411  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14964.092    ± 429.913  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18587.614     ± 70.398  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50821.066    ± 532.621  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65793.969     ± 98.546  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56163.194    ± 909.252  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6259.297    ± 394.887  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6597.028     ± 72.452  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6373.603     ± 35.713  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        811.622     ± 45.429  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        923.478    ± 106.308  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7339.366   ± 1711.198  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12300.323     ± 15.529  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4555.091     ± 14.917  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3006.377    ± 251.882  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4465.522     ± 52.678  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23269.889    ± 232.084  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24129.466    ± 854.459  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488546.087   ± 7682.613  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     495798.759   ± 3477.924  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     510042.385  ± 10837.013  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     517381.450   ± 8845.028  ops/s
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
