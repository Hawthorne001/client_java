# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-25T20:28:32Z
- **Commit:** [`5ee188f`](https://github.com/Hawthorne001/client_java/commit/5ee188ff288806f76e53a89d32431a93bb53da11)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.56K | ± 26.88 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.14K | ± 364.59 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.47K | ± 1.19K | ops/s | 1.1x slower |
| prometheusAdd | 28.45K | ± 36.99 | ops/s | 1.1x slower |
| simpleclientInc | 6.75K | ± 222.10 | ops/s | 4.7x slower |
| simpleclientAdd | 6.66K | ± 86.55 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.61K | ± 13.43 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 2.59K | ± 177.40 | ops/s | 12x slower |
| openTelemetryInc | 2.52K | ± 142.31 | ops/s | 13x slower |
| openTelemetryAdd | 2.35K | ± 146.26 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 48.98 | ops/s | **fastest** |
| prometheusClassic | 3.50K | ± 181.89 | ops/s | 1.3x slower |
| prometheusNative | 1.97K | ± 20.29 | ops/s | 2.3x slower |
| openTelemetryClassic | 632.61 | ± 14.57 | ops/s | 7.1x slower |
| openTelemetryExponential | 442.82 | ± 18.77 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.27K | ± 51.31 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.09K | ± 166.09 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 325.04K | ± 2.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 323.92K | ± 1.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 301.70K | ± 2.12K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.70K | ± 2.34K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29470.899   ± 1191.828  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2350.977    ± 146.257  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2522.488    ± 142.309  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2585.508    ± 177.403  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28449.541     ± 36.994  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31562.062     ± 26.876  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31135.999    ± 364.586  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6657.718     ± 86.545  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6752.359    ± 222.103  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6609.437     ± 13.429  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        632.612     ± 14.570  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        442.819     ± 18.774  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3501.190    ± 181.893  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1970.309     ± 20.286  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4509.905     ± 48.979  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18085.415    ± 166.086  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18266.776     ± 51.311  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297704.538   ± 2335.564  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     301704.322   ± 2123.913  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     323922.228   ± 1228.574  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     325036.997   ± 2109.518  ops/s
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
