# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-29T09:30:02Z
- **Commit:** [`372423c`](https://github.com/Hawthorne001/client_java/commit/372423c0e54cff6206e9ba5845bd33f69f6c033c)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| codahaleIncNoLabels | 37.19K | ± 1.17K | ops/s | **fastest** |
| prometheusAdd | 36.64K | ± 464.66 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 35.94K | ± 1.34K | ops/s | 1.0x slower |
| prometheusInc | 35.42K | ± 527.13 | ops/s | 1.0x slower |
| openTelemetryIncNoLabels | 25.39K | ± 356.03 | ops/s | 1.5x slower |
| openTelemetryInc | 22.48K | ± 390.73 | ops/s | 1.7x slower |
| openTelemetryAdd | 19.66K | ± 181.57 | ops/s | 1.9x slower |
| simpleclientInc | 9.16K | ± 94.09 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 9.04K | ± 108.56 | ops/s | 4.1x slower |
| simpleclientAdd | 8.91K | ± 203.71 | ops/s | 4.2x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 8.95K | ± 83.27 | ops/s | **fastest** |
| simpleclient | 6.13K | ± 79.05 | ops/s | 1.5x slower |
| prometheusClassicSingleThread | 4.37K | ± 191.88 | ops/s | 2.0x slower |
| prometheusClassic | 3.36K | ± 232.04 | ops/s | 2.7x slower |
| prometheusNative | 2.11K | ± 348.02 | ops/s | 4.2x slower |
| openTelemetryClassic | 527.70 | ± 30.85 | ops/s | 17x slower |
| openTelemetryExponential | 462.64 | ± 31.64 | ops/s | 19x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 25.02K | ± 505.84 | ops/s | **fastest** |
| prometheusWriteToNull | 24.97K | ± 370.10 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToByteArray | 341.46K | ± 2.75K | ops/s | **fastest** |
| prometheusWriteToNull | 339.97K | ± 4.36K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 324.84K | ± 2.27K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 324.72K | ± 3.70K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      37187.077   ± 1165.749  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19658.244    ± 181.569  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      22479.904    ± 390.735  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      25385.632    ± 356.032  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      36644.627    ± 464.659  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      35418.926    ± 527.135  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      35935.117   ± 1339.940  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       8906.600    ± 203.712  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9164.867     ± 94.086  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       9036.017    ± 108.558  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        527.704     ± 30.846  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        462.639     ± 31.638  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3363.534    ± 232.038  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       8947.061     ± 83.270  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4374.235    ± 191.880  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2107.906    ± 348.023  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6131.484     ± 79.051  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      25020.172    ± 505.835  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24965.614    ± 370.103  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     324720.714   ± 3704.526  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     324842.938   ± 2268.581  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     341464.318   ± 2747.524  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     339968.849   ± 4360.818  ops/s
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
