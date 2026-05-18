# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-18T19:00:33Z
- **Commit:** [`94b33b7`](https://github.com/Hawthorne001/client_java/commit/94b33b7527ce21b12ff2a3f9cd23c63cdb42e274)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.60K | ± 1.84K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.45K | ± 2.59K | ops/s | 1.2x slower |
| prometheusAdd | 50.77K | ± 435.57 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.93K | ± 1.60K | ops/s | 1.3x slower |
| simpleclientInc | 6.61K | ± 76.78 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.35K | ± 11.82 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 169.00 | ops/s | 10x slower |
| openTelemetryAdd | 3.56K | ± 485.50 | ops/s | 18x slower |
| openTelemetryIncNoLabels | 3.23K | ± 146.00 | ops/s | 20x slower |
| openTelemetryInc | 3.10K | ± 262.82 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 1.55K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 68.17 | ops/s | 1.2x slower |
| prometheusNative | 2.76K | ± 256.51 | ops/s | 1.9x slower |
| openTelemetryClassic | 762.94 | ± 24.67 | ops/s | 7.0x slower |
| openTelemetryExponential | 610.23 | ± 71.09 | ops/s | 8.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.40K | ± 788.70 | ops/s | **fastest** |
| prometheusWriteToNull | 23.31K | ± 1.26K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 516.37K | ± 3.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.56K | ± 4.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.61K | ± 2.19K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 485.76K | ± 2.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47927.231   ± 1602.729  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3556.030    ± 485.495  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3101.388    ± 262.818  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3230.522    ± 146.002  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50773.885    ± 435.568  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64601.682   ± 1840.494  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55449.347   ± 2589.525  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6316.545    ± 169.004  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6612.815     ± 76.783  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6346.127     ± 11.816  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        762.944     ± 24.665  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        610.235     ± 71.092  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5336.941   ± 1554.946  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2762.467    ± 256.513  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4440.243     ± 68.170  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23396.666    ± 788.697  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23308.343   ± 1255.691  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485760.648   ± 2730.591  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488607.102   ± 2187.394  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503561.514   ± 4406.188  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     516366.149   ± 3894.073  ops/s
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
