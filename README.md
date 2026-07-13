# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-12T11:47:53Z
- **Commit:** [`1bb6c6d`](https://github.com/Hawthorne001/client_java/commit/1bb6c6dfc3a31b410b135baa12ee8ee7671897bc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 78.30K | ± 1.75K | ops/s | **fastest** |
| prometheusNoLabelsInc | 63.84K | ± 5.07K | ops/s | 1.2x slower |
| prometheusAdd | 62.06K | ± 706.77 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 56.37K | ± 2.23K | ops/s | 1.4x slower |
| simpleclientInc | 8.00K | ± 20.00 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 7.62K | ± 41.43 | ops/s | 10x slower |
| simpleclientAdd | 7.51K | ± 310.64 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 6.78K | ± 1.69K | ops/s | 12x slower |
| openTelemetryInc | 5.60K | ± 1.25K | ops/s | 14x slower |
| openTelemetryAdd | 4.94K | ± 1.11K | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassic | 8.21K | ± 1.72K | ops/s | **fastest** |
| simpleclient | 5.84K | ± 66.65 | ops/s | 1.4x slower |
| prometheusNative | 3.44K | ± 54.07 | ops/s | 2.4x slower |
| openTelemetryClassic | 882.63 | ± 11.56 | ops/s | 9.3x slower |
| openTelemetryExponential | 689.99 | ± 39.93 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 35.54K | ± 228.78 | ops/s | **fastest** |
| openMetricsWriteToNull | 35.39K | ± 339.61 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 694.93K | ± 2.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 674.82K | ± 4.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 659.41K | ± 2.52K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 638.00K | ± 4.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56371.023   ± 2227.315  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4936.141   ± 1108.237  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5600.685   ± 1253.370  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       6776.090   ± 1693.837  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62059.026    ± 706.771  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      78298.597   ± 1753.208  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63841.119   ± 5069.640  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7512.465    ± 310.637  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7996.318     ± 20.000  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7622.463     ± 41.434  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        882.626     ± 11.563  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        689.994     ± 39.929  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8206.715   ± 1719.741  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3435.736     ± 54.073  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5837.525     ± 66.645  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35393.994    ± 339.614  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35544.922    ± 228.785  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     638001.867   ± 4290.821  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     659411.802   ± 2520.513  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     674817.890   ± 4936.483  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     694931.795   ± 2901.496  ops/s
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
