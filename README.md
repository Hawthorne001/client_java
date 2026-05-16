# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-16T17:42:23Z
- **Commit:** [`94b33b7`](https://github.com/Hawthorne001/client_java/commit/94b33b7527ce21b12ff2a3f9cd23c63cdb42e274)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.87K | ± 93.17 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.62K | ± 513.94 | ops/s | 1.2x slower |
| prometheusAdd | 48.10K | ± 347.50 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.98K | ± 1.13K | ops/s | 1.4x slower |
| simpleclientInc | 6.13K | ± 60.97 | ops/s | 9.8x slower |
| simpleclientAdd | 6.03K | ± 152.97 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.88K | ± 34.37 | ops/s | 10x slower |
| openTelemetryInc | 5.04K | ± 903.10 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 4.95K | ± 1.02K | ops/s | 12x slower |
| openTelemetryAdd | 4.20K | ± 873.16 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.61K | ± 1.45K | ops/s | **fastest** |
| simpleclient | 4.34K | ± 72.71 | ops/s | 1.3x slower |
| prometheusNative | 2.78K | ± 120.68 | ops/s | 2.0x slower |
| openTelemetryClassic | 727.97 | ± 2.48 | ops/s | 7.7x slower |
| openTelemetryExponential | 559.77 | ± 8.07 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.39K | ± 171.58 | ops/s | **fastest** |
| prometheusWriteToNull | 27.36K | ± 200.91 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 585.49K | ± 1.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 551.22K | ± 19.62K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 546.68K | ± 6.58K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 536.71K | ± 5.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42977.793   ± 1132.680  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4195.927    ± 873.158  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5039.610    ± 903.100  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4954.118   ± 1016.815  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48100.288    ± 347.500  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59868.668     ± 93.166  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51619.561    ± 513.938  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6027.234    ± 152.967  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6126.510     ± 60.973  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5882.742     ± 34.368  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        727.971      ± 2.485  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.767      ± 8.068  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5609.940   ± 1449.284  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2780.873    ± 120.677  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4336.996     ± 72.707  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27391.034    ± 171.582  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27359.362    ± 200.905  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     536708.210   ± 5158.609  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546681.839   ± 6582.998  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     551219.332  ± 19623.647  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     585487.471   ± 1743.795  ops/s
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
